<!-- markdownlint-disable MD013 MD034 -->

# Strands Agents Harness SDK：Python / TypeScript 的进程内 Agent 运行库

> 上游仓库：https://github.com/strands-agents/harness-sdk · 归类：Agent 框架与技能生态 · 本页基于 2026-09-18 的 README、文档、package、release、NOTICE、LICENSE 与 REST API 静态整理；未运行模型或评测生产可靠性。

## 定位

Strands Agents 是一个进程内 SDK，而不是托管控制面。它提供 agent loop、tool、MCP、structured output、memory、session、multi-agent、guardrail、hook、tracing 与 eval primitives，让开发者在 Python 或 TypeScript 服务中组装自己的 harness。

2026-09-18 的 GitHub 官方 Python Trending 抓取显示约 `+46 stars today`；REST API 快照为 `7,328 stars / 1,151 forks / 764 open issues`，Apache-2.0。最新同日双 release 为 Python `v1.56.0` 与 TypeScript `v1.18.0`（9 月 15 日）。

## 用法

Python `>=3.10`，TypeScript 需要 Node.js `>=22`：

```sh
pip install strands-agents strands-agents-tools
npm install @strands-agents/sdk
```

```python
from strands import Agent
from strands_tools import calculator

agent = Agent(tools=[calculator])
agent("What is the square root of 1764?")
```

默认 provider 是 Amazon Bedrock；选择 Anthropic、OpenAI、Gemini、Ollama 或自定义 provider 时需要显式更改配置和凭据。

## 原理

- 模型收到 prompt、上下文和 tool schema，自主决定调用工具；SDK 负责循环、状态、限制、streaming 与停止原因。
- hook 可以在模型、tool 或 lifecycle 事件处记录、验证、取消或重定向；steering handler 支持运行中纠偏。
- memory / session 管理跨轮状态，multi-agent primitives 组合 graph、swarm 或 agents-as-tools。
- tracing、OpenTelemetry、eval 与 guardrail 为生产观测提供接口，但具体策略、数据留存和验证仍由应用实现。
- Python / TypeScript 共处 monorepo，版本分别发布；“同一 SDK”不表示两种语言的全部功能和行为始终同步。

## 价值

- 作为 library 嵌入现有 FastAPI、Express 或 Next.js 进程，避免为简单 Agent 先部署完整平台。
- provider、tool 与 memory 可替换，适合对比不同模型和运行环境。
- lifecycle budget、turn limit、cancellation、stop reason 和 hooks 比手写 while-loop 更容易形成可测 contract。
- 文档、示例、双语言 SDK 与 Apache-2.0 许可适合团队二次封装。

## 风险边界

- 默认 Bedrock 会把输入发往云端并依赖 AWS 凭据；更换 provider 只改变去向，不自动解决数据分类、保留、费用或地区合规。
- `strands-agents-tools` 中的 shell、文件、网络等工具会扩大执行权限；SDK 提供 guardrail 接口不等于默认安全策略完整。
- 模型驱动的 tool selection 仍会受到 prompt injection、错误参数、循环、非幂等操作和不可信 tool output 影响。
- tracing、memory 与 session 可能保存 prompt、工具输入、响应与业务数据，需独立定义脱敏、租户隔离、保留和删除。
- Python / TypeScript release 节奏与默认行为可能不同，跨语言复制示例需对照对应版本文档。
- 本页未执行 `v1.56.0` / `v1.18.0`，没有验证延迟、成本、guardrail 召回、provider parity 或故障恢复。

## 补充建议

1. 从只读 calculator / fixture tools 建立确定性测试，再逐项加入文件、网络与外部写入；默认拒绝未注册工具。
2. 为每个任务设置 turn、token、wall-clock 与费用上限，记录 stop reason，并对超限、取消和 provider 失败做回归。
3. 对 prompt injection、恶意 tool output、重放与重复写入建立 eval；高影响动作使用 preview、approval 和 post-readback。
4. 分别锁定 Python 与 TypeScript 版本，用同一任务集比较结果和 trace，不假设跨 SDK 行为一致。

## 参考资料

- 上游 README：https://github.com/strands-agents/harness-sdk
- 官方文档：https://strandsagents.com/
- Python `v1.56.0` release：https://github.com/strands-agents/harness-sdk/releases/tag/python%2Fv1.56.0
- TypeScript `v1.18.0` release：https://github.com/strands-agents/harness-sdk/releases/tag/typescript%2Fv1.18.0
- GitHub REST API：https://api.github.com/repos/strands-agents/harness-sdk
- LICENSE：https://github.com/strands-agents/harness-sdk/blob/main/LICENSE.APACHE
