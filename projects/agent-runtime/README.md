# agent-runtime

- GitHub：<https://github.com/easylink-ai-open/agent-runtime>
- 抓取时间：2026-07-05（Asia/Shanghai）
- 今日信号：GitHub API 显示该仓库创建于 2026-07-01，抓取时约
  `112 stars / 17 forks`，README 定位为 provider-neutral 的独立 agent runtime core。

## 定位

`agent-runtime` 是一个独立的 Python agent 运行时内核。它把 agent loop、
中立消息类型、LLM provider 客户端、工具调度、prompt/cache primitives、
collaboration mode、hooks、budget 和上下文辅助函数抽成产品无关组件。

它关注的不是终端 UI 或完整应用，而是把“可复用的 agent 执行内核”从具体产品包、
数据库、Web 服务和品牌策略中拆出来。

## 用法

README 给出的最小使用方式是：

```python
from agent_runtime import Agent, LLMConfig

agent = Agent(
    llm_config=LLMConfig(
        api="openai-chat-completions",
        model="gpt-4.1-mini",
        api_key="...",
        base_url="https://api.openai.com/v1",
    )
)
result = agent.ask("hi")
print(result.content)
```

产品层可以注入自己的 tools、prompt provider、cache strategy、sandbox、
memory、session 和持久化机制。

## 原理

项目把 runtime 边界设计成 provider-neutral：

- `Message`、`TextPart`、`ImagePart`、`ToolCallPart`、`ToolResultPart`
  表示中立对话结构。
- `LLMRequest`、`LLMResponse`、`LLMStreamEvent` 归一化模型调用与返回。
- 内置 OpenAI / Anthropic wire converters，把中立结构映射到具体 provider。
- `ModelClient`、`ToolDispatcher`、`SystemPromptProvider`、`CacheStrategy`
  等协议用于替换产品侧实现。

这使得 agent loop 可以复用，而 memory、sessions、sandboxing、channels、
durable storage 等产品能力留在外层组合。

## 价值

- 对 agent 产品开发者：提供一个可拆出的 runtime 思路，避免把 loop 写死在某个应用里。
- 对多 provider 应用：中立类型减少 OpenAI / Anthropic wire shape 的耦合。
- 对测试：可以注入 fake model client 和工具 dispatcher，更容易验证 loop 行为。

## 风险边界

- 它是早期新仓库，生态、文档、版本兼容和生产案例仍有限。
- runtime 本身不解决 sandbox 安全、权限隔离、持久化、队列和多用户问题。
- provider-neutral 抽象可能掩盖具体模型特性，例如 cache、tool call 细节和 streaming 差异。
- 如果产品已有成熟框架，迁移成本可能高于收益。

## 补充建议

- 与 `autogen`、`crewAI`、`flue`、`learn-agent` 对照：本项目更偏底层 runtime，
  不强调多 agent 编排或教学。
- 适合作为自研 agent 产品的内核参考，但生产落地仍需补权限、审计、持久化和任务恢复。
- 后续关注其是否提供稳定 API、测试矩阵和实际产品集成案例。

## 参考资料

- GitHub 仓库：<https://github.com/easylink-ai-open/agent-runtime>
- README：<https://github.com/easylink-ai-open/agent-runtime#readme>
