<!-- markdownlint-disable MD013 -->

# TUIOS（Gaurav-Gosain/tuios）

> 上游仓库：<https://github.com/Gaurav-Gosain/tuios> · 归类：Coding Agents 与终端助手 · 本页基于 2026-09-30 的 GitHub API、README、Agent / architecture / remote-machine 文档、Release、Security Policy 与 LICENSE 静态整理，未运行 daemon、接入远端主机或处理真实 Agent 审批。

- 抓取快照：4,312 stars、184 forks、18 open issues。
- 热度信号：GitHub Go Trending 抓取时约 +215 当日 stars。
- 版本与许可：MIT；latest Release 与 tag 均为 `v0.8.1`。

## 定位

TUIOS 是用 Go 构建的终端 multiplexer / window manager，提供 BSP tiling、workspace、持久 daemon、scrollback、远端 host 与 Agent-aware Inbox。它能识别多类 coding-agent CLI，通过 hooks 显示 working / waiting / done / error，并把审批、提问、消息和多 Agent fan-out 汇入同一终端界面。

## 用法

可用 Homebrew、Go install、Docker 或安装脚本获取，执行 `tuios` 进入界面；daemon 模式用 `new` / `attach` 保留 session。`tuios integration install` 为受支持的 Agent 写入状态 hooks，`tuios fan` 可在独立 worktree 启动多宿主任务，`tuios mcp` 暴露受限控制面。远端机器需在 `[hosts]` 中显式配置策略，不能把默认发现当授权。

## 原理

界面采用 Bubble Tea v2 的 Model-View-Update，daemon 保存 session 并管理 PTY。Agent 状态由进程 / 屏幕检测和宿主 hooks 上报，Inbox 聚合 approval、question、mail、error 与完成事件；pane grant 以 `read`、`write`、`fan`、`respond`、`admin` 描述通过 TUIOS 可执行的动作。远端 host、worktree pull 与 MCP 再把相同控制面扩展到多机。

## 价值

并行 Agent 的主要摩擦往往不是启动，而是知道哪个会话在等待、回答谁的问题、如何恢复以及怎样把远端结果带回。TUIOS 把这些信号和终端本体合并，且不强迫团队更换既有 CLI；对混用 Claude Code、Codex、Gemini 或 OpenCode 的工程师尤其有价值。

## 风险边界

- TUIOS 管理真实 PTY 和进程，不是 sandbox；Agent 仍拥有其 OS 用户、环境变量、SSH agent、文件和网络权限。
- pane grant 约束 TUIOS 控制面，不一定约束 Agent 自身 shell 或第三方工具，不能替代系统级隔离和最小权限凭据。
- Inbox 快捷审批会缩短判断时间；错误的 pane / host / worktree 归属可能把确认发送给不期望的进程。
- `fan`、远端 host 与 worktree pull 会扩大代码、prompt 和结果的传播面；主机互信、冲突、secret 和恶意输出须独立治理。
- Security Policy 表示仅最新 main 获正式支持且个人维护无响应时限；即使有 `v0.8.1`，生产采用仍需关注快速变化和恢复路径。
- 安装脚本、hooks、MCP 与 tmux shim 都会增加用户级集成表面，应固定 Release 并审阅写入内容。

## 补充建议

先在无 secret 仓库和专用 OS 用户下验证 session 恢复、审批路由、daemon 重启与多 worktree 冲突。远端 host 使用独立 SSH key、命令 / 目录 allowlist 和最小 pane grant；高风险审批仍回到原 pane 检查完整上下文。升级前导出配置并保存旧二进制，给 hook 与 MCP 做可逆安装清单。

## 参考资料

- [GitHub 仓库](https://github.com/Gaurav-Gosain/tuios)
- [GitHub REST API](https://api.github.com/repos/Gaurav-Gosain/tuios)
- [v0.8.1 Release](https://github.com/Gaurav-Gosain/tuios/releases/tag/v0.8.1)
- [Agent State 与 Inbox](https://github.com/Gaurav-Gosain/tuios/blob/main/docs/AGENT_STATE.md)
- [Architecture](https://github.com/Gaurav-Gosain/tuios/blob/main/docs/ARCHITECTURE.md)
- [Remote Sessions 与 Worktrees](https://github.com/Gaurav-Gosain/tuios/blob/main/docs/SESSIONS.md#agents-and-worktrees-on-another-machine)
- [Security Policy](https://github.com/Gaurav-Gosain/tuios/blob/main/SECURITY.md)
- [LICENSE](https://github.com/Gaurav-Gosain/tuios/blob/main/LICENSE)
