<!-- markdownlint-disable MD013 -->

# Open Intelligent UI（CopilotKit/OpenIntelligentUI）中文解读

> 上游仓库：<https://github.com/CopilotKit/OpenIntelligentUI> · 归类：前端、UI 与 Agent 交互层 · 本页基于 2026-10-12 的 README、架构、交互、路由、部署文档、许可证与 GitHub REST API 静态整理；未配置 provider key、启动应用或对生成 UI 做浏览器安全测试。

## 定位

Open Intelligent UI 是 CopilotKit 的开源 Generative UI 示例：Agent 不只返回文本，还能选择原生组件或生成可交互 HTML / CSS / JavaScript，用图表、3D 解释、计算器与地图回答问题。它更像一套可改造的完整应用与模式参考，而不是通用低代码平台。

## 用法

上游要求 Node.js 22+、pnpm 9+、Python 3.12+ 与 uv。`make setup && make dev` 启动 Next.js 前端和 Python Agent；默认回答模型需要 OpenAI key，Jev visualization router 需要 Typesafe key。浏览器输入的 key 只保存在内存，但会经应用服务器发送到各 provider。

## 原理

- Next.js / CopilotKit 把对话事件流送到 FastAPI + LangGraph / Deep Agent。
- Agent 在纯文本、native component、A2UI table 与 `generateSandboxedUi` 之间选择输出。
- 自定义 CSS / HTML / JavaScript 流式进入隔离 Websandbox iframe；host 只暴露经验证的 `sendPrompt` 与 HTTPS `openLink` bridge。
- checkpoint 使用进程内 `BoundedMemorySaver(max_threads=200)`；当前不是持久化共享状态。

## 价值

- 展示 Generative UI 从 Agent tool call、流式参数到隔离 renderer 的完整链路。
- 明确区分结构化原生组件与自定义 UI，便于按风险和可维护性选择 renderer。
- 示例覆盖交互解释、对比、计算器和地图，可作为产品原型与测试基线。

## 风险边界

- iframe sandbox 降低同源访问面，但不证明生成内容事实正确、无视觉欺骗、无外部资源风险或无桥接逻辑漏洞。
- 示例数据、路线与价格明确是演示，不是实时业务事实；“可交互”也不等于计算、单位或决策正确。
- key 经自托管应用转发到 provider；浏览器不落盘不等于服务端、网络、provider 或 tracing 路径无数据风险。
- 进程内 checkpoint 在重启 / 横向扩容时会丢失或分裂；生产部署需独立设计认证、租户、持久化、配额与审计。

## 补充建议

- 用 CSP、网络 allowlist、bridge schema fuzzing、恶意 HTML / CSS / JS fixture 与可访问性测试验证 renderer。
- 对每类 native / generated UI 建确定性数据和计算 oracle，不把动画或漂亮图表当作事实证明。
- 在生产化前替换内存 checkpoint，并对 key、conversation、generated artifact、external assets 画完整数据流。

## 参考资料

- GitHub 仓库：<https://github.com/CopilotKit/OpenIntelligentUI>
- GitHub REST API：<https://api.github.com/repos/CopilotKit/OpenIntelligentUI>
- 架构：<https://github.com/CopilotKit/OpenIntelligentUI/blob/main/docs/architecture.md>
- Interactive answers：<https://github.com/CopilotKit/OpenIntelligentUI/blob/main/docs/interactive-answers.md>
- Visualization routing：<https://github.com/CopilotKit/OpenIntelligentUI/blob/main/docs/visualization-routing.md>
- Deployment：<https://github.com/CopilotKit/OpenIntelligentUI/blob/main/docs/deployment.md>
- LICENSE：<https://github.com/CopilotKit/OpenIntelligentUI/blob/main/LICENSE>
