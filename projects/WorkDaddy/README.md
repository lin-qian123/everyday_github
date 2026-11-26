<!-- markdownlint-disable MD013 -->

# WorkDaddy：通过 CDP 增强 WorkBuddy 与 CodeBuddy 桌面端

- 上游：[babygoton/WorkDaddy](https://github.com/babygoton/WorkDaddy)，repository ID `1338532566`；2026-11-27 新建档案。
- 快照：3,510 stars / 385 forks / 185 open issues（累计，含 PR）；JavaScript daily +49。
- 最新稳定发行 1.2.23（2026-11-22）；tag SHA `97989701a0d90187d1a88bfcc53433aa5c0d52a4`，main SHA `657b586ca54a067289c923c68a44651899a64f9a`。API compare 为 ahead 1、文件差异为空，两者提交身份仍不同。
- 证据：固定 README、许可、daemon / 注入 / 备份 / 导出 / 诊断局部源码及发行记录；未安装、接入真实客户端、登录、切号或运行自动化。

## 定位

这是第三方桌面增强层，给 WorkBuddy 国内 / 国际版和 CodeBuddy 国内 / 国际版提供账户备份、切换、会话复制、模型管理等功能。CodeBuddy 仅覆盖 Electron 智能体窗口，README 明确不包含 VS Code 编辑器增强面板，且隐藏部分 WorkBuddy 专属增强功能。

它依赖已有官方客户端及登录态，通过本机 Chrome DevTools Protocol（CDP）连接和注入界面。它并不提供独立模型，也没有因为“不修改官方安装包”而获得官方隶属关系或独立的操作系统隔离。

## 用法

1. 先确认官方客户端、品牌和平台。发行 1.2.23 的作者验证列表为 WorkBuddy 5.11.3、WorkBuddy AI 5.7.6，不把该列表扩展为所有客户端版本的验证。
2. 从对应 Releases 选择 WorkDaddy / WorkDaddy AI / CodeDaddy CN / CodeDaddy 包。macOS 启动器使用本机 Node.js，README 建议 22.13 或更新版本；Linux 包内置对应架构 Node.js。
3. 首次试用先备份账户与会话数据，再在临时工作区逐项开启功能。启动会建立后台 daemon 并连接客户端调试接口；源码安装也会创建备份、迁移旧路径和启动服务，不是只读安装。
4. WorkBuddy 的免打扰开关涉及外写目录、命令、批量删除、系统工具和弹窗自动允许。所查代码在无已保存状态时将五项读为 false；已有设置会被保留，不能据此推定任一用户当前状态。
5. 需要退出时分别确认客户端、后台 daemon、调试端口与数据副本；卸载说明明确保留账户备份和运行数据。

本轮没有执行这些步骤，也没有采用 README 中放宽 macOS 安全提示的安装操作。

## 原理

launcher 以调试参数启动目标 Electron，daemon 通过 CDP 观察登录变化、备份认证文件，并用 `Runtime.evaluate` 注入面板。四个 profile 的本地 API 默认端口为 47832–47835，renderer CDP 为 9222–9225；CodeBuddy 还使用主进程调试端口 9244 / 9245。实际端口和绑定以配置为准。

本地 API 有来源判断和 `X-WorkDaddy-Token` 检查，部分公开状态 / 启动器路径有例外；不能写成“所有接口均无认证”，也不能把回环地址当作对同用户进程的强隔离。

免打扰不仅改界面：daemon 会调整宿主 `settings.sandbox` 中的目录、命令排除和批量删除阈值；`autoApprove` 则记录开关，由注入前端自动点允许。UI 的外写说明措辞宽泛，所查实现实际合并具体目录清单，真实作用仍需对目标客户端版本验收。

## 价值

对于经常在多个获授权账户和客户端间工作的用户，它集中处理登录备份、会话归属、限流提示和恢复，减少重复手工步骤。分 profile 和明确身份键有助于避免误把不同客户端的账户混在一起。

1.2.19–1.2.21 的发行记录连续涉及账户身份、删除标记传播和会话同步修复，说明这类工具的关键验收项包括恢复与数据归属。发行声明属于作者证据，本轮未重现这些故障或修复效果。

## 风险边界

| 议题 | 已核事实与边界 |
| --- | --- |
| 凭据与加密 | `backupAuthFile` 原样复制认证文件并设 0600；上游密文信封会保留，旧版明文 auth 也可能保留。导出另使用 scrypt + AES-256-GCM；“导出加密”不能推出全部本地备份都已重新加密。 |
| 权限与执行 | 命令 / 系统工具免确认会改变宿主策略，弹窗自动允许会移除逐次人工判断。批量删除路径保留回收站保护的代码意图，仍需检查目标版本实际行为。 |
| 数据出口 | README 列出官方登录 / 积分 API、GitHub 更新检查和显式模型连通测试；诊断模块默认开启 Sentry，可由关于页或 `WORKDADDY_TELEMETRY=0` 关闭。账号留本机与完全离线是不同命题。 |
| 迁移与同步 | 跨账户复制、删除、分支和旧目录迁移会改变持久数据；备份、回滚和副本归属需要单独验证。账号隔离目录不等于隔离宿主权限或模型服务数据。 |
| 版本耦合 | 注入依赖 Electron、DOM 和客户端存储结构。README 的升级兼容描述不是对未来官方版本的保证。 |
| 许可与服务条款 | GitHub API 为 NOASSERTION，LICENSE 实际写 AGPL-3.0-or-later；官方客户端、商标、账户与模型服务另有各自条件。不能只依据 badge 或 stars 判断复用范围。 |

## 补充建议

1. 固定增强工具和官方客户端版本；记录 profile、端口、开关前后配置与停止方法。
2. 用脱敏测试账户和临时会话核对备份、导入导出、切换、删除及恢复；分别检查明文旧文件、密文信封和加密导出。
3. 每次只开一个增强开关，验证实际命令、目录和回滚效果；将自动续接的额外调用、预算和终止条件纳入观察。
4. 分别评估诊断、模型测试、任务仓库下载和会话复制的数据路径；不要把主题 / 面板功能当作权限审计结果。

## 参考资料

- [仓库 API](https://api.github.com/repos/babygoton/WorkDaddy)、[1.2.23 发行](https://github.com/babygoton/WorkDaddy/releases/tag/1.2.23)、[tag 与 main 比较](https://api.github.com/repos/babygoton/WorkDaddy/compare/1.2.23...657b586ca54a067289c923c68a44651899a64f9a)。
- [固定 README](https://raw.githubusercontent.com/babygoton/WorkDaddy/657b586ca54a067289c923c68a44651899a64f9a/README.md)、[daemon / 权限与 API](https://raw.githubusercontent.com/babygoton/WorkDaddy/657b586ca54a067289c923c68a44651899a64f9a/scripts/daemon.js)、[注入与开关确认](https://raw.githubusercontent.com/babygoton/WorkDaddy/657b586ca54a067289c923c68a44651899a64f9a/scripts/inject.js)。
- [备份与认证兼容](https://raw.githubusercontent.com/babygoton/WorkDaddy/657b586ca54a067289c923c68a44651899a64f9a/scripts/lib.js)、[加密导出](https://raw.githubusercontent.com/babygoton/WorkDaddy/657b586ca54a067289c923c68a44651899a64f9a/scripts/secure-transfer.js)、[诊断默认值](https://raw.githubusercontent.com/babygoton/WorkDaddy/657b586ca54a067289c923c68a44651899a64f9a/scripts/sentry-report.js)、[LICENSE](https://raw.githubusercontent.com/babygoton/WorkDaddy/657b586ca54a067289c923c68a44651899a64f9a/LICENSE)。
