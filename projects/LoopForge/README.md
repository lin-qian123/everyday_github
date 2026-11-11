<!-- markdownlint-disable MD013 -->

# LoopForge：带脚本、复核和人工关卡的 Coding Agent 交付流程

- 上游：[`Tencent/LoopForge`](https://github.com/Tencent/LoopForge)；仓库 ID：`1314510108`。
- 核读：2026-11-12（Asia/Shanghai）；主线固定于 [`c87694a3d9fe`](https://github.com/Tencent/LoopForge/tree/c87694a3d9fee16dc399f4cd5331cd47b1b72cef)。
- 热度快照：313 stars / 60 forks / 57 open issues（含 PR）；来自 [GitHub API](https://api.github.com/repos/Tencent/LoopForge)，不代表采用量或质量。

## 定位

自托管的软件交付工作台，用聊天或可版本化 SOP 编排 Coding Agent、确定性脚本、人工关卡和交付物。它调用现有 CodeBuddy、Codex、Claude Code 等执行器，并不替代模型或 CLI。今天官方 Go daily +76；平台稳定发行 v0.3.6 于 UTC 11-11 发布，[Local npm 包 `loopforge-cli`](https://registry.npmjs.org/loopforge-cli/latest) 当前为 0.2.2，两套版本分别跟踪。

GitHub API 标为 NOASSERTION，实际根 LICENSE 明确为 MIT 并保留第三方组件原许可；不能把识别失败写成无许可。

## 用法

平台路径按当前稳定发行固定 checkout（本轮未执行）：

```bash
git clone --branch v0.3.6 https://github.com/Tencent/LoopForge.git
cd LoopForge
LOOPFORGE_BIND=127.0.0.1 ./start.sh
```

安装器会检查依赖、拉取固定镜像、创建 MySQL / 平台、配置 session secret 和内置模板；缺失组件可能触发系统安装。先限制网络访问，再创建首个管理员账号。无模型 key 可运行“脚本 + 人工关卡”演示；真正 Agent 步骤另需凭据与配额。

只用现有宿主可走 Local：`npx -y loopforge-cli@0.2.2 install codex` 后按 Classic 入口 `$devflow-codex "需求"` 使用；Portable 的安装命令是 `skills install codex`，入口 `$devflow`。两版在同一项目同一宿主互斥，不要混用状态。Local 需要 Node >=20、Python >=3.8；目前只运行内置流程，平台自定义 SOP 导出到独立 Local 仍属计划功能。

## 原理

平台把 Agent、Script、Human gate、Sub-SOP 和 Preview 节点串成依赖图；每步定义角色、工具、模型、交付物和失败返回边。需求、运行、日志、关卡与 PR/MR 交付关联，失败时可返工、暂停或重跑。

Compose 平台持有宿主 Docker socket，用独立 sibling 容器和绑定的 workspace 运行任务；沙箱本身不挂 socket。Local 则通过宿主插件 / 技能运行，并在 `artifacts/{task_slug}/` 保存需求、设计、复核和测试证据。两种执行权限模型不能混为一谈。

## 价值

适合团队把“这次让模型修一下”变成可重复的步骤、可检查的制品和有责任人的验收。确定性脚本处理构建 / 测试，人工关卡保留关键判断，能减少仅看聊天回答就交付的盲区。

作者记录了真实和模拟验收，也明确了跳过项和历史部署差异；这些是上游证据，本轮没有重新运行。内置 token 金额采用公开标准价测算和覆盖率，并不是供应商实际账单。

## 风险边界

- 默认 `LOOPFORGE_BIND=0.0.0.0`、`AGENTFLOW_ALLOW_SIGNUP=true`；第一个账号成为管理员。部署时先收紧入口，受不信任网络可达时关闭注册，HTTPS 反代按文档配置 secure cookies。
- 当前为受信任团队模型：登录用户可列出全部项目、需求与运行；项目修改有 owner/admin 控制，不能据此声称多租户内容保密。
- Docker socket 等同宿主高权限。任务容器隔离不消除平台控制面的影响范围；可按文档移除 socket 并分离执行机器，仍须独立验证权限和挂载。
- 模型 / GitHub 授权、共享 CodeBuddy key、第三方 MCP 和运行日志都需治理。Local 日志可能含工具参数与输出；本地 dashboard 不等于宿主或模型调用不联网。
- 升级必须审查现有安装的数据迁移；文档说明应用启动不自动迁移，不要对新库盲重放全部历史 SQL。人工批准只针对实际验收制品，不能把改动后的代码沿用旧批准。
- `mode=direct` 可合并到共享分支；启用前约束真实仓库写权限和交付策略。多角色不会自动产生独立判断。

## 补充建议

先用空白试验项目验证无 key 演示、失败返回、取消、恢复与批准后的内容一致性，再接有限权限的模型和仓库。将 Local / 平台、发布包 / 主线、公开标准价 / 实际账单分别记录，保留迁移前备份和恢复演练。

本轮未安装、启动容器、注册账号、连接模型 / 仓库、执行 SOP 或验证隔离。

## 参考资料

- [功能与启动](https://github.com/Tencent/LoopForge/blob/c87694a3d9fee16dc399f4cd5331cd47b1b72cef/README.md)。
- [账号、网络、Docker 与迁移](https://github.com/Tencent/LoopForge/blob/c87694a3d9fee16dc399f4cd5331cd47b1b72cef/docs/deployment.md)。
- [Compose 默认配置](https://github.com/Tencent/LoopForge/blob/c87694a3d9fee16dc399f4cd5331cd47b1b72cef/compose.yaml)。
- [Local 安装与版本边界](https://github.com/Tencent/LoopForge/blob/c87694a3d9fee16dc399f4cd5331cd47b1b72cef/docs/local/usage.md)。
- [上游验收证据及跳过项](https://github.com/Tencent/LoopForge/blob/c87694a3d9fee16dc399f4cd5331cd47b1b72cef/docs/validation.md)。
- [费用统计口径](https://github.com/Tencent/LoopForge/blob/c87694a3d9fee16dc399f4cd5331cd47b1b72cef/docs/token-pricing.md)。
- [安全策略](https://github.com/Tencent/LoopForge/blob/c87694a3d9fee16dc399f4cd5331cd47b1b72cef/SECURITY.md)。
- [MIT 与第三方条款](https://github.com/Tencent/LoopForge/blob/c87694a3d9fee16dc399f4cd5331cd47b1b72cef/LICENSE)。
