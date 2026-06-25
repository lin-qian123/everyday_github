# orca（stablyai/orca）

- GitHub: https://github.com/stablyai/orca
- 官网: https://onOrca.dev
- 记录日期: 2026-06-25 (Asia/Shanghai)

## 定位

`orca` 是一个面向多代理并行开发的桌面工作台。它的核心不是替代 Codex、Claude Code、OpenCode 或 Pi，而是把这些 agent 放进各自隔离的 git worktree 中并行运行，再用一个统一界面跟踪、比较和接管结果。

## 用法

### 1) 直接安装桌面客户端

官方 README 提供桌面下载入口，并支持 macOS、Windows、Linux。

### 2) 用 worktree 方式并行跑多个 agent

根据 README 的主打路径，可以把同一任务扇出给多个 agent，每个 agent 占一个独立 worktree：

1. 在同一仓库中创建多个隔离工作目录。
2. 让不同 agent 在各自 worktree 中执行同一任务或不同子任务。
3. 在 `orca` 的统一界面里比较结果，再合并表现更好的分支。

### 3) 用移动端跟进长任务

项目同时提供移动端 companion，用于在桌面外查看 agent 状态、接收完成通知并补发 follow-up。

## 原理

1. `orca` 把“agent 执行”与“代码隔离”绑在一起，核心隔离单元不是会话，而是 git worktree。
2. 它把多个终端、多个 agent、多个仓库上下文聚合到一个 ADE（agent development environment）里，降低并行实验的切换成本。
3. README 里强调 terminal splits、design mode、mobile companion，说明它想做的不只是调度层，而是完整的人机协作工作台。

## 价值

- 对频繁做对比实验、并行试错和多分支验证的开发者来说，它比单会话 CLI 更接近真实生产流程。
- 它把“多 agent”从抽象概念落成了具体的文件隔离、终端隔离和结果比对机制。
- 如果团队已经接受 worktree 工作流，`orca` 这类产品能明显减少“开一堆窗口 + 手动比结果”的摩擦。

## 风险边界

- 它的价值依赖你是否真的会长期使用多 worktree / 多 agent；对单线程开发者来说，学习和界面复杂度可能偏高。
- 多 worktree 会把 Git 操作、依赖管理和磁盘使用复杂度一起放大，团队需要更清晰的分支与合并纪律。
- 官方强调支持多种 agent，但不同 agent 在权限、补丁策略和停止条件上的行为差异，仍需要你自己验证。

## 补充建议

1. 优先拿“同一需求让两个 agent 并行改同一仓库”的小实验验证它，而不是一开始全量迁移日常开发。
2. 如果你团队已经在用 Codex / Claude Code / OpenCode，重点评估它对 worktree 生命周期、差异比较和回收清理是否真正省事。
3. 把它和纯 dashboard 型工具区分开看：它更像 agent IDE / ADE，而不是只做观察面板。

## 参考资料

- https://github.com/stablyai/orca
- https://onOrca.dev
- https://www.onorca.dev/docs/model/worktrees
- https://github.com/trending
- https://github.com/trending/typescript
