<!-- markdownlint-disable MD013 MD034 -->

# composio

`ComposioHQ/composio` 是一个面向 AI agents 的工具接入、认证和执行网关。它提供 TypeScript / Python SDK、CLI、provider adapters、toolkits、per-user sessions、triggers 和 sandbox，目标是让 agent 能在受控认证边界内调用大量外部应用。

- GitHub：https://github.com/ComposioHQ/composio
- 文档：https://docs.composio.dev
- 官网：https://composio.dev
- 分类：Agent 框架与技能生态
- 许可证：MIT

## 热度信号

- 2026-07-15 通过 GitHub API 抓取时约 `29.2k stars`、`4.7k forks`。
- 仓库在 2026-07-14 仍有 push，topics 覆盖 `agents`、`mcp`、`function-calling`、`llmops`。
- README 强调 `1000+` pre-authenticated toolkits、per-user sessions、authentication、triggers 和 sandbox。

## 定位

Composio 解决的是 agent 落地中最麻烦的一层：工具调用不仅要有 schema，还要有认证、授权、用户隔离、会话、执行日志和 provider 适配。

它适合：

- 让 OpenAI Agents、Claude Agent SDK、Vercel AI SDK、LangChain 等框架调用 SaaS 工具。
- 为每个用户创建独立 session，避免所有 agent 共用一把全局密钥。
- 在产品中把“用户意图”转成真实外部操作，如邮件、日历、CRM、工单等。

## 用法

TypeScript 示例依赖：

```bash
npm install @composio/core @composio/openai-agents @openai/agents
```

Python 示例依赖：

```bash
pip install composio composio-openai-agents openai-agents
```

典型流程是：创建 `Composio` client，按用户创建 session，取出该 session 可用工具，再交给 agent runtime。

## 原理

Composio 的抽象可以拆成五层：

- toolkit catalog：维护可调用的外部应用能力。
- auth/session：把工具授权绑定到具体用户或会话。
- provider adapters：适配 OpenAI Agents、Claude、Vercel AI SDK、LangChain 等调用格式。
- CLI / SDK：让开发者搜索、执行和脚本化工具。
- sandbox/workbench：降低 agent 执行外部动作时的失控风险。

## 价值

- 把 agent tool calling 从 demo 拉向产品级认证边界。
- 降低多 provider agent 框架之间的重复适配成本。
- 对 SaaS agent 产品尤其关键，因为用户授权和审计是上线门槛。
- MCP 与 OpenAPI / SDK 并行支持，能覆盖不同 agent 客户端。

## 风险边界

- 工具越多，权限面越大；需要明确哪些 action 可读、可写、可删除。
- 认证代理层本身成为高价值基础设施，密钥管理和审计不可省略。
- 第三方 SaaS API 变更会影响 agent 稳定性。
- agent 自动执行外部动作时，必须设置 human-in-the-loop 或幂等回滚策略。

## 补充建议

- 从只读工具开始接入，再逐步开放写操作。
- 为高风险动作设置审批、预算和速率限制。
- 对每个 provider adapter 做端到端测试，而不是只验证工具列表可见。
- 与 `open-connector`、`agent-toolkit-for-aws`、`awesome-mcp-servers` 一起比较，区分“连接器目录”“认证网关”和“官方工具包”。

## 参考资料

- GitHub 仓库：https://github.com/ComposioHQ/composio
- 文档：https://docs.composio.dev
- Quickstart：https://docs.composio.dev/docs/quickstart
- Changelog：https://docs.composio.dev/reference/changelog
