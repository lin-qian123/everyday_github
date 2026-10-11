<!-- markdownlint-disable MD013 -->

# AgentScope Java（agentscope-ai/agentscope-java）中文解读

> 上游仓库：<https://github.com/agentscope-ai/agentscope-java> · 归类：Agent 框架与技能生态 · 本页基于 2026-10-12 的中英文 README、v2 文档、Release、许可证与 GitHub REST API 静态整理；未接入模型、数据库、IM channel、sandbox backend 或分布式集群。

## 定位

AgentScope Java 2.0 是面向企业 Java 生态的长时程 Agent framework / harness，提供事件流、middleware、allow / approve / deny 权限、workspace、memory、skills、subagents、session recovery、分布式 persistence 与 Agent service control plane。

## 用法

上游要求 JDK 17+。Maven 项目引入 `agentscope-harness` 和所需 model provider extension，再用 `HarnessAgent.Builder` 配置 agent identity、workspace 与 model。每次请求构造带 `sessionId` / `userId` 的 `RuntimeContext`，用 `call()` 或 `streamEvents()` 执行；正式长任务再引入 AgentSession、外部 state store 与 sandbox backend。

## 原理

- ReAct core 通过 middleware 和 toolkit channel 扩展 memory、skill、subagent、plan 与上下文压缩。
- 32 类 typed events 表达模型、文本、tool、审批与状态变化，供前端和审计消费。
- RuntimeContext 把 session / user / agent / org 维度传递给 workspace、KV 与 sandbox state。
- state store 可落到 JSON、MySQL、Redis、PostgreSQL 等后端，以支持多 replica 恢复；workspace 可用 local、Docker、Kubernetes 或 cloud sandbox。

## 价值

- 为 Java 团队提供比单轮 agent loop 更完整的长任务、事件、权限和恢复抽象。
- provider extension、AG-UI / A2A、IM channel 与 service layer 便于接入现有企业应用。
- permission、HITL、sandbox 与 session recovery 是一等概念，适合建立显式运行约束。

## 风险边界

- allow / approve / deny 只约束接入该机制的 tool call；local subprocess、Docker、Kubernetes 与 cloud sandbox 的隔离、egress、secret 和逃逸面并不等价。
- 多租户 key 和 state namespace 是设计机制，不是已验证的 tenant isolation；必须做跨 org / session 越权和恢复一致性测试。
- memory、conversation、skill、trace 与外部 state store 会持久化敏感信息；自我沉淀 skill 还引入 prompt / supply-chain 污染风险。
- API latest Release 为 `v2.0.4`，README quickstart 仍示例 `2.0.3`；依赖、文档、extension 与 service 版本必须成套固定。

## 补充建议

- 先用 mock model / tools 和内存 state store 验证 event、approval、pause / resume，再逐步引入数据库和 sandbox。
- 为每个 tool 声明 actor、scope、side effect、idempotency、rollback 与 post-readback；外部系统继续保留自身授权层。
- 对 local / Docker / Kubernetes / cloud backend 分别执行恶意任务、egress、mount、credential 与 cross-tenant 测试，不用统一接口名称代替隔离证据。

## 参考资料

- GitHub 仓库：<https://github.com/agentscope-ai/agentscope-java>
- GitHub REST API：<https://api.github.com/repos/agentscope-ai/agentscope-java>
- `v2.0.4` Release：<https://github.com/agentscope-ai/agentscope-java/releases/tag/v2.0.4>
- v2 文档：<https://java.agentscope.io/v2/en/docs/index.html>
- Permission system：<https://java.agentscope.io/v2/en/docs/building-blocks/permission-system.html>
- Workspace / sandbox：<https://java.agentscope.io/v2/en/docs/harness/workspace.html>
- Production deployment：<https://java.agentscope.io/v2/en/docs/others/going-to-production.html>
- LICENSE：<https://github.com/agentscope-ai/agentscope-java/blob/main/LICENSE>
