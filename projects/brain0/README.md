# brain0

<!-- markdownlint-disable MD013 -->

## 定位

`brain0` 自称是 “The black box for AI-written code”。它面向 AI coding agent 生成代码后的可追溯性：把 commit、agent prompt、agent 读取过的上下文、风险评分、DLP audit 和 provenance attestation 连接成被动 decision graph。

截至 2026-07-12，GitHub API 显示该仓库约 342 stars、12 forks，创建于 2026-07-02，许可证为 Apache-2.0。虽然星数低于今日其他项目，但主题与 HalluSquatting、agent 供应链和 AI 代码审计风险高度相关。

## 用法

快速启动：

```bash
npx brain0 up
```

README 描述该命令会从 git remote 推断 repo id，索引 git 历史，自动发现 Codex 和 Claude Code 会话，将事实与意图关联，并在 `http://localhost:8787` 打开图形界面。

常用命令包括：

```bash
brain0 today
brain0 report
```

## 原理

brain0 不要求 agent 主动配合，而是读取 git 历史和 agent 已写到磁盘的 transcript。它尝试将代码 diff、文件 / symbol 级变化和 prompt 意图连起来，形成可浏览的决策图，并标注 agent 读取过哪些内容、哪些变更风险更高。

## 价值

- 解决 AI 代码审查中的关键缺口：仅看 diff 很难知道 agent 为什么这样改。
- 适合多 agent、并行 worktree、长任务自动化场景的事后审计。
- 与 `agent-chief`、`mcpsnoop`、`SkillSpector` 一起构成 agent observability / security 方向。
- 本地优先、Apache-2.0，适合先在内部仓库验证。

## 风险边界

- 仍是早期项目，自动关联 prompt 与 commit 可能误判或漏判。
- 它能帮助审计，不等于自动证明代码正确或安全。
- 读取 agent transcript 可能包含敏感 prompt、路径、密钥片段或客户数据，落地前必须做脱敏策略。
- 对未落盘会话、远程云端 agent 或被清理的历史，覆盖会有限。

## 补充建议

- 优先用于 AI 自动化强、审计压力高的仓库，而不是普通小项目。
- 与 `mcpsnoop` 分工：mcpsnoop 看工具调用流，brain0 看代码变更背后的意图和 provenance。
- 建议和 CI、代码所有权、敏感文件规则一起使用，而不是单独依赖风险分。

## 参考资料

- GitHub 仓库：<https://github.com/Brain0-ai/brain0>
- npm 包：<https://www.npmjs.com/package/brain0>
- HalluSquatting 风险背景：<https://www.tomshardware.com/tech-industry/cyber-security/hallusquatting-is-the-latest-agentic-ai-exploit-where-models-dream-up-potentially-malicious-urls-in-tool-calls-attack-exploits-a-fundamental-weakness-in-every-available-model>
