# ditto

<!-- markdownlint-disable MD013 -->

## 定位

`ditto` 是一个本地 agent profile mining 工具。它读取 Claude Code、Codex、Copilot CLI 等本地会话日志，从真实工作记录中提取用户偏好、完成标准、写作风格和拒绝模式，生成 agent 可读取的 `you.md` 类个人工作画像。

截至 2026-07-13，GitHub API 显示该仓库约 132 stars、13 forks，创建于 2026-07-08，许可证为 MIT。它的核心观点是：真正有价值的“记忆”不只是用户显式写下的规则，而是历史会话里反复证明过的工作方式。

## 用法

README 将 ditto 描述为 zero-dependency Python 工具，默认面向本地日志。典型使用方式是让工具扫描本机 coding-agent 会话，生成分层 profile，再让 Claude Code、Codex、Cursor 或 Copilot 在任务前读取。

项目主题包括：

```text
agent-memory
agent-skills
claude-code
codex
context-engineering
local-first
personalization
```

## 原理

ditto 不要求用户手写规则，而是从历史 session 中抽取证据：用户如何定义 done、如何要求验证、如何评价 UI、如何拒绝糟糕方案、如何写作和沟通。它把这些模式整理成 agent 可复用上下文，并按工作、设计、写作等层次加载。

## 价值

- 解决长时间使用 coding agent 后“每次新会话仍像第一次见面”的问题。
- 比手写 `AGENTS.md` / `CLAUDE.md` 更能反映真实偏好，但也可与它们互补。
- 完全围绕本地日志运行，适合个人先试用。
- 对 agent personalization、team onboarding、style transfer 和 memory hygiene 都有参考价值。

## 风险边界

- 会话日志可能包含代码、密钥片段、客户信息和私人表达，必须先理解脱敏策略。
- 从历史行为提取偏好可能固化坏习惯，需要人工审查输出。
- 不同 agent 日志格式变化会影响覆盖率。
- profile 越强，越可能把个人偏好误当作项目规范；团队场景需要分层管理。

## 补充建议

- 适合作为个人 agent memory 的补充层，不应替代项目级 `AGENTS.md`。
- 对团队而言，应区分“个人工作风格”和“仓库强制规范”。
- 可与 `brain0` 分工：ditto 提取人的偏好，brain0 追踪 agent 改代码的意图和风险。

## 参考资料

- GitHub 仓库：<https://github.com/ohad6k/ditto>
- YouTube Shorts 示例：<https://www.youtube.com/shorts/SgMgDwYLe4c>
- Reddit 讨论入口：<https://www.reddit.com/r/claudeskills/comments/1ur1iq6/i_built_a_claude_skill_from_8_months_of_my_own/>
