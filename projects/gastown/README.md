<!-- markdownlint-disable MD013 -->

# gastown

## 定位

`gastown` 是一个多 agent workspace manager，用来协调 Claude Code、GitHub Copilot、Codex、Gemini 等 AI coding agents 在多个项目、任务和 worktree 中并行工作。

它比普通终端多路复用器更偏“工作流编排层”：强调持久 work state、git-backed hooks、mailbox、handoff、agent 身份、任务 ledger、队列合并和恢复机制。

## 用法

项目建议用户从 “Mayor” 这个主协调 agent 开始，把目标交给它，再由 Gas Town 管理 town、rig、crew member、polecat、hooks、convoy、beads 等工作单元。

本地部署需要 Git、Go、Beads、sqlite3、tmux、Claude Code CLI 等依赖；也提供 Docker 方式减少宿主依赖。核心使用方式是把一个或多个 git 仓库接入 Gas Town，再让不同 worker agents 按任务执行、汇报、交接和合并。

## 原理

Gas Town 的关键结构包括：

- **Town**：总 workspace。
- **Rig**：单个项目或仓库容器。
- **Crew Member**：人工或主工作区。
- **Polecat**：带持久身份的 worker agent。
- **Hooks**：基于 git worktree 的持久状态存储。
- **Beads / Convoys**：结构化任务和任务组。
- **Witness / Deacon / Dogs**：监控、巡检和维护层。
- **Refinery**：类似 Bors 的合并队列与验证门禁。

它试图解决的不是“怎么让一个 agent 写代码”，而是“4 到 30 个 agent 并行工作时，如何保留上下文、分派任务、处理卡住、合并结果并留下审计痕迹”。

## 价值

- **团队级多 agent 协调**：适合研究多人类/多 agent 软件工程流程。
- **持久状态**：把 agent 记忆和任务状态从易丢失的会话迁移到 git-backed ledger。
- **恢复能力**：强调 session discovery、predecessor query 和 crash/restart 后接续。
- **合并治理**：把 agent 完成任务后的验证、排队、失败隔离和重派做成一等概念。

## 风险边界

- 术语和系统复杂度很高，新用户学习成本明显高于 `tmux`、`herdr` 或单一 coding agent。
- 多 agent 自动合并会放大错误传播，需要强制测试、代码审查和权限隔离。
- 项目依赖链较长，Go、Dolt / Beads、tmux、Claude Code 等版本差异会影响体验。
- 目前更适合高级用户和实验团队，不应直接替代成熟 CI/CD 与人工 code ownership 流程。

## 补充建议

- 小团队先用一个非关键仓库试验 task ledger、handoff 和 merge queue，再考虑扩大到生产仓库。
- 与 `herdr` 区分：`herdr` 偏终端会话与状态视图，`gastown` 偏任务、身份、持久工作状态和合并治理。
- 与 `codex-plugin-cc` 结合看，可以看到跨 agent 调用和多 agent workspace 正在向同一个工程问题收敛。

## 参考资料

- GitHub 仓库：<https://github.com/gastownhall/gastown>
- Beads：<https://github.com/sst/opencode/tree/main/packages/beads>
- GitHub Trending：<https://github.com/trending>
