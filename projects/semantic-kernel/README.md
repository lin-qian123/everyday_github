<!-- markdownlint-disable MD013 MD034 -->

# semantic-kernel

`microsoft/semantic-kernel` 是 Microsoft 的模型无关 AI agent / multi-agent SDK。当前 README 明确提示 Semantic Kernel 已演进到 Microsoft Agent Framework 方向，但原仓库仍是理解微软 agent 编排、插件、memory、process framework 和多语言 SDK 的重要入口。

- GitHub：https://github.com/microsoft/semantic-kernel
- 文档入口：https://aka.ms/semantic-kernel
- 迁移方向：https://github.com/microsoft/agent-framework
- 分类：Agent 框架与技能生态
- 许可证：MIT

## 热度信号

- 2026-07-15 通过 GitHub API 抓取时约 `28.3k stars`、`4.7k forks`。
- 仓库在 2026-07-10 仍有 push，topics 包含 `ai`、`llm`、`openai`、`sdk`。
- README 顶部强调 Microsoft Agent Framework 是 Semantic Kernel 的 enterprise-ready successor。

## 定位

Semantic Kernel 主要面向需要把 LLM 接入真实应用的开发者。它的关注点不是单次聊天，而是：

- 如何把模型、工具、插件和 prompt 模板组织成可维护代码。
- 如何在 Python、.NET、Java 等运行时中构建 agent。
- 如何处理多 agent 协作、memory、planning、workflow 和企业集成。

在 2026 年的语境下，它更像 Microsoft agent stack 的历史核心与迁移入口。

## 用法

Python 安装：

```bash
pip install semantic-kernel
```

.NET 安装：

```bash
dotnet add package Microsoft.SemanticKernel
dotnet add package Microsoft.SemanticKernel.Agents.Core
```

使用前通常需要配置 Azure OpenAI、OpenAI 或其他模型服务的 API key。

## 原理

Semantic Kernel 把 agent 应用拆成几类稳定原语：

- 模型连接器：接入 OpenAI、Azure OpenAI、Hugging Face、NVIDIA、Ollama、ONNX 等。
- 插件与函数：把本地函数、OpenAPI spec、prompt template 和 MCP 工具包装成能力。
- agent framework：用 agent、tool、memory、planning 组织任务执行。
- process framework：把业务流程显式建模，而不是完全交给模型自由规划。
- 向量与检索：接入 Azure AI Search、Elasticsearch、Chroma 等数据层。

这种设计适合企业应用，因为它把“模型调用”放回可测试的软件结构里。

## 价值

- 对 Microsoft / Azure 技术栈用户，集成路径清晰。
- 对多语言团队，Python、.NET、Java 的覆盖降低了平台割裂。
- 对企业 agent，插件、流程、memory 和观测能力比单个 demo 更重要。
- 对迁移到 Microsoft Agent Framework 的团队，Semantic Kernel 是理解旧项目和新框架边界的必要背景。

## 风险边界

- README 已明确提示 Microsoft Agent Framework 是后续方向，新项目需要评估是否直接采用 successor。
- 框架能力多，学习曲线不低，轻量脚本型 agent 可能不需要完整 SK。
- 企业集成容易把权限、数据源和插件范围扩大，必须做最小权限和审计。
- 多运行时支持带来 API 差异，团队需要固定语言与版本策略。

## 补充建议

- 新项目优先比较 `semantic-kernel` 与 `microsoft/agent-framework` 的当前 API 稳定性。
- 如果已有 SK 代码，应先查迁移指南，再决定是否重构。
- 对 Azure-heavy 团队，重点验证身份、日志、向量检索和部署治理，而不是只跑 quickstart。
- 与 `openai-agents-python`、`LangGraph`、`Mastra` 对比时，应按语言栈和企业治理需求选择。

## 参考资料

- GitHub 仓库：https://github.com/microsoft/semantic-kernel
- Microsoft Agent Framework：https://github.com/microsoft/agent-framework
- 迁移指南：https://learn.microsoft.com/en-us/agent-framework/migration-guide/from-semantic-kernel
- Semantic Kernel 博客说明：https://devblogs.microsoft.com/agent-framework/semantic-kernel-and-microsoft-agent-framework/
