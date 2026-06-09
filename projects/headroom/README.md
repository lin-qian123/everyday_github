# headroom

## 项目定位
`headroom` 是一个面向 LLM/Agent 工作流的上下文压缩层，核心目标是在不明显损伤回答质量的前提下，把日志、文件、RAG 片段和工具输出先压缩再送给模型，从而降低 token 成本与上下文拥塞。

- GitHub：https://github.com/chopratejas/headroom
- 文档入口：https://headroom-docs.vercel.app/
- 适用人群：高频调用 Claude Code、Codex、Cursor、Aider、OpenAI-compatible API 的工程团队。

## 用法

官方 README 给出的入门路径很直接：

1. 安装：
   - `pip install "headroom-ai[all]"`
   - `npm install headroom-ai`
2. 选择接入模式：
   - `headroom wrap claude`
   - `headroom proxy --port 8787`
   - 或在代码内以内联库方式调用压缩能力。
3. 用 `headroom stats` 观察压缩后的 token 节省情况。

典型落地方式：

- 作为代理层：对已有 OpenAI-compatible 客户端“零代码改造”接入。
- 作为 CLI 包装层：直接包住 Claude Code、Codex、Cursor 一类 agent。
- 作为应用中间件：把压缩能力接进自建 RAG / 多代理系统。

## 原理

从仓库结构与文档入口看，`headroom` 的设计不是单一压缩脚本，而是完整的上下文治理层：

- 压缩层：对长日志、RAG 片段、文件内容做可逆或近可逆压缩，减少模型看到的冗余 token。
- 代理层：通过 `wrap`、`proxy`、`mcp install` 等入口，把压缩能力放到现有 agent 调用链前面。
- 记忆/缓存层：结合共享上下文、缓存优化和失败学习，减少重复上下文传输。
- 兼容层：明确覆盖 Claude Code、Codex、Cursor、Aider、Copilot CLI、OpenClaw 等客户端。

它解决的本质问题不是“让模型更聪明”，而是“别把太多低价值上下文直接喂给模型”。

## 价值

- 对重度 agent 工作流，成本收益非常直接，尤其适合长会话和高频工具调用。
- 比“再换更大上下文模型”更工程化，因为它先处理输入侧冗余。
- 对多代理/RAG 场景价值更高，因为这类系统最容易被日志、检索片段和中间结果淹没。

## 风险边界

- 压缩层一旦做错，最先受损的是证据细节和边界条件，不能只看总体 token 节省。
- 接在代理链路前面意味着它会影响调试体验，必须保留旁路和原文回看能力。
- 对高风险流程（安全审计、合规、医疗、法律）不能默认把压缩视作“无损”。

## 补充建议

- 评估时不要只看平均压缩率，至少补三组基准：长日志、RAG 检索片段、工具输出。
- 生产接入前应验证两件事：压缩后是否丢失关键异常信息；跨 agent 客户端行为是否一致。
- 如果团队已经在做 MCP / Agent 平台层，`headroom` 更适合作为“基础设施插件”，而不是每个项目单独集成。

## 参考资料

- 仓库主页：https://github.com/chopratejas/headroom
- 快速开始：https://headroom-docs.vercel.app/
- 架构文档：https://headroom-docs.vercel.app/architecture
- GitHub Trending：https://github.com/trending
