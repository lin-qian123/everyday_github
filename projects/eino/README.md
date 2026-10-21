<!-- markdownlint-disable MD013 -->

# Eino

> 更新：2026-10-22（Asia/Shanghai）。分类：Agent 框架与技能生态。主上游 `cloudwego/eino`；默认分支快照 `0a5ca53b9d3b`。官方资料与源码静态研究；热度、发行及社媒口径见[当日日报](../../daily/2026-10-22/ai-hotspots.md)。

## 定位

CloudWeGo 的 Go LLM 应用框架，提供 ChatModel / Tool / Retriever 等抽象、ADK Agent、图与工作流组合；具体 provider 接入主要在 eino-ext，示例在 eino-examples。框架不是预装完整业务能力的独立助手。[README.md](https://github.com/cloudwego/eino/blob/0a5ca53b9d3bf7b661dccc863465ec568a421eea/README.md)

## 用法

模块路径 `github.com/cloudwego/eino`，`go.mod` 声明 Go `1.18`；应固定本仓库、eino-ext 与所选 provider 的兼容版本，并检查所有依赖的实际工具链要求。当前最近正式 Release 为 `v0.9.22`。[go.mod](https://github.com/cloudwego/eino/blob/0a5ca53b9d3bf7b661dccc863465ec568a421eea/go.mod) [README.md](https://github.com/cloudwego/eino/blob/0a5ca53b9d3bf7b661dccc863465ec568a421eea/README.md)

官方快速路径为创建 ChatModel、配置 `adk.NewChatModelAgent`，再经 `adk.NewRunner(...).Query` 消费事件。先只接 mock / 只读工具，检查流式结束、错误和费用；README 示例中省略的错误处理应在真实服务中补齐。[README.md](https://github.com/cloudwego/eino/blob/0a5ca53b9d3bf7b661dccc863465ec568a421eea/README.md)

## 原理

ADK 管理模型与工具的 ReAct 回合；compose 把确定性节点连为可编译图，处理流式数据转换，图也能封成 Agent 工具。callbacks 提供观测注入，中断 / 恢复承载人机交互状态与路由。[README.md](https://github.com/cloudwego/eino/blob/0a5ca53b9d3bf7b661dccc863465ec568a421eea/README.md) [adk/interrupt.go](https://github.com/cloudwego/eino/blob/0a5ca53b9d3bf7b661dccc863465ec568a421eea/adk/interrupt.go)

## 价值

工程判断：适合已有 Go 服务、想把稳定业务流水线与模型选择结合的团队。类型接口、流式和图结构有助于统一接入；可靠性仍需来自应用自身的任务真值、超时和副作用控制。

## 风险边界

- `ToolsNodeConfig.ExecuteSequentially` 默认 false，即工具并行执行；对共享文件、订单等写入，需要显式选择顺序或做并发 / 幂等治理。工具名与 schema 不构成授权机制。[compose/tool_node.go](https://github.com/cloudwego/eino/blob/0a5ca53b9d3bf7b661dccc863465ec568a421eea/compose/tool_node.go)
- 支持 interrupt / resume 不表示所有敏感动作默认审批；应用要在正确边界发起中断、保存 checkpoint 并决定何时恢复。重试或恢复需验证是否重放已执行副作用。[adk/interrupt.go](https://github.com/cloudwego/eino/blob/0a5ca53b9d3bf7b661dccc863465ec568a421eea/adk/interrupt.go) [compose/tool_node.go](https://github.com/cloudwego/eino/blob/0a5ca53b9d3bf7b661dccc863465ec568a421eea/compose/tool_node.go)
- callbacks / tracing 可能接触 prompt、检索结果与工具输出；具体网络出口、脱敏和留存由选用的组件与 handler 决定。DeepAgent 配 shell / Python 后的权限来自宿主。[README.md](https://github.com/cloudwego/eino/blob/0a5ca53b9d3bf7b661dccc863465ec568a421eea/README.md)
- Apache-2.0 适用于本仓库代码，provider、模型、数据和外部集成需另核。[LICENSE-APACHE](https://github.com/cloudwego/eino/blob/0a5ca53b9d3bf7b661dccc863465ec568a421eea/LICENSE-APACHE)

## 补充建议

先做一个确定性图：输入校验 → mock 模型 → 输出校验，再加只读查询。以超时、取消、重复回调、两工具冲突和审批恢复做故障注入，记录副作用次数、trace 内容与成本。本轮未构建 Go 项目，也未调用 provider。

## 参考资料

- [README.md](https://github.com/cloudwego/eino/blob/0a5ca53b9d3bf7b661dccc863465ec568a421eea/README.md)
- [go.mod](https://github.com/cloudwego/eino/blob/0a5ca53b9d3bf7b661dccc863465ec568a421eea/go.mod)
- [LICENSE-APACHE](https://github.com/cloudwego/eino/blob/0a5ca53b9d3bf7b661dccc863465ec568a421eea/LICENSE-APACHE)
- [compose/tool_node.go](https://github.com/cloudwego/eino/blob/0a5ca53b9d3bf7b661dccc863465ec568a421eea/compose/tool_node.go)
- [adk/interrupt.go](https://github.com/cloudwego/eino/blob/0a5ca53b9d3bf7b661dccc863465ec568a421eea/adk/interrupt.go)
- [仓库 API](https://api.github.com/repos/cloudwego/eino)
- [v0.9.22 Release](https://github.com/cloudwego/eino/releases/tag/v0.9.22)
