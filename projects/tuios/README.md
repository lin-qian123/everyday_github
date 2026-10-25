<!-- markdownlint-disable MD013 -->

# TUIOS：Agent 终端工作台与 0.11.0 权限修复更新

- 主上游：[Gaurav-Gosain/tuios](https://github.com/Gaurav-Gosain/tuios)；repository ID `1051789550`。
- 采样日期：2026-10-26（Asia/Shanghai）；分类：Coding Agents 与终端助手。
- API 累计快照：5,978 stars / 276 forks / 47 open issues（含 PR 口径）；与榜单日增分开。
- 默认分支 `main`，本页静态依据固定在 `547791a0bf8dd10656680be6d483e913ac2f6faf`。发行 API 首项 [v0.11.0](https://github.com/Gaurav-Gosain/tuios/releases/tag/v0.11.0)，UTC 2026-10-25T11:40:35Z，正式发行。
- 核验层级：读取上游文档、许可、元数据及所列部分实现；未安装运行上游、调用模型或复现实验。

## 定位

TUIOS 是 Go 编写的终端 multiplexer / window manager，把 pane、workspace、BSP tiling、持久 daemon、Agent 状态和 Inbox 放在当前终端中。0.11.0 发行扩展了跨机 Agent 对话与产物查看、fan 对比、TML 表单及插件流程。本页在原 2026-09-30 说明基础上刷新，而非重复建立项目。

## 用法

可选择固定 0.11.0 的安装方式，先审阅制品与权限；以下为文档入口，本轮未执行：

```bash
go install github.com/Gaurav-Gosain/tuios/cmd/tuios@v0.11.0
tuios
tuios integration install claude-code
tuios doctor agents
```

integration install 会为宿主安装 hooks / 集成，并非只读查看。Inbox 的权限提示代答另需显式配置；按主线文档可选 strict mode 和有限 grants。**更换二进制后旧 daemon 仍运行旧构建**，上游要求再运行 tuios restart-server；应先审查活进程与可恢复 Agent，重启会恢复布局 / 历史与新 shell，不是所有旧进程无损续跑。

## 原理

Bubble Tea 界面连接管理 PTY 和会话的 daemon，hooks、屏幕规则与宿主集成上报 Agent 状态。Inbox 汇集审批、提问、邮件和错误；fan 可以给多个独立 worktree 启动同一任务，再比较候选。pane grant 管理通过 TUIOS 控制面的动作；MCP、tmux shim 和远端主机把这套控制面延伸给其他工具，不等于限制这些进程自身的全部 OS 能力。

## 价值

适合同时运行多种编码 CLI、经常切换本机与远端会话的人：可以把“谁在等输入、改了什么、哪个尝试值得保留”集中查看。0.11.0 的权限修复也说明状态和代答边界应进入采用检查，而非只看终端截图和启动速度。

## 风险边界

- **已发布的中等级别公告 GHSA-78rj-pghh-vh42**：影响 ≤0.10.1，修复版为 0.11.0。公告描述在默认 open mode 下，同一 daemon 的恶意 pane 可借状态更新绕过另一 Agent 提示的代答限制。这里记录上游公告和修复声明，本轮未复现利用或验证补丁。
- 主线文档默认 pane 可有较宽权限；strict / grants 是 TUIOS 控制面策略，不能替代 OS 沙箱。持有真实终端、SSH agent、环境变量和文件的进程仍需最小权限。
- 多客户端附着同一 session 时均有完整控制，不设每客户端权限级别。远端 SSH、网页入口和 native plugin 的批准 / grants 各需独立审查。
- **上游 README 明确没有 X / Twitter 账号、没有 token 或 presale，并点名警告冒充账号 @tuiosdev。** 本库只转述并链接一手声明，未调查该账号或验证其传播规模，也不把它列作官方渠道。
- SECURITY.md 仍写仅 main 正式支持、tagged prerelease 尽力支持，与当前非预发行 v0.11.0 元数据有措辞差异，不能据此承诺长期维护或响应时限。代码为 MIT。

## 补充建议

先核对已装二进制、daemon 和各远端主机版本；旧版本按公告评估升级，并在可丢弃会话验证重启、Agent 恢复、Inbox 归属与有限 grants。插件固定源码 / 锁定文件，审批前查看实际权限。对历史会话中可能产生的误答单独复核；项目身份以仓库与 tuios.dev 回链为准。

## 参考资料

- [README.md](https://github.com/Gaurav-Gosain/tuios/blob/547791a0bf8dd10656680be6d483e913ac2f6faf/README.md)。
- [LICENSE](https://github.com/Gaurav-Gosain/tuios/blob/547791a0bf8dd10656680be6d483e913ac2f6faf/LICENSE)。
- [SECURITY.md](https://github.com/Gaurav-Gosain/tuios/blob/547791a0bf8dd10656680be6d483e913ac2f6faf/SECURITY.md)。
- [docs/AGENT_STATE.md](https://github.com/Gaurav-Gosain/tuios/blob/547791a0bf8dd10656680be6d483e913ac2f6faf/docs/AGENT_STATE.md)。
- [docs/SESSIONS.md](https://github.com/Gaurav-Gosain/tuios/blob/547791a0bf8dd10656680be6d483e913ac2f6faf/docs/SESSIONS.md)。
- [权限公告 GHSA-78rj-pghh-vh42](https://github.com/Gaurav-Gosain/tuios/security/advisories/GHSA-78rj-pghh-vh42)。
- [仓库 API](https://api.github.com/repos/Gaurav-Gosain/tuios)、[发行 API](https://api.github.com/repos/Gaurav-Gosain/tuios/releases?per_page=1)；动态元数据仅代表本轮采样。
- 事实来源为以上一手材料；价值、风险评估和建议为本库工程判断，未当作上游实测结果。
