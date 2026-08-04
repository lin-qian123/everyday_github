# diri

- 仓库：[cristicretu/diri](https://github.com/cristicretu/diri)
- 快照：2026-08-05 抓取；GitHub API 显示其创建于 2026-08-04，约 81 stars、2 forks，Apache-2.0。数字会随时间变化。
- 分类：Coding Agents 与终端助手

## 定位

macOS 原生 coding-agent 编排器，可在 Git worktree 或远端主机并行运行 Claude Code、Codex、Cursor、Gemini 与普通 shell，并展示会话状态、持久输出和菜单栏汇总。

## 用法

README 要求 Swift、Rust 与 Xcode 命令行工具：先运行 `swift build`、`swift test`，再在 `diri/` 构建应用；本地安装前阅读打包、远端节点和性能文档。首次只为无敏感数据的仓库创建 worktree 与本地 session。

## 原理

Rust/GPUI 桌面端负责 UI；Swift daemon 管理 PTY、子进程、日志、worktree 和控制 socket，额外 helper 持有 PTY 以便 daemon 重启后恢复。状态识别由数据化 manifest 与 reducer 驱动，MCP shim 可把编排能力暴露给 agent。

## 价值

把并发 agent 的状态、终端持久性和 worktree 隔离放入同一 macOS 工作台，尤其适合需要人工及时处理“needs-you”状态的开发流程。远端 host 支持也有助于把本地 UI 与计算环境分开。

## 风险边界

并行 agent 会竞争 Git、端口、凭据与工作树资源；持久 PTY 日志可能含代码、命令和 token。MCP 的“spawn/orchestrate”能力不应默认获得生产主机权限；Cursor/Gemini 在 README 中仅为部分支持。

## 补充建议

为每个 agent 分配独立 worktree、分支和最小凭据，禁止多个会话直接写同一目录。远端连接使用受限 SSH key、审计日志和资源配额；将 status 识别当作辅助信号，而非完成验收。

## 参考资料

- [项目 README](https://github.com/cristicretu/diri)
- [打包说明](https://github.com/cristicretu/diri/blob/main/diri/PACKAGING.md)
- [GitHub API 元数据快照](https://api.github.com/repos/cristicretu/diri)
