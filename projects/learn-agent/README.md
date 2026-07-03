# learn-agent

- GitHub：<https://github.com/7-e1even/learn-agent>
- 抓取时间：2026-07-04（Asia/Shanghai）
- 今日信号：GitHub API 显示该仓库创建于 2026-07-03，抓取时约
  `51 stars / 5 forks`，主题包含 `agent-loop`、`coding-agent`、
  `claude-code`、`codex`、`cursor`、`opencode` 和 `tutorial`。

## 定位

`learn-agent` 是一个从零实现 coding agent 的渐进式教程仓库。它把
Claude Code、Codex、Cursor、opencode 这类 coding agent 背后的机制
拆成 15 课，每课配一份零依赖、单文件、可运行的 Node.js 示例。

它的定位不是提供可直接替代 Claude Code 的完整产品，而是把 agent
loop、工具系统、预算、上下文压缩、prompt cache、权限、provider
兼容、工具渐进披露等机制做成可学习、可调试的最小实现。

## 用法

README 给出的快速启动方式是：

```bash
git clone https://github.com/7-e1even/learn-agent
cd learn-agent
AGENT_API_KEY=sk-xxx node s01_agent_loop/agent.mjs
```

适合的阅读路径：

1. 从 `s01_agent_loop` 理解 agent 与 chatbot 的关键差异。
2. 顺序运行每个章节的单文件示例，观察失败模式和修复机制。
3. 在 `s12_full_agent` 查看多个机制合体后的端到端版本。
4. 对照作者提到的 Reina 完整实现，理解教程版与产品版的差异。

## 原理

项目把 coding agent 的可用性拆成一组工程机制：

- 主循环：模型提出行动，工具执行，结果回灌，直到任务完成或预算耗尽。
- 工具系统：用稳定契约封装读写文件、执行命令和编辑操作。
- 预算与熔断：限制循环次数、输出体积、连续错误和上下文窗口。
- 上下文管理：通过压缩、持久化和 prompt cache 降低遗忘和成本。
- 子代理与团队：把长任务拆成可监控、可并发的子任务。
- 权限和 provider 兼容：在副作用前审批，并把不同模型的 tool call 差异压平。

## 价值

- 对开发者：比只看 API 文档更接近真实 agent 失败模式，适合补 agent harness 的工程直觉。
- 对团队：可以作为内部培训材料，解释为什么 coding agent 需要预算、权限、验证和上下文策略。
- 对本仓库：补上“从 agent 原理到可跑最小代码”的学习型项目，
  与 `awesome-harness-engineering`、`loop-engineering` 形成互补。

## 风险边界

- 教程示例有意简化，不能直接承担生产代码修改、权限隔离或团队审计。
- 零依赖方便学习，但真实产品需要更完整的日志、沙箱、权限、并发、状态恢复和 secret 管理。
- 项目把经验来自 Reina 的说法写在 README 中；若用于选型，应同时检查 Reina 主仓的实际活跃度和许可证。

## 补充建议

- 新手可先跑 `s01`、`s03`、`s06`、`s13`，分别理解 loop、预算、压缩和权限。
- 对已有 coding agent 使用者，可把该项目当作“为何 agent 会空转、爆窗、忘任务、乱改文件”的机制解释材料。
- 后续观察它是否会补充 Python 版、MCP 示例或 CI 验收章节。

## 参考资料

- GitHub 仓库：<https://github.com/7-e1even/learn-agent>
- Reina：<https://github.com/Reina-Agent/Reina>
