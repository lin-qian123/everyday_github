# everyday_github

一个持续更新的 AI 开源项目与平台热点中文索引仓库，按天记录 GitHub / X / Instagram / YouTube 的热点变化，并为重点项目沉淀中文解读。

## 目录

- [这是什么](#这是什么)
- [收录范围](#收录范围)
- [如何使用](#如何使用)
- [仓库结构](#仓库结构)
- [项目分类索引](#项目分类索引)
  - [Coding Agents 与终端助手](#coding-agents-与终端助手)
  - [Agent 框架与技能生态](#agent-框架与技能生态)
  - [记忆层与个人 AI 基础设施](#记忆层与个人-ai-基础设施)
  - [RAG、检索与知识处理](#rag检索与知识处理)
  - [前端、UI 与 Agent 交互层](#前端ui-与-agent-交互层)
  - [语音、视频与多模态](#语音视频与多模态)
  - [模型、训练与推理基础设施](#模型训练与推理基础设施)
  - [办公、商业与行业应用](#办公商业与行业应用)
- [完整索引与每日热点](#完整索引与每日热点)
- [当前状态](#当前状态)
- [维护约定](#维护约定)

## 这是什么

这个仓库主要做三件事：

- 每日跟踪 GitHub 上靠前的 AI 开源项目。
- 为重点项目建立中文说明，记录定位、用法、原理、价值与风险边界。
- 汇总 X、GitHub、Instagram、YouTube 等平台的 AI 热点，形成可追溯的日报。

它不是单纯的“项目收藏夹”，而是一个面向研究、选型和长期跟踪的中文工作仓库。

## 收录范围

- `AI coding / agent`：终端助手、代码代理、自动化工作流。
- `Agent infra`：技能系统、MCP、浏览器控制、沙箱、上下文注入。
- `Memory / RAG`：长期记忆、知识库、索引、抓取、检索。
- `Multimodal`：语音、视频、数字人、搜索与摘要。
- `Models / Systems`：模型训练、推理框架、量化、向量检索。
- `Applied AI`：金融、产品管理、演示文稿、个人效率等应用层项目。

## 如何使用

1. 先看 [`daily/`](./daily/) 下最近一天的 `ai-hotspots.md`，快速了解当天热点。
2. 再按下面的分类索引进入感兴趣的项目目录。
3. 深入时直接打开 [`projects/`](./projects/) 下对应项目的 `README.md`。

如果你是第一次进入这个仓库，建议从这几个入口开始：

- 最新日报：[`daily/2026-06-23/ai-hotspots.md`](./daily/2026-06-23/ai-hotspots.md)
- 项目总目录：[`projects/`](./projects/)
- 自动化约束：[`AGENTS.md`](./AGENTS.md)
- 开发续接记录：[`TODO.md`](./TODO.md)

## 仓库结构

- `daily/`：按日期归档的热点日报。
- `projects/`：统一存放所有项目说明目录。
- `projects/<project>/README.md`：单个项目的中文介绍与分析。
- `AGENTS.md`：自动化执行规则。
- `TODO.md`：待办事项、阶段记录与接续线索。

## 项目分类索引

说明：

- 首页只放“精选索引”，强调可读性，不把 200+ 项目全部堆在首页。
- 每个项目都可在 [`projects/`](./projects/) 找到独立中文说明。
- 链接优先放 GitHub 仓库主页，便于快速打开与二次判断。

### Coding Agents 与终端助手

| 项目 | 简介 | 链接 |
| --- | --- | --- |
| `codex` | OpenAI 的开源 coding agent，偏终端协作与代码任务执行。 | [GitHub](https://github.com/openai/codex) |
| `claude-code` | Anthropic 的终端代码助手，强调仓库理解、改动执行与工作流协作。 | [GitHub](https://github.com/anthropics/claude-code) |
| `OpenHands` | 面向通用软件任务的开源 AI 开发代理。 | [GitHub](https://github.com/All-Hands-AI/OpenHands) |
| `opencode` | 增长很快的开源 coding agent，强调终端中的 agentic 开发体验。 | [GitHub](https://github.com/anomalyco/opencode) |
| `kilocode` | 覆盖 VS Code、JetBrains 与 CLI 的开源 coding agent 平台。 | [GitHub](https://github.com/Kilo-Org/kilocode) |
| `goose` | 可扩展的通用代理执行器，适合自动化与工程操作。 | [GitHub](https://github.com/aaif-goose/goose) |
| `cline` | 面向 IDE 工作流的 AI 编码助手，社区热度长期较高。 | [GitHub](https://github.com/cline/cline) |
| `aider` | 偏向实际改代码与提交循环的老牌 CLI 助手。 | [GitHub](https://github.com/paul-gauthier/aider) |
| `continue` | 从 IDE 助手演进到 PR / CI 中的 AI 检查与代码治理路线。 | [GitHub](https://github.com/continuedev/continue) |
| `cursor` | 产品化 AI IDE 代表项，体现“编辑器即 Agent 入口”的路线。 | [GitHub](https://github.com/cursor/cursor) |
| `qwen-code` | 阿里系开源终端 coding agent，围绕 Qwen coder 能力优化。 | [GitHub](https://github.com/QwenLM/qwen-code) |
| `tabby` | 自托管、可本地部署的开源 AI 编码助手。 | [GitHub](https://github.com/TabbyML/tabby) |
| `zed` | 高性能、多人协作的代码编辑器，体现 AI 时代开发入口向编辑器本体回流。 | [GitHub](https://github.com/zed-industries/zed) |

### Agent 框架与技能生态

| 项目 | 简介 | 链接 |
| --- | --- | --- |
| `autogen` | Microsoft 的多代理编排框架。 | [GitHub](https://github.com/microsoft/autogen) |
| `crewAI` | 面向多角色协作的 agent workflow 框架。 | [GitHub](https://github.com/crewAIInc/crewAI) |
| `Flowise` | 低代码 AI workflow / agent 编排平台。 | [GitHub](https://github.com/FlowiseAI/Flowise) |
| `agno` | 面向 agent 应用构建的全栈式框架。 | [GitHub](https://github.com/agno-agi/agno) |
| `CopilotKit` | 面向 Agent Native 应用的前端交互层框架。 | [GitHub](https://github.com/CopilotKit/CopilotKit) |
| `browser-use` | 把浏览器控制能力接进 agent 工作流。 | [GitHub](https://github.com/browser-use/browser-use) |
| `cua` | computer-use agent 基础设施套件，覆盖桌面驱动、沙箱、基准与虚拟化。 | [GitHub](https://github.com/trycua/cua) |
| `chrome-devtools-mcp` | 将 Chrome DevTools 能力封装为 MCP 工具。 | [GitHub](https://github.com/ChromeDevTools/chrome-devtools-mcp) |
| `skills` | 面向多代理环境的技能安装与分发工具。 | [GitHub](https://github.com/vercel-labs/skills) |
| `context7` | 为 LLM / agent 提供更稳定上下文注入的开发基础设施。 | [GitHub](https://github.com/upstash/context7) |
| `modelcontextprotocol-servers` | MCP 官方服务器集合，是当前 agent 工具生态的基础目录之一。 | [GitHub](https://github.com/modelcontextprotocol/servers) |
| `postman-mcp-server` | Postman 官方 MCP Server，把 API 工作区与集合管理能力接进 agent。 | [GitHub](https://github.com/postmanlabs/postman-mcp-server) |
| `babyagi` | 经典 autonomous agent 名字的新实验版本，偏函数式 agent 研究样本。 | [GitHub](https://github.com/yoheinakajima/babyagi) |
| `JARVIS` | HuggingGPT 路线代表项目，用 LLM 做任务规划与外部模型路由。 | [GitHub](https://github.com/microsoft/JARVIS) |
| `ponytail` | 把“少写代码、优先现成能力”的工程约束注入多种 coding agent。 | [GitHub](https://github.com/DietrichGebert/ponytail) |
| `omnigent` | 多 agent 共享会话、共享策略和共享沙箱的 meta-harness。 | [GitHub](https://github.com/omnigent-ai/omnigent) |
| `agent-native` | 把 Agent、UI、动作层和共享状态统一到同一产品架构里的 agent-native 应用框架。 | [GitHub](https://github.com/BuilderIO/agent-native) |
| `flue` | 强调 sandbox、durable execution、skills 和 subagents 的 TypeScript agent harness 框架。 | [GitHub](https://github.com/withastro/flue) |
| `mcphub` | 面向多 MCP server 的统一网关与路由层，强调管理、编排与权限控制。 | [GitHub](https://github.com/samanhappy/mcphub) |
| `Archon` | 把 AI 编码流程写成 YAML workflow 的工作流引擎，强调确定性与可重复执行。 | [GitHub](https://github.com/coleam00/Archon) |
| `background-agents` | 面向团队后台异步执行的开源 coding agent 系统，覆盖 Web、Slack、GitHub 和定时任务入口。 | [GitHub](https://github.com/ColeMurray/background-agents) |

### 记忆层与个人 AI 基础设施

| 项目 | 简介 | 链接 |
| --- | --- | --- |
| `mem0` | 热度很高的长期记忆基础设施项目。 | [GitHub](https://github.com/mem0ai/mem0) |
| `memsearch` | 面向 coding agent 的可检索持久记忆层。 | [GitHub](https://github.com/zilliztech/memsearch) |
| `agentmemory` | 强调 agent 可复用记忆的轻量项目。 | [GitHub](https://github.com/rohitg00/agentmemory) |
| `claude-mem` | 面向 Claude 工作流的记忆插件路线。 | [GitHub](https://github.com/thedotmack/claude-mem) |
| `Personal_AI_Infrastructure` | Daniel Miessler 的个人 AI 基础设施方案。 | [GitHub](https://github.com/danielmiessler/Personal_AI_Infrastructure) |
| `supermemory` | 试图把“记忆”做成可复用产品层能力。 | [GitHub](https://github.com/supermemoryai/supermemory) |
| `open-notebook` | 把笔记与 AI 工作流结合的本地化知识项目。 | [GitHub](https://github.com/lfnovo/open-notebook) |
| `openless` | 强调输入整理、提示加工和结构化输出的效率工具。 | [GitHub](https://github.com/Open-Less/openless) |
| `agentsview` | 本地优先的 coding agent 会话搜索、成本统计与使用分析面板。 | [GitHub](https://github.com/kenn-io/agentsview) |
| `codebase-memory-mcp` | 面向 agent 的代码知识图谱与持久记忆层，把仓库结构索引成可查询 MCP 能力。 | [GitHub](https://github.com/DeusData/codebase-memory-mcp) |
| `cognee` | 面向 agent 的开源长期记忆平台，把文档、工具调用和上下文沉淀为可查询知识图谱。 | [GitHub](https://github.com/topoteretes/cognee) |
| `ax` | 面向 Claude Code、Codex 等工具的本地 agent 复盘、记忆、成本与 observability 图谱层。 | [GitHub](https://github.com/Necmttn/ax) |

### RAG、检索与知识处理

| 项目 | 简介 | 链接 |
| --- | --- | --- |
| `ragflow` | 开源 RAG 平台，长期位于高热榜。 | [GitHub](https://github.com/infiniflow/ragflow) |
| `anything-llm` | 一体化知识库问答与本地 LLM 工作台。 | [GitHub](https://github.com/Mintplex-Labs/anything-llm) |
| `dify` | AI 应用平台，也常被用来快速搭建知识库应用。 | [GitHub](https://github.com/langgenius/dify) |
| `cocoindex` | 索引构建与持续更新导向的知识处理基础设施。 | [GitHub](https://github.com/cocoindex-io/cocoindex) |
| `crawl4ai` | 面向 LLM 场景的网页抓取与结构化提取工具。 | [GitHub](https://github.com/unclecode/crawl4ai) |
| `firecrawl` | 把搜索、抓取、交互和结构化提取封装成统一 Web context API 的热门基础设施。 | [GitHub](https://github.com/firecrawl/firecrawl) |
| `turbovec` | 低内存向量检索库，代表检索压缩层热点。 | [GitHub](https://github.com/RyanCodrai/turbovec) |
| `paperless-ngx` | 文档归档、OCR 与可搜索知识仓库工具。 | [GitHub](https://github.com/paperless-ngx/paperless-ngx) |
| `local-deep-research` | 偏本地化 deep research / 文献搜集工作流。 | [GitHub](https://github.com/LearningCircuit/local-deep-research) |
| `milvus` | 大规模向量检索底座，适合生产级 RAG 基础设施。 | [GitHub](https://github.com/milvus-io/milvus) |
| `qdrant` | 强调过滤、混合检索和多向量表达的 AI 搜索引擎。 | [GitHub](https://github.com/qdrant/qdrant) |
| `haystack` | 面向生产级 LLM / RAG / agent 的透明编排框架。 | [GitHub](https://github.com/deepset-ai/haystack) |
| `llama_index` | 把文档解析、索引、检索与 agent 连接起来的数据接入层框架。 | [GitHub](https://github.com/run-llama/llama_index) |
| `chroma` | 轻量、AI 友好的搜索与向量检索基础设施。 | [GitHub](https://github.com/chroma-core/chroma) |
| `faiss` | Meta 主导的向量相似度搜索与聚类库，是很多检索系统的底层内核。 | [GitHub](https://github.com/facebookresearch/faiss) |
| `Hyper-Extract` | 把非结构化文档抽成强类型知识对象、图谱和超图的知识抽取 CLI。 | [GitHub](https://github.com/yifanfeng97/Hyper-Extract) |

### 前端、UI 与 Agent 交互层

| 项目 | 简介 | 链接 |
| --- | --- | --- |
| `awesome-design-md` | 收集 `DESIGN.md` 模板的设计约束索引仓库。 | [GitHub](https://github.com/VoltAgent/awesome-design-md) |
| `design-md` | Google Labs 的设计说明格式实践。 | [GitHub](https://github.com/google-labs-code/design.md) |
| `open-design` | 面向开放设计流程和组件思路的项目。 | [GitHub](https://github.com/nexu-io/open-design) |
| `AionUi` | 偏 AI 应用界面的组件/模板方向。 | [GitHub](https://github.com/iOfficeAI/AionUi) |
| `UI-TARS-desktop` | 偏桌面 Agent UI 与可操作前端表面。 | [GitHub](https://github.com/bytedance/UI-TARS-desktop) |
| `OpenSandbox` | 为 Agent 提供可控执行环境与隔离层。 | [GitHub](https://github.com/alibaba/OpenSandbox) |
| `page-agent` | 页面级 agent 交互与操作路线。 | [GitHub](https://github.com/alibaba/page-agent) |
| `lightpanda-browser` | 为自动化与 Agent 场景设计的高性能浏览器内核路线。 | [GitHub](https://github.com/lightpanda-io/browser) |
| `openui` | 开源生成式 UI 原型工具，支持描述界面并导出到多种前端框架。 | [GitHub](https://github.com/wandb/openui) |
| `chatbot-ui` | 开源 AI 聊天前端骨架，适合做多模型、自托管聊天入口。 | [GitHub](https://github.com/mckaywrigley/chatbot-ui) |
| `stitch-mcp` | 把 Google Stitch 生成的 UI 设计接入本地开发与 coding agent 工作流的 CLI / MCP 桥接层。 | [GitHub](https://github.com/davideast/stitch-mcp) |

### 语音、视频与多模态

| 项目 | 简介 | 链接 |
| --- | --- | --- |
| `MOSS-TTS` | OpenMOSS 的语音生成模型家族。 | [GitHub](https://github.com/OpenMOSS/MOSS-TTS) |
| `fish-speech` | 社区热度很高的开源语音模型项目。 | [GitHub](https://github.com/fishaudio/fish-speech) |
| `Open-LLM-VTuber` | 把 LLM、角色扮演与 VTuber 工作流结合。 | [GitHub](https://github.com/Open-LLM-VTuber/Open-LLM-VTuber) |
| `Deep-Live-Cam` | 偏实时视觉生成与视频增强。 | [GitHub](https://github.com/hacksider/Deep-Live-Cam) |
| `Pixelle-Video` | 视频生成/编辑方向的高热项目。 | [GitHub](https://github.com/AIDC-AI/Pixelle-Video) |
| `video-search-and-summarization` | NVIDIA 的视频搜索与摘要蓝图。 | [GitHub](https://github.com/NVIDIA-AI-Blueprints/video-search-and-summarization) |
| `voicebox` | 本地优先的语音合成与声音工作台。 | [GitHub](https://github.com/jamiepine/voicebox) |
| `VibeVoice` | Microsoft 的语音方向项目。 | [GitHub](https://github.com/microsoft/VibeVoice) |
| `OpenMontage` | 多代理驱动的开源视频生产系统，把研究、脚本、素材、字幕和合成串成完整流水线。 | [GitHub](https://github.com/calesthio/OpenMontage) |
| `palmier-pro` | 面向 macOS 的 AI 时间线视频编辑器，支持通过 MCP 与 Claude / Codex / Cursor 协作。 | [GitHub](https://github.com/palmier-io/palmier-pro) |
| `LTX-2` | Lightricks 的音视频基础模型与推理/训练工具栈，覆盖 audio-to-video、lipdub 与多条视频 pipeline。 | [GitHub](https://github.com/Lightricks/LTX-2) |

### 模型、训练与推理基础设施

| 项目 | 简介 | 链接 |
| --- | --- | --- |
| `llama.cpp` | 本地推理生态的标志性项目。 | [GitHub](https://github.com/ggml-org/llama.cpp) |
| `vllm` | 高性能推理服务框架。 | [GitHub](https://github.com/vllm-project/vllm) |
| `LocalAI` | 本地优先的开源 AI 引擎，兼容 OpenAI / Anthropic API。 | [GitHub](https://github.com/mudler/LocalAI) |
| `ollama` | 当前最主流的本地模型运行底座之一，承担拉取、运行与统一接口暴露。 | [GitHub](https://github.com/ollama/ollama) |
| `sglang` | 面向大模型与多模态模型的高性能 serving 基础设施。 | [GitHub](https://github.com/sgl-project/sglang) |
| `gemini-cli` | Google 的 CLI 入口项目，兼具模型调用与开发体验属性。 | [GitHub](https://github.com/google-gemini/gemini-cli) |
| `FastChat` | 老牌 LLM 训练、服务与评测底座，连接 Chatbot Arena 与多模型 API 路线。 | [GitHub](https://github.com/lm-sys/FastChat) |
| `BitNet` | 微软系低比特模型路线代表项目。 | [GitHub](https://github.com/microsoft/BitNet) |
| `TabPFN` | 表格机器学习方向的高热项目。 | [GitHub](https://github.com/PriorLabs/TabPFN) |
| `timesfm` | Google 的时间序列基础模型。 | [GitHub](https://github.com/google-research/timesfm) |
| `train-llm-from-scratch` | 从零训练 LLM 的学习型项目。 | [GitHub](https://github.com/FareedKhan-dev/train-llm-from-scratch) |
| `minimind` | 偏教学与实验导向的小型模型项目。 | [GitHub](https://github.com/jingyaogong/minimind) |
| `text-generation-webui` | 本地模型工作台，兼顾 UI、多后端和 OpenAI-compatible API。 | [GitHub](https://github.com/oobabooga/text-generation-webui) |
| `llamafile` | 把本地大模型打包成单文件可执行体的分发方案。 | [GitHub](https://github.com/Mozilla-Ocho/llamafile) |
| `GLM-5` | 智谱 / Z.ai 面向长时程 agentic engineering 的开源大模型系列。 | [GitHub](https://github.com/zai-org/GLM-5) |
| `Rapid-MLX` | 面向 Apple Silicon 的本地 AI 推理引擎，主打 OpenAI-compatible 接口与 agent 工具调用。 | [GitHub](https://github.com/raullenchai/Rapid-MLX) |

### 办公、商业与行业应用

| 项目 | 简介 | 链接 |
| --- | --- | --- |
| `pm-skills` | 把 PM 方法论封装成 agent 可调用技能。 | [GitHub](https://github.com/phuryn/pm-skills) |
| `career-ops` | 面向求职、简历、职业运营的 AI 工作流项目。 | [GitHub](https://github.com/santifer/career-ops) |
| `financial-services` | Anthropic 的金融服务场景能力示例。 | [GitHub](https://github.com/anthropics/financial-services) |
| `financial-services-plugins` | 配套金融插件与行业工作流扩展。 | [GitHub](https://github.com/anthropics/financial-services-plugins) |
| `AI-Trader` | 交易与量化分析方向的 AI 项目。 | [GitHub](https://github.com/HKUDS/AI-Trader) |
| `TradingAgents` | 多代理交易研究与决策框架。 | [GitHub](https://github.com/TauricResearch/TradingAgents) |
| `Vibe-Trading` | 偏交易工作流的 agent 化项目。 | [GitHub](https://github.com/HKUDS/Vibe-Trading) |
| `presenton` | 开源 AI 演示文稿生成器。 | [GitHub](https://github.com/presenton/presenton) |
| `ppt-master` | 生成原生可编辑 PPTX 的 agent 工作流，强调真实办公交付物。 | [GitHub](https://github.com/hugohe3/ppt-master) |
| `daily_stock_analysis` | 用大模型驱动多市场股票分析、定时推送与 Web 工作台的行业应用型系统。 | [GitHub](https://github.com/ZhuLinsen/daily_stock_analysis) |

## 完整索引与每日热点

- 全量项目目录：[`projects/`](./projects/)
- 最近日报：
  - [`2026-06-23`](./daily/2026-06-23/ai-hotspots.md)
  - [`2026-06-22`](./daily/2026-06-22/ai-hotspots.md)
  - [`2026-06-21`](./daily/2026-06-21/ai-hotspots.md)
  - [`2026-06-20`](./daily/2026-06-20/ai-hotspots.md)
  - [`2026-06-19`](./daily/2026-06-19/ai-hotspots.md)
  - [`2026-06-18`](./daily/2026-06-18/ai-hotspots.md)
  - [`2026-06-17`](./daily/2026-06-17/ai-hotspots.md)

如果你要找的是某个具体项目，而不是看分类，直接在 [`projects/`](./projects/) 中按名称查找会更快。

## 当前状态

- 状态：持续日更中。
- 最新更新：`2026-06-23`。
- 当前项目总数：`251`。
- 最近新增项目：`ax`、`firecrawl`、`daily_stock_analysis`。
- 覆盖平台：GitHub、X、Instagram、YouTube。

## 维护约定

- 默认直接在当前分支更新，不新建分支。
- 所有项目目录统一收纳到 `projects/`。
- 每日自动化不仅更新 `daily/` 与 `projects/`，还要同步维护首页分类导航、项目简介和链接。
- 新项目优先归入既有分类；只有在现有分类明显不合适时才新增分类。
- 自动化成功完成后，默认提交并推送到 `origin/master`。
- 热点内容优先采用官方来源与主流媒体交叉验证。
- 对争议性结论明确区分“事实、判断、不确定性”。
- 若 GitHub 头部热点已在仓库中建立目录，则优先刷新既有项目说明，并在当日日报中显式说明取舍。
