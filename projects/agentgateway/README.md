<!-- markdownlint-disable MD013 -->

# Agentgateway（agentgateway/agentgateway）

> 上游仓库：<https://github.com/agentgateway/agentgateway> · 归类：Agent 框架与技能生态 · 本页基于 2026-10-03 的 GitHub API、README、standalone / Kubernetes 文档、security policy、Release 与 LICENSE 静态整理，未部署 proxy、接入 provider / MCP / A2A、运行 guardrail 或验证多租户隔离。

- 抓取快照：5,144 stars、908 forks、308 open issues。
- 热度信号：GitHub Rust Trending 抓取时约 +17 当日 stars。
- 版本与许可：Apache-2.0；latest Release / tag 为 `v1.6.0`，项目由 Linux Foundation 托管并处于 active development。

## 定位

Agentgateway 是面向 Agent-to-LLM、Agent-to-tool 与 Agent-to-agent 流量的 AI-native proxy / gateway，原生覆盖 MCP 与 A2A，也提供 OpenAI-compatible LLM routing。它把认证、RBAC、rate limit、budget、guardrail、failover、observability 和 Kubernetes inference routing 放到独立基础设施层。

## 用法

可按 standalone quickstart 用 YAML 配置运行单体 gateway，也可在 Kubernetes 中部署 controller 并使用 Gateway API。LLM 路径配置 OpenAI、Anthropic、Gemini、Bedrock 等 provider；MCP 路径联邦 stdio / HTTP / SSE / Streamable HTTP server，并可从 OpenAPI 生成工具；A2A 路径提供 capability discovery 与任务协作。内置 UI 用于浏览连接与路由状态。

## 原理

数据面用 Rust proxy 解析 LLM、MCP、A2A 与普通 HTTP 连接，按身份、CEL policy、rate / spend、load-balance 和 failover 决策路由；Kubernetes controller 下发 Gateway API / inference 配置，并可基于 GPU、KV cache、LoRA adapter 与 queue depth 选择 self-hosted model。OpenTelemetry 记录 metrics / logs / traces，guardrail 可调用 regex、OpenAI moderation、Bedrock Guardrails、Google Model Armor 或自定义 webhook。

## 价值

将 provider key、工具联邦、policy 和 telemetry 从每个 Agent framework 抽离，可减少重复集成并统一成本 / 访问治理；standalone 与 Kubernetes 两条路径允许从单机验证扩展到集群。MCP、A2A、LLM 三类流量在同一控制面，也便于分析一次 Agent 调用的端到端网络边界。

## 风险边界

- gateway 集中模型 prompt、tool payload、身份、密钥和 trace，成为高价值故障与攻击面；部署成功不等于租户隔离、secret 管理或日志脱敏正确。
- guardrail 是可配置过滤层，上游 security policy 明确“未按用户预期生效”通常视为配置 / 产品限制；不能把 guardrail 当作事实、合规或 prompt-injection 保证。
- CEL、ext-auth、ext-proc 与外部 rate-limit service 属于用户或受信组件；错误 policy、恶意扩展和暴露 admin interface 不会由 gateway 自动修复。
- OpenAI-compatible translation、failover 和 provider routing 可能改变 tool、stream、error、usage 与模型语义；协议可通不等于结果等价。
- MCP federation 扩大工具发现与授权面；A2A capability discovery 也可能跨 agent / tenant 暴露元数据或诱导任务委派。
- 作者功能列表与 active-development 状态不是 performance、安全或生产 SLA；本轮未跑吞吐、failure injection 或 cross-namespace authorization 测试。

## 补充建议

固定 `v1.6.0`，在非生产 namespace 以单 provider、单只读 MCP tool 和合成 prompt 起步；区分 data / control / admin plane，给每条路由显式 identity、tenant、egress、budget、日志字段与 fail-closed 规则。用协议 contract、跨租户、恶意 MCP description、prompt injection、provider timeout / fallback、guardrail bypass 与 telemetry redaction fixture 做回归，再逐项引入 A2A 和写工具。

## 参考资料

- [GitHub 仓库](https://github.com/agentgateway/agentgateway)
- [GitHub REST API](https://api.github.com/repos/agentgateway/agentgateway)
- [README 与功能概览](https://github.com/agentgateway/agentgateway/blob/main/README.md)
- [Standalone Quickstart](https://agentgateway.dev/docs/standalone/latest/documentation/quickstart)
- [Kubernetes Quickstart](https://agentgateway.dev/docs/kubernetes/latest/documentation/quickstart)
- [Security policy](https://github.com/agentgateway/agentgateway/blob/main/SECURITY.md)
- [v1.6.0 Release](https://github.com/agentgateway/agentgateway/releases/tag/v1.6.0)
- [LICENSE](https://github.com/agentgateway/agentgateway/blob/main/LICENSE)
