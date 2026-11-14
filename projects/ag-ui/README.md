<!-- markdownlint-disable MD013 -->

# AG-UI

- 上游：[ag-ui-protocol/ag-ui](https://github.com/ag-ui-protocol/ag-ui)
- 分类：前端、UI 与 Agent 交互层。
- 核验：2026-11-15（Asia/Shanghai）；仓库 ID `979392131`，固定主线 `f77065ad109c40e60ecbdec9d8fa6fa09987c41e`；协议 `1.0`，`@ag-ui/core` 主线 / npm 均为 `1.0.4`。
- 证据范围：官方 API、发行、固定 SHA README / 1.0 规范 / 清单与 npm 元数据的静态核读；未创建应用、调用模型、部署或做浏览器交互测试。

## 定位

AG-UI 将 Agent 和用户应用之间的交互表示为有序的类型化事件流，覆盖消息、工具调用、状态、进度和人工中断。它服务于 Agent 与前端的连接；MCP 工具接入、A2A Agent 间通信以及 A2UI 界面描述是不同层，可组合但不能互相替代。[README](https://github.com/ag-ui-protocol/ag-ui/blob/f77065ad109c40e60ecbdec9d8fa6fa09987c41e/README.md)

它是开放协议、SDK 与框架桥接集合，不是一个统一版本的全能前端，也不自动提供业务账户权限或长期任务可靠性。

## 用法

上游给出的创建入口为：

```bash
npx create-ag-ui-app@latest
npm run dev
```

创建后先进入生成的应用目录再启动。这是移动的脚手架入口，须按所选客户端 / 服务端模板补齐依赖和模型配置，不能把本页静态核读当作启动成功。正式复现时记录实际解析的脚手架版本、lockfile、前端 SDK 与后端 integration 版本。[应用入门](https://github.com/ag-ui-protocol/ag-ui/blob/f77065ad109c40e60ecbdec9d8fa6fa09987c41e/docs/quickstart/applications.mdx)

版本按包分别固定：`@ag-ui/core@1.0.4` 与 `@ag-ui/langgraph@0.0.46` 的版本号不同，不应统称为“AG-UI 1.0.4 的所有集成”。11-13 发行要求后者的 client 等 peer dependencies `>=1.0.0`，并修复 LangGraph interrupt schema、ToolMessage 与 run version 声明。[发行](https://github.com/ag-ui-protocol/ag-ui/releases/tag/release%2F2026-11-13)、[core npm](https://registry.npmjs.org/@ag-ui%2Fcore/latest)、[LangGraph npm](https://registry.npmjs.org/@ag-ui%2Flanggraph/latest)

## 原理

1. 客户端发送 `RunAgentInput`，包含 thread / run、消息、工具和状态；端点通过桥接把框架事件转为协议事件。一次 run 由 `RUN_STARTED` 与结束事件界定。
2. 客户端按兼容翻译、中间件、schema enforcement 和验证等步骤处理流；中间件在 enforcement 前执行，方便迁移旧形状。协议语义与具体 transport binding 分开。[架构](https://github.com/ag-ui-protocol/ag-ui/blob/f77065ad109c40e60ecbdec9d8fa6fa09987c41e/docs/spec/1.0/architecture.mdx)
3. 状态通过 snapshot 与 JSON Patch delta 更新，并在后续 run 输入中往返；它是应用接收的远端输入。[状态规范](https://github.com/ag-ui-protocol/ag-ui/blob/f77065ad109c40e60ecbdec9d8fa6fa09987c41e/docs/spec/1.0/events/state.mdx)
4. 人工中断以 interrupt outcome 结束当前 run，恢复时携带每个 interrupt 的回答或明确 abandoned 记录；客户端必须检查完整覆盖，过期回答按其判断拒绝，遗漏不能自动当成同意或放弃。[中断 / 恢复](https://github.com/ag-ui-protocol/ag-ui/blob/f77065ad109c40e60ecbdec9d8fa6fa09987c41e/docs/spec/1.0/basic/patterns/interrupt-resume.mdx)

## 价值

对需要换 Agent 框架、保留现有 UI 或展示长任务状态的团队，可减少重复定义消息与工具事件格式。将交互记录为 run input 与事件，也有助于重放“界面当时看见了什么”和排查恢复问题。

这是协议设计价值；框架桥接的完整度、真实动作的幂等和恢复、UI 可用性仍要用具体应用测试。README 保留“约 16 种事件”的概括，本页以冻结的 1.0 规范为准，不把旧概括作为当前 schema 数量。

## 风险边界

- **界面批准与动作授权分开。** 应用负责用户身份、数据范围、工具执行和哪些动作需要同意；协议事件本身不能替代服务端授权。规范允许 producer 不保留前次中断状态，因此消费端覆盖检查也不应被当成独立防伪机制。
- **状态不是可信配置。** 1.0 规范明确要求应用在渲染、执行或据此授予权限前验证 state，且 producer 不应放入秘密，因为状态会在客户端和 Agent 之间往返。
- **兼容不保证无损。** 有意义内容被降级删除时必须告警；不认识的扩展与已知字段畸形值处理不同。协议版本由双方输入 / `RUN_STARTED` 声明，不能用 npm 包 semver 代替协商。[版本兼容](https://github.com/ag-ui-protocol/ag-ui/blob/f77065ad109c40e60ecbdec9d8fa6fa09987c41e/docs/spec/1.0/basic/versioning.mdx)
- **连接恢复不等于业务 exactly-once。** 工具结果重放、断线重连、刷新及多客户端仍需绑定可信身份与动作记录，并验证重复执行。本轮只读规范与发行，未证明任意适配器已经满足这些要求。
- 根代码 MIT；模型、宿主服务与各个模板有独立配置和费用。源码中的版本号、npm 已发布版本、部署镜像及线上服务仍应分别记录。[清单](https://github.com/ag-ui-protocol/ag-ui/blob/f77065ad109c40e60ecbdec9d8fa6fa09987c41e/sdks/typescript/packages/core/package.json)、[许可](https://github.com/ag-ui-protocol/ag-ui/blob/f77065ad109c40e60ecbdec9d8fa6fa09987c41e/LICENSE)

## 补充建议

先做只读最小交互，再验证同意、拒绝、超时、遗漏一个 interrupt、刷新恢复、工具结果重复和越权 state。保留原始输入 / 事件及版本警告，同时避免记录真实秘密。

若已有 A2UI renderer，可把 AG-UI 当作事件交互层评估；先固定 catalog、schema 与业务动作授权，分别验收可渲染、可交互和真实动作。对比 1.0 规范与所用 integration，不能只看 README 的 Supported 标记。

## 参考资料

- [仓库 API](https://api.github.com/repos/ag-ui-protocol/ag-ui)、[11-13 包发行](https://github.com/ag-ui-protocol/ag-ui/releases/tag/release%2F2026-11-13)。
- [固定 README](https://github.com/ag-ui-protocol/ag-ui/blob/f77065ad109c40e60ecbdec9d8fa6fa09987c41e/README.md)、[入门](https://github.com/ag-ui-protocol/ag-ui/blob/f77065ad109c40e60ecbdec9d8fa6fa09987c41e/docs/quickstart/applications.mdx)、[core 清单](https://github.com/ag-ui-protocol/ag-ui/blob/f77065ad109c40e60ecbdec9d8fa6fa09987c41e/sdks/typescript/packages/core/package.json)、[MIT 许可](https://github.com/ag-ui-protocol/ag-ui/blob/f77065ad109c40e60ecbdec9d8fa6fa09987c41e/LICENSE)。
- [1.0 架构](https://github.com/ag-ui-protocol/ag-ui/blob/f77065ad109c40e60ecbdec9d8fa6fa09987c41e/docs/spec/1.0/architecture.mdx)、[中断](https://github.com/ag-ui-protocol/ag-ui/blob/f77065ad109c40e60ecbdec9d8fa6fa09987c41e/docs/spec/1.0/basic/patterns/interrupt-resume.mdx)、[状态](https://github.com/ag-ui-protocol/ag-ui/blob/f77065ad109c40e60ecbdec9d8fa6fa09987c41e/docs/spec/1.0/events/state.mdx)、[版本协商](https://github.com/ag-ui-protocol/ag-ui/blob/f77065ad109c40e60ecbdec9d8fa6fa09987c41e/docs/spec/1.0/basic/versioning.mdx)。
