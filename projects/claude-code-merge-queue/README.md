# claude-code-merge-queue

<!-- markdownlint-disable MD013 MD012 -->

## 定位

`claude-code-merge-queue` 是一个本地、零云成本的 Claude Code 并行 agent 合并队列。它不负责创建 worktree，而是接在 Claude Code 原生 worktree 隔离之后，解决多个 agent 同时 landing、rebase、push、build、test 时的冲突和资源争用。

它属于 agent 工程治理工具，目标是让多个并行 coding agents 可以更安全地落到同一集成分支。

## 用法

典型安装流程：

```bash
npm install --save-dev claude-code-merge-queue
npx claude-code-merge-queue init
```

初始化会写入或合并：

- `claude-code-merge-queue.config.mjs`
- `CLAUDE.md`
- `.claude/settings.json` 的 `WorktreeCreate` hook
- 可选 Husky pre-push hook
- `package.json` 中的 `land`、`sync`、`promote`、`preview` 等脚本

之后 agent 在各自 worktree 中完成检查并调用 `land`，队列串行化 rebase / push / check；人类在需要发布时手动执行 `promote`。

## 原理

项目把并行开发中的共享资源变成队列化操作：

- lane：每个 worktree 对应一个有编号的并行开发通道。
- build lock：对昂贵构建或共享测试资源做机器级串行化。
- land：通过 FIFO 队列把 rebase、检查和 push 串起来。
- sync：让主 checkout 跟上集成分支，并处理依赖变化。
- promote：人类手动把集成分支推向生产。
- pre-push hook：阻止绕过队列直接推送。

这类工具的核心不是“让 agent 更聪明”，而是让 agent 不能轻易制造竞态条件。

## 价值

- 对多 agent 开发：把并行 worktree 的最后一公里合并问题具体化。
- 对本地团队：不依赖 GitHub Enterprise Merge Queue，也不消耗 CI minutes。
- 对测试稳定性：减少共享数据库、端口、构建缓存带来的假性 flaky。
- 对 agent 规训：把“请按流程操作”变成 hook 和队列，而不是自然语言约定。

## 风险边界

- 目前主要面向 Claude Code 工作流，其他 coding agent 需要额外适配。
- 本地队列无法替代远端 CI、代码审查和权限控制。
- 如果 `checkCommand` 配置不足，队列只能保证串行，不能保证质量。
- 自动写入 `CLAUDE.md`、hooks 和 package scripts 前应先看 diff，避免覆盖团队规则。

## 补充建议

- 适合已经使用多个 Claude Code worktree 的项目先试点。
- 把 `checkCommand` 设为真实发布前门槛，而不是只跑轻量 lint。
- 对共享数据库测试，优先使用项目提供的 ephemeral 扩展点隔离资源。
- 可与 `herdr`、`gastown`、`orca` 做组合：前者管会话和任务，merge queue 管落地顺序。

## 参考资料

- GitHub 仓库：<https://github.com/funador/claude-code-merge-queue>
- Claude Code：<https://github.com/anthropics/claude-code>
