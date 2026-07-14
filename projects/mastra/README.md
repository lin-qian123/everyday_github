<!-- markdownlint-disable MD013 MD034 -->

# mastra

`mastra-ai/mastra` 是一个面向 TypeScript 技术栈的 AI applications / agents 框架。它把 model routing、agents、workflows、human-in-the-loop、memory、RAG、MCP server、evals 和 observability 放进同一套开发体验里。

- GitHub：https://github.com/mastra-ai/mastra
- 官网：https://mastra.ai
- 文档：https://mastra.ai/docs
- 分类：Agent 框架与技能生态
- 许可证：仓库 API 标记为 `NOASSERTION`，使用前需核查当前 LICENSE

## 热度信号

- 2026-07-15 通过 GitHub API 抓取时约 `26.2k stars`、`2.4k forks`。
- 仓库在 2026-07-14 仍有 push，topics 包含 `agents`、`mcp`、`workflows`、`evals`、`typescript`。
- README 标注 Y Combinator W25，并强调面向 production-ready AI products。

## 定位

Mastra 的定位是 TypeScript / Node / React / Next.js 团队的 agent 应用框架。它不像可视化平台那样从画布开始，而是把 agent、workflow、memory、tool、eval 和 observability 组织成代码优先的开发体验。

适合：

- Web 产品团队在现有 TypeScript 应用里嵌入 agent。
- 需要 workflows 明确控制流程，同时保留 agent 自主工具调用。
- 需要 human-in-the-loop、暂停恢复和状态存储的业务流程。

## 用法

README 推荐用脚手架创建项目：

```bash
npm create mastra@latest
```

Mastra Studio 默认用于构建、测试和管理 agents、workflows、tools。具体端口和命令以初始化项目输出为准。

## 原理

Mastra 提供几个核心模块：

- model routing：通过统一接口接入多模型 provider。
- agents：让 LLM 使用 tools 解决开放式任务。
- workflows：用图式工作流显式控制步骤、分支和并行。
- human-in-the-loop：暂停 agent / workflow，等待用户输入或审批。
- memory / RAG：提供 conversation history、retrieval 和 observational memory。
- MCP servers：把 agents、tools 等结构化资源暴露给支持 MCP 的系统。
- evals / observability：为生产 agent 提供度量和调试入口。

## 价值

- 对 TypeScript 团队，上手成本低于切到 Python agent stack。
- workflow 与 agent 并存，适合既要确定性又要模型灵活性的业务。
- human-in-the-loop 和 storage 支持长任务恢复。
- 内置 evals 和 observability，说明项目关注生产化而非纯 demo。

## 风险边界

- TypeScript 生态变化快，依赖版本和框架适配要固定。
- agent 自主循环仍需停止条件、预算和工具权限约束。
- human-in-the-loop 只能降低风险，不能替代真实审计和回滚。
- API 仍在快速演进时，生产项目要预留升级成本。

## 补充建议

- 如果主栈是 Next.js / Node，Mastra 值得与 Vercel AI SDK、LangGraph JS、CopilotKit 一起评估。
- 用 workflows 承载关键业务步骤，把开放式探索留给 agent。
- 对每个工具加超时、重试、幂等和日志。
- 上线前跑 evals，至少覆盖失败输入、工具不可用和权限不足场景。

## 参考资料

- GitHub 仓库：https://github.com/mastra-ai/mastra
- 官网：https://mastra.ai
- 文档：https://mastra.ai/docs
- Models：https://mastra.ai/models
