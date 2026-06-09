# agno

## 项目定位
`agno` 是一个面向生产环境的 Agent 平台 SDK，主张把“做一个 agent demo”推进到“构建、运行、治理一整个平台级 agent 系统”。

- GitHub：https://github.com/agno-agi/agno
- 官方文档：https://docs.agno.com/
- 官方站点：https://agno.com/
- 适用人群：需要把 agent 作为产品能力、内部平台能力或多业务自动化基础设施的工程团队。

## 用法

`agno` 官方文档把工作流拆成 SDK + Runtime + Control Plane 三层，典型路径是：

1. 安装并按文档创建第一个 agent。
2. 在 SDK 层定义 agents、teams、workflows。
3. 通过 AgentOS/运行时把 agent 暴露为生产 API、MCP 服务或其他接口。
4. 再接入存储、权限、调度、观测、人工审批等生产能力。

从公开文档和 README 能看出，它不只是“本地运行一个 agent”：

- 可以把 agent 作为生产服务运行。
- 支持 tracing、scheduling、RBAC、human approval。
- 能接 Slack、Drive、MCP、自定义数据源等上下文提供方。
- 允许通过控制平面统一管理多 agent 系统。

## 原理

`agno` 的关键价值在于把 agent 系统拆成几个稳定层次，而不是把所有能力塞进一个 prompt loop：

- Framework 层：负责定义 agents、teams、workflows，以及 memory、knowledge、guardrails、tools。
- Runtime 层：把这些对象运行成可服务化的后端，支持 session、streaming、background jobs 等能力。
- Control Plane 层：提供监控、版本、权限、调度与运维入口。
- Interface 层：同一个 agent 可以暴露为 REST、SSE、MCP、Slack 等不同接口。

它解决的本质问题不是“怎么再写一个 agent”，而是“怎么把 agent 真正纳入软件系统和运维体系里”。

## 价值

- 对已经跨过 demo 阶段的团队，`agno` 的价值明显高于轻量 agent 框架，因为它直接把生产治理当一等公民。
- 100+ 工具集成、上下文提供方、JWT/RBAC、审计和调度，说明它瞄准的是平台层，而不是玩具级样例。
- 对内部 Copilot、数据 agent、文档处理、研究助手等场景，它提供了比较完整的基础设施骨架。

## 风险边界

- 平台型框架的学习和落地成本天然更高，不适合只想快速验证单个 prompt 的项目。
- 功能面很宽，初次接入如果同时开太多能力，容易把问题复杂化。
- 它强调自有数据、权限和运行时控制，这很好，但也意味着你需要真正承担平台运维责任。

## 补充建议

- 如果团队目前还停留在“单 agent + 单脚本”，先用它落一个最小生产链路：一个 agent、一个 API、一个审批点、一个观测面板。
- 真正值得评估的不是 demo 效果，而是它在权限、回放、调度、失败恢复和多租户隔离上的稳定性。
- 对长期要做 agent 产品的平台团队，`agno` 比只关注 prompt orchestration 的框架更有参考价值。

## 参考资料

- 仓库主页：https://github.com/agno-agi/agno
- 官方文档：https://docs.agno.com/
- Runtime / Agent API：https://docs.agno.com/features/api
- GitHub Trending：https://github.com/trending
