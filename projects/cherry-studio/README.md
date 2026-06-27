# cherry-studio（CherryHQ/cherry-studio）

- GitHub: https://github.com/CherryHQ/cherry-studio
- 主页: https://cherryai.com
- 文档: https://docs.cherry-ai.com/docs/en-us
- 记录日期: 2026-06-28 (Asia/Shanghai)

## 定位

`cherry-studio` 是一个跨平台 AI 桌面客户端，定位接近“统一的大模型与助手工作台”。它把多家云端模型、本地模型、文档处理、话题管理、MCP 接入和预置助手整合到一个桌面应用里。

## 热度信号

1. GitHub API 在 2026-06-28 抓取时显示约 `47,889 stars`、`4,545 forks`，仓库在 `2026-06-27T22:10:45Z` 仍有推送。
2. GitHub TypeScript 日榜在 2026-06-28 抓取时出现该项目，Trending 页面显示约 `47 stars today`。
3. 官方 README 把它定义为 `AI productivity studio with smart chat, autonomous agents, and 300+ assistants`，并列出 `MCP Server`、`300+ Pre-configured AI Assistants`、本地模型与多家云端模型统一接入。

## 用法

### 1) 下载 release 或 nightly 版本

README 首页直接给出 GitHub releases 入口，适合先体验桌面客户端。

### 2) 配置模型来源

官方说明支持 OpenAI、Gemini、Anthropic、Claude、Perplexity、Poe，以及本地 Ollama、LM Studio。

### 3) 使用预置助手、文档处理与 MCP 能力

- 选择现成 assistant 或自定义助手。
- 导入文本、图片、Office、PDF 等资料。
- 通过 MCP Server、主题管理、翻译、Mermaid 等能力扩展使用场景。

## 原理

1. 它的核心不是单模型聊天，而是把模型接入层、助手层、文档层和客户端体验层打包成一体。
2. 这类产品试图解决的不是“某个模型强不强”，而是“在一台机器上怎么高效组织多个模型与多个工作主题”。
3. 从 roadmap 看，项目还在继续往 deep research、OCR、MCP marketplace、知识管理和移动端扩展。

## 价值

- 对经常切换多模型、多助手和多资料来源的人，这类桌面工作台比单一 Web 聊天入口更高效。
- 它说明热点不只在编码 agent，面向普通知识工作的本地 AI 客户端也在继续收敛成稳定赛道。
- 如果对比 `hermes-studio`、`chatbot-ui`、`openui`，`cherry-studio` 更偏个人生产力工作台，而不是纯 agent 控制面或前端框架。

## 风险边界

- 多模型统一入口会带来 API key 管理、数据外发、供应商策略差异和成本不可见等问题。
- “300+ assistants” 更像分发与组合能力，不等于每个助手都有稳定的专业质量。
- 若用于企业资料处理，仍需额外评估本地缓存、同步与隐私边界。

## 补充建议

1. 先把它看成“多模型桌面工作台”，重点验证模型接入、资料处理和主题管理是否真能减少日常切换成本。
2. 如果正在比较 `hermes-studio` 与这类桌面客户端，区分清楚“agent 控制面”和“个人生产力客户端”两种产品方向。
3. 关注其 roadmap 里的 `MCP Marketplace`，这可能决定它是否会从聊天客户端升级成更完整的 AI 桌面生态入口。

## 参考资料

- https://github.com/CherryHQ/cherry-studio
- https://cherryai.com
- https://docs.cherry-ai.com/docs/en-us
- https://github.com/trending/typescript
