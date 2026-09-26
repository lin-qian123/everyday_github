<!-- markdownlint-disable MD013 -->

# OpenRig（mvschwarz/openrig）

> 上游仓库：<https://github.com/mvschwarz/openrig> · 归类：Agent 框架与技能生态 · 本页基于 2026-09-26 的 GitHub API、README、Security Policy、Release 与 manifest 静态整理，未安装 CLI、启动 daemon 或运行真实 Agent。

- 抓取快照：454 stars、59 forks、31 open issues。
- 热度信号：GitHub TypeScript Trending 抓取时约 +80 当日 stars。
- 版本与许可：Apache-2.0；latest Release、tag 与根 manifest 均为 `v0.5.15` / `0.5.15`。

## 定位

OpenRig 是管理 Claude Code、Codex、Pi 等 coding-agent harness 的本地多 Agent 控制层。它不替代模型或 coding agent，而是用声明式 RigSpec、稳定 seat 地址、队列、消息、快照恢复和 TUI，把分散的 tmux 会话组织成可持续运行的团队。

## 用法

运行环境需要 Node.js 20 / 22 / 24 与 tmux。上游建议先安装 `@openrig/cli`，执行 `rig setup --dry-run` 审查计划，再用 `rig up first-project --cwd . --plan` 查看拓扑、确认登录和权限后启动；`rig ps`、`rig send`、`rig queue` 与 `rig tui` 分别用于检查 seat、派发任务、追踪队列和观察状态。首次使用应放在可丢弃仓库和专用系统用户下，不直接对高价值主工作区启用。

## 原理

系统由 CLI / TUI / MCP、Hono HTTP daemon、领域服务、SQLite、tmux 与各 runtime adapter 组成。RigSpec 定义 pod、seat、连接和 continuity policy；daemon 负责持久状态、消息与资源投影，tmux 承载真实 Agent 终端。快照保存拓扑和恢复线索，但每个 Agent 仍有独立上下文，恢复结果也可能是 resumed、fresh 或 failed。

## 价值

OpenRig 把“启动多个终端”提升为可寻址、可观察、可恢复的 Agent 团队运行面，适合需要 Claude Code 与 Codex 混合、长期保留角色、显式交接和独立复核的工程工作。README 对机器写入、权限模式和恢复边界写得比多数 harness 更具体，也提供 Release、Security Policy 与升级流程。

## 风险边界

- `rig setup --dry-run` 只预览 setup 阶段，不覆盖 daemon 后续自动写入；启动会修改 `~/.tmux.conf`、Claude / Codex 配置、workspace trust、hooks、skills 与实例数据库。
- 默认 Codex 使用 workspace-write，Claude 使用 `acceptEdits`；显式 YOLO / full-bypass 会提升到危险权限。OpenRig 是控制面，不是 OS sandbox，也不缩小 provider、MCP、shell、网络或 secret 权限。
- daemon、hook 和 context collector 会记录 seat / session、transcript path、token / quota 等元数据；provider 与选定 MCP 还有各自数据流。
- managed writer 可能替换特定配置键，部分损坏配置会按空对象恢复；README 明确这不是完整保留或回滚保证，首次使用前必须备份。
- 上游示例、软件工厂叙事和恢复能力未在本轮运行；最新 npm 版本才受支持，`main` 上修复不等于已发布包含修复。

## 补充建议

先创建专用用户和无 secret 的副本仓库，只启用两个 seat，固定 `v0.5.15`，逐项 diff `~/.claude`、`~/.codex`、`~/.tmux.conf` 与 workspace 文件。分别测试权限拒绝、daemon 崩溃、重启恢复、消息错投、配置回滚和恶意仓库 prompt injection；用外部测试结果而非 TUI 状态判断任务完成。

## 参考资料

- [GitHub 仓库](https://github.com/mvschwarz/openrig)
- [GitHub REST API](https://api.github.com/repos/mvschwarz/openrig)
- [v0.5.15 Release](https://github.com/mvschwarz/openrig/releases/tag/v0.5.15)
- [Getting Started](https://github.com/mvschwarz/openrig/blob/main/docs/reference/getting-started.md)
- [Security Policy](https://github.com/mvschwarz/openrig/blob/main/SECURITY.md)
- [LICENSE](https://github.com/mvschwarz/openrig/blob/main/LICENSE)
- [官方 YouTube 频道](https://www.youtube.com/@openrig)
