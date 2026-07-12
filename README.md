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

- 最新日报：[`daily/2026-07-13/ai-hotspots.md`](./daily/2026-07-13/ai-hotspots.md)
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
| `MiMo-Code` | 小米 MiMo 团队的终端原生 coding agent，强调持久记忆、checkpoint、subagent 与目标判定。 | [GitHub](https://github.com/XiaomiMiMo/MiMo-Code) |
| `dao-code` | 围绕 DeepSeek V4 长上下文与 prefix cache 优化的低成本终端 coding agent。 | [GitHub](https://github.com/tigicion/dao-code) |
| `learn-agent` | 从零实现 coding agent 的渐进式教程，覆盖 agent loop、预算、压缩、权限和工具披露。 | [GitHub](https://github.com/7-e1even/learn-agent) |
| `Godcoder` | 本地优先的桌面 coding agent，强调 BYOK、Harness mode、CoWork mode 与 MCP 接入。 | [GitHub](https://github.com/eli-labz/Godcoder) |
| `agterm` | 面向多 agent session 的 macOS 原生终端，用 workspace、status hooks 和 `agtermctl` 管理长任务。 | [GitHub](https://github.com/umputun/agterm) |
| `codex-plugin-cc` | OpenAI 的 Claude Code 插件，在 Claude Code 内调用 Codex 做审查、对抗式审查、救援和会话转移。 | [GitHub](https://github.com/openai/codex-plugin-cc) |
| `herdr` | 终端原生的多 agent session 管理器，用真实 pane、持久会话和状态识别管理 Claude Code、Codex、Copilot 等工具。 | [GitHub](https://github.com/ogulcancelik/herdr) |
| `claude-antigravity-agents` | Claude Code skill，把长审查、研究和第二意见任务委派给 Google Antigravity CLI 子 agent。 | [GitHub](https://github.com/markfulton/claude-antigravity-agents) |
| `oh-my-openagent` | 面向复杂代码库的低 token coding agent harness，围绕 Codex、OpenCode 等生态做上下文与编排优化。 | [GitHub](https://github.com/code-yeongyu/oh-my-openagent) |
| `Codex-X` | Codex 桌面/CLI 的本地配置控制面，覆盖 Provider、Auth、TOML、会话、Skills 与 MCP 管理。 | [GitHub](https://github.com/yynxxxxx/Codex-X) |
| `tau` | Hugging Face 组织下的极简终端 coding agent，也是可读的 agent harness 教学实现。 | [GitHub](https://github.com/huggingface/tau) |
| `codex-hygiene` | 面向 Codex Desktop 的上下文、工具表面、MCP / app / skill 可用性和长线程 replay 诊断 skill。 | [GitHub](https://github.com/sunflower-of-parchman/codex-hygiene) |
| `tabby` | 自托管、可本地部署的开源 AI 编码助手。 | [GitHub](https://github.com/TabbyML/tabby) |
| `zed` | 高性能、多人协作的代码编辑器，体现 AI 时代开发入口向编辑器本体回流。 | [GitHub](https://github.com/zed-industries/zed) |
| `orca` | 多 worktree 并行调度的 agent 开发环境，把多个 coding agent 收到同一工作台里。 | [GitHub](https://github.com/stablyai/orca) |

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
| `agent-toolkit-for-aws` | AWS 官方维护的 agent 插件、skills 与 MCP 接入工具包。 | [GitHub](https://github.com/aws/agent-toolkit-for-aws) |
| `agents` | 面向 Claude Code、Codex、Cursor 等多种 harness 的插件市场与技能分发仓库。 | [GitHub](https://github.com/wshobson/agents) |
| `nvidia-skills` | NVIDIA 官方验证的 agent skill 目录，面向 CUDA-X、蓝图与平台工具。 | [GitHub](https://github.com/NVIDIA/skills) |
| `SkillSpector` | 面向 agent skills 的安全扫描器，专查恶意模式、权限风险与 MCP 相关漏洞。 | [GitHub](https://github.com/NVIDIA/SkillSpector) |
| `strix` | 用 AI hacker agents 做应用漏洞发现、PoC 验证和 CI 安全门禁。 | [GitHub](https://github.com/usestrix/strix) |
| `ai-maestro` | 面向多终端、多机器、多 agent 协作的 AI agent 控制面与编排系统。 | [GitHub](https://github.com/23blocks-OS/ai-maestro) |
| `awesome-harness-engineering` | 汇总 agent harness 工程的上下文、工具、记忆、权限、验证与可观测性模式。 | [GitHub](https://github.com/ai-boost/awesome-harness-engineering) |
| `testsprite-cli` | 面向 coding agent 的测试验证 CLI，把失败证据打包成 agent 可处理的修复输入。 | [GitHub](https://github.com/TestSprite/testsprite-cli) |
| `superlog` | agentic observability 工作台，把 OpenTelemetry 数据、incident 分组和 agent 调查摘要接起来。 | [GitHub](https://github.com/superloglabs/superlog) |
| `VulnClaw` | 基于 LLM Agent、MCP 工具链和渗透 skill 的授权安全测试工作流。 | [GitHub](https://github.com/Unclecheng-li/VulnClaw) |
| `loop-engineering` | 面向 AI coding agent 的 loop 工程模式、脚手架和预算/审计 CLI。 | [GitHub](https://github.com/cobusgreyling/loop-engineering) |
| `security-audit-skill` | Cloudflare 开源的 coding-agent 安全审计 skill，强调多阶段发现、验证和结构化输出。 | [GitHub](https://github.com/cloudflare/security-audit-skill) |
| `self-learning-skills` | 面向 coding agent 的自学习元技能，把会话中验证过的黄金路径沉淀成可复用 skill / rule / memory。 | [GitHub](https://github.com/Kulaxyz/self-learning-skills) |
| `bumblebee` | Perplexity 开源的开发端点供应链清点工具，覆盖 MCP 配置、agent skills 和扩展暴露面。 | [GitHub](https://github.com/perplexityai/bumblebee) |
| `fable-soul` | 面向 Codex / Claude Code 的 agent 判断层规则包，把验证、根因和完成度纪律写成可加载 skill。 | [GitHub](https://github.com/akseolabs-seo/fable-soul) |
| `token-diet` | 面向 Claude Code、Codex、Cursor 等 coding agent 的 token 成本控制 skill。 | [GitHub](https://github.com/Kulaxyz/token-diet) |
| `ConferenceWatch` | 跟踪 AI/ML 会议 deadline、CFP、地点和录用率趋势的 agent skill。 | [GitHub](https://github.com/Zsun79/ConferenceWatch) |
| `agent-runtime` | Provider-neutral 的 agent runtime core，把 loop、工具调度、预算和消息类型抽成可复用内核。 | [GitHub](https://github.com/easylink-ai-open/agent-runtime) |
| `T3MP3ST` | 面向授权红队测试的多代理 offensive-security meta-harness，强调 scope、工具链和可复算声明。 | [GitHub](https://github.com/elder-plinius/T3MP3ST) |
| `lemma-platform` | 人类与 AI agents 共用的结构化 workspace，用 pod 承载表格、workflow、权限和审批。 | [GitHub](https://github.com/lemma-work/lemma-platform) |
| `tupper` | 本地 agent code-execution sandbox，提供 E2B-style TypeScript SDK、MCP server 和多后端隔离路线。 | [GitHub](https://github.com/lightbearco/tupper) |
| `system_prompts_leaks` | 收集 Claude、ChatGPT / Codex、Gemini、Copilot、Cursor 等产品系统提示词，用于研究 agent 工具边界与安全策略。 | [GitHub](https://github.com/asgeirtj/system_prompts_leaks) |
| `gastown` | 多 agent workspace manager，用 git-backed hooks、任务 ledger、handoff 和合并队列协调多个 coding agents。 | [GitHub](https://github.com/gastownhall/gastown) |
| `system-prompts-and-models-of-ai-tools` | 覆盖多款 AI 工具系统提示词、内部工具说明和模型线索的社区资料库，用于研究 agent 边界。 | [GitHub](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools) |
| `awesome-claude-code` | Claude Code 生态资源索引，收集 skills、subagents、status lines、插件、MCP 和工作流资料。 | [GitHub](https://github.com/hesreallyhim/awesome-claude-code) |
| `OpenOPC` | AI-native company 工作台，把角色招聘、任务分派、交接、组织记忆和 Office UI 串成多 agent 公司流程。 | [GitHub](https://github.com/HKUDS/OpenOPC) |
| `claude-code-merge-queue` | 本地 Claude Code 并行 worktree 合并队列，串行化 rebase、push、build 与 test。 | [GitHub](https://github.com/funador/claude-code-merge-queue) |
| `open-connector` | 面向 AI agents 的开源连接器网关，用 SDK、CLI、MCP、HTTP 和 OpenAPI 统一 SaaS action 与凭据边界。 | [GitHub](https://github.com/oomol-lab/open-connector) |
| `sim-use` | 让 AI agent 观察并操作 iOS Simulator 与 Android emulator/device 的移动端验证 CLI。 | [GitHub](https://github.com/lycorp-jp/sim-use) |
| `mcpsnoop` | MCP 透明代理调试器，捕获真实客户端与 server 之间的 JSON-RPC 工具调用流。 | [GitHub](https://github.com/kerlenton/mcpsnoop) |
| `reverse-flow-skill` | 面向 Codex / AI Agent 的本地 CTF 逆向工程流程 skill，覆盖样本分诊、静态分析、深度逆向和报告输出。 | [GitHub](https://github.com/lingbol088-spec/reverse-flow-skill) |
| `loopkit` | 可落盘的 `.claude/` harness 与 49 个小 skill，用 Plan-Act-Verify、hooks 和 verifier subagent 约束 coding agent。 | [GitHub](https://github.com/Archive228/loopkit) |
| `homerail` | 语音优先的本地 agent DAG runtime，用 CLI、Docker worker、scorecard 和 replay 管理可审计工作流。 | [GitHub](https://github.com/xiaotianfotos/homerail) |
| `OpenTag` | Slack-first 团队 agent gateway，把 Codex、Claude Code、OpenCode 等 runtime 接进线程、审批、记忆和审计流。 | [GitHub](https://github.com/linxidnju/OpenTag) |
| `eve` | Vercel 的 filesystem-first agent framework，用文件约定组织 instructions、tools、skills、channels 和 schedules。 | [GitHub](https://github.com/vercel/eve) |
| `loopy` | AI-agent loop library 与可安装 skill，把重复工作写成带反馈、度量和停止条件的流程。 | [GitHub](https://github.com/Forward-Future/loopy) |
| `fable-method` | 把 think / act / prove 写成可安装 skills 与 judge eval 的 agent 工作流方法论。 | [GitHub](https://github.com/Sahir619/fable-method) |
| `Cognitive-Core-Skills` | 面向 LLM / SLM / agents / world models 的认知能力 taxonomy、schema 和 159 张 skill cards。 | [GitHub](https://github.com/eli-labz/Cognitive-Core-Skills) |
| `contextvc` | Git-native agent 上下文控制面，用 `.context/` 渲染 AGENTS、CLAUDE、Cursor、Copilot、Gemini 等规则文件。 | [GitHub](https://github.com/HaochengLu/contextvc) |

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
| `open-knowledge` | AI-native Markdown 编辑器与 LLM Wiki，把本地知识库、MCP、skills 和 git 同步接入 agent 工作流。 | [GitHub](https://github.com/inkeep/open-knowledge) |
| `nanobot` | 轻量个人 AI agent kernel，整合 WebUI、聊天渠道、MCP、记忆、自动化和模型路由。 | [GitHub](https://github.com/HKUDS/nanobot) |
| `engram` | 面向 Claude Code / Codex 的本地学习记忆引擎，用 free recall、盲评和 FSRS 复习调度沉淀知识。 | [GitHub](https://github.com/nagisanzenin/engram) |
| `agent-chief` | 本地优先的 agent 注意力路由层，过滤空报告、批处理事件、委派任务并验证完成结果。 | [GitHub](https://github.com/SmileLikeYe/agent-chief) |
| `openwiki` | LangChain 的代码库 / 个人知识库 wiki CLI，把 agent 需要长期读取的上下文落盘并可由 CI 更新。 | [GitHub](https://github.com/langchain-ai/openwiki) |
| `brain0` | AI 写代码的本地黑盒审计层，把 commit、prompt、读取上下文、风险评分和 provenance 连接成决策图。 | [GitHub](https://github.com/Brain0-ai/brain0) |
| `exxperts` | 本地优先的 AI rooms 与审批式长期记忆工作台，把 room、memory、KB 和 artifacts 保存在本机。 | [GitHub](https://github.com/EXXETA/exxperts) |
| `ditto` | 从 Claude Code、Codex、Copilot CLI 本地日志中挖掘个人工作画像，生成 agent 可读 profile。 | [GitHub](https://github.com/ohad6k/ditto) |

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
| `MinerU` | 面向 LLM / agent 的复杂文档解析基础设施，强调把 PDF / Office 资料转成结构化 Markdown / JSON。 | [GitHub](https://github.com/opendatalab/MinerU) |
| `codeseek` | Rust 代码智能 CLI，为 coding agent 提供调用图、混合语义搜索和 MCP 工具。 | [GitHub](https://github.com/CodeBendKit/codeseek) |
| `ky-markdown-rebuilder` | Codex / Claude Code 文档重建 skill，把视觉复杂 PDF、PPT、长截图整理成按页对齐 Markdown。 | [GitHub](https://github.com/KyrieCheungYep/ky-markdown-rebuilder) |

### 前端、UI 与 Agent 交互层

| 项目 | 简介 | 链接 |
| --- | --- | --- |
| `awesome-design-md` | 收集 `DESIGN.md` 模板的设计约束索引仓库。 | [GitHub](https://github.com/VoltAgent/awesome-design-md) |
| `design-md` | Google Labs 推动的设计契约格式，把视觉系统写成 coding agent 可读取的文本规范。 | [GitHub](https://github.com/google-labs-code/design.md) |
| `open-design` | 面向开放设计流程和组件思路的项目。 | [GitHub](https://github.com/nexu-io/open-design) |
| `AionUi` | 偏 AI 应用界面的组件/模板方向。 | [GitHub](https://github.com/iOfficeAI/AionUi) |
| `UI-TARS-desktop` | 偏桌面 Agent UI 与可操作前端表面。 | [GitHub](https://github.com/bytedance/UI-TARS-desktop) |
| `OpenSandbox` | 为 Agent 提供可控执行环境与隔离层。 | [GitHub](https://github.com/alibaba/OpenSandbox) |
| `page-agent` | 页面级 agent 交互与操作路线。 | [GitHub](https://github.com/alibaba/page-agent) |
| `lightpanda-browser` | 为自动化与 Agent 场景设计的高性能浏览器内核路线。 | [GitHub](https://github.com/lightpanda-io/browser) |
| `openui` | 开源生成式 UI 原型工具，支持描述界面并导出到多种前端框架。 | [GitHub](https://github.com/wandb/openui) |
| `chatbot-ui` | 开源 AI 聊天前端骨架，适合做多模型、自托管聊天入口。 | [GitHub](https://github.com/mckaywrigley/chatbot-ui) |
| `stitch-mcp` | 把 Google Stitch 生成的 UI 设计接入本地开发与 coding agent 工作流的 CLI / MCP 桥接层。 | [GitHub](https://github.com/davideast/stitch-mcp) |
| `hermes-studio` | Hermes Agent 的桌面工作台、本地运行时与 Web 控制台组合，强调会话、任务与控制面。 | [GitHub](https://github.com/EKKOLearnAI/hermes-studio) |
| `ai-website-cloner-template` | 用 AI coding agent 复刻网站的 Next.js 工作流模板，强调设计 token 抽取与并行重建。 | [GitHub](https://github.com/JCodesMore/ai-website-cloner-template) |
| `cherry-studio` | 跨平台多模型 AI 桌面客户端，集成预置助手、文档处理与 MCP 能力。 | [GitHub](https://github.com/CherryHQ/cherry-studio) |
| `openpencil` | AI-native 矢量设计工具，把 prompt、agent team、Design-as-Code 与 MCP 接入同一画布。 | [GitHub](https://github.com/ZSeven-W/openpencil) |
| `GUI-Agents-Paper-List` | GUI agent 论文、基准、数据集和研究趋势的结构化索引。 | [GitHub](https://github.com/OSU-NLP-Group/GUI-Agents-Paper-List) |
| `Agent-S` | Simular AI 的 computer-use / GUI agent 框架，围绕 OSWorld 等桌面操作基准推进 Agent S3。 | [GitHub](https://github.com/simular-ai/Agent-S) |
| `hermex` | iPhone 原生 self-hosted agent 控制面，用手机管理 Hermes 会话、任务、skills 和 workspace。 | [GitHub](https://github.com/uzairansaruzi/hermex) |
| `peerd` | 浏览器原生 AI agent harness，用扩展、vault、actor agent 和 WASM sandbox 驱动真实网页任务。 | [GitHub](https://github.com/NotASithLord/peerd) |
| `ui-ux-pro-max-skill` | 面向 coding agent 的 UI/UX 设计 skill，把行业风格、设计系统、色彩、排版和交付检查结构化。 | [GitHub](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) |
| `gzh-design-skill` | 面向 AI agent 的微信公众号排版 skill，把 Markdown 转为可粘贴的内联 HTML 并提供主题与校验脚本。 | [GitHub](https://github.com/isjiamu/gzh-design-skill) |
| `guizang-material-illustration` | 面向中文内容生产的材质插画 skill，把文章、图表、教学材料和工作汇报转成带中文标签的解释图。 | [GitHub](https://github.com/op7418/guizang-material-illustration) |
| `Browser-BC` | 本地记录浏览器任务轨迹，并按站点 capability bucket 蒸馏成 Claude / Codex 可复用 skill。 | [GitHub](https://github.com/Einsia/Browser-BC) |

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
| `hyperframes` | 用 HTML/CSS 与可 seek 动画直接渲染视频的 agent 友好型开源框架。 | [GitHub](https://github.com/heygen-com/hyperframes) |
| `Open-Generative-AI` | 面向图像与视频生成的开源聚合工作台，覆盖多模型、桌面端与 Web 端。 | [GitHub](https://github.com/Anil-matcha/Open-Generative-AI) |
| `video-use` | 让 coding agent 驱动视频剪辑、字幕、调色与渲染检查的自动化工作流。 | [GitHub](https://github.com/browser-use/video-use) |
| `FluidVoice` | 面向 macOS 的本地离线语音转文字应用，强调设备端 AI 后处理。 | [GitHub](https://github.com/altic-dev/FluidVoice) |
| `lingbot-map` | 流式 3D 重建基础模型，把视频/传感器流转成可用空间表示。 | [GitHub](https://github.com/Robbyant/lingbot-map) |
| `claude-video` | `/watch` agent skill，用字幕、Whisper、关键帧和去重机制让 Claude / Codex 等工具理解视频内容。 | [GitHub](https://github.com/bradautomates/claude-video) |
| `claude-real-video` | 本地视频关键帧、去重、转写和 contact sheet 工具，让任意 LLM 可审计地读取视频内容。 | [GitHub](https://github.com/HUANGCHIHHUNGLeo/claude-real-video) |
| `motion-anything` | Agentic motion layer，用自然语言生成和编辑页面动效、launch video，并导出 CSS、React、Lottie、MP4、GIF。 | [GitHub](https://github.com/nexu-io/motion-anything) |
| `FableCut` | 浏览器非线性视频编辑器，把时间线暴露为 JSON、REST 和 MCP，方便 agent 直接剪辑。 | [GitHub](https://github.com/ronak-create/FableCut) |
| `video-production-skills` | AI 视频制作 skill 集合，覆盖动效导演、参考视频复刻、暗色 SaaS 短片和片头包装。 | [GitHub](https://github.com/Pluviobyte/video-production-skills) |
| `pixel2motion` | Codex / Claude logo 动效 skill，把 raster logo 转成 SVG、HTML motion demo、GIF / video 预览和 QA 证据。 | [GitHub](https://github.com/nolangz/pixel2motion) |
| `lapian-notes` | 本地拉片笔记工具，把影片抽帧、字幕、AI 分析包、剧情泳道和结构树接成可编辑影视研究工作流。 | [GitHub](https://github.com/bkingfilm/lapian-notes) |
| `watch-skill` | 本地优先的视频理解与自验证层，让 agent 读取视频、录屏、会议并引用时间戳证据。 | [GitHub](https://github.com/oxbshw/watch-skill) |

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
| `AgentsMeetRL` | 聚焦用强化学习训练 LLM agents 的项目索引与 Claude Code skill，覆盖奖励、环境、工具调用和 GUI agent。 | [GitHub](https://github.com/thinkwee/AgentsMeetRL) |
| `local-llm` | 本地运行高端 LLM 的硬件、GPU 互联、vLLM runner 和语音转文字实践记录。 | [GitHub](https://github.com/jamesob/local-llm) |
| `Talos` | 将本机 Ollama / GPU 作为 Talos network worker，接收开放模型推理任务并回传在线与使用状态。 | [GitHub](https://github.com/jmerelnyc/Talos) |
| `Hy3` | 腾讯混元 295B MoE / 21B active 开放权重模型，强调 256K 上下文、工具调用和 agentic 任务能力。 | [GitHub](https://github.com/Tencent-Hunyuan/Hy3) |
| `coreai-models` | Apple 的 Core AI 模型导出、Python primitives、Swift runtime utilities 和 agent skills 仓库。 | [GitHub](https://github.com/apple/coreai-models) |

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
| `worldmonitor` | 面向全球情报与基础设施监测的 AI 工作台，强调多源新闻聚合与态势感知。 | [GitHub](https://github.com/koala73/worldmonitor) |
| `ai-berkshire` | 把价值投资研究拆成技能与多 Agent 流程的领域化投研框架。 | [GitHub](https://github.com/xbtlin/ai-berkshire) |
| `open-science` | 面向科研发现的开源 AI 工作台愿景项目，强调模型无关、本地可部署和可审计 provenance。 | [GitHub](https://github.com/aipoch/open-science) |
| `CSSwitch` | Claude Science 的第三方模型接入切换工具，用本地代理连接 DeepSeek、Qwen、GLM、Kimi 等端点。 | [GitHub](https://github.com/SuperJJ007/CSSwitch) |
| `meetily` | 隐私优先的本地 AI 会议助手，覆盖实时转写、说话人分离、Ollama 摘要和自托管会议记录。 | [GitHub](https://github.com/Zackriya-Solutions/meetily) |
| `Vibe-Research` | 个人 AI 投研看板，整合 A 股/美股/港股数据、资讯、持仓、研报和本地 AI 分析入口。 | [GitHub](https://github.com/simonlin1212/Vibe-Research) |
| `dashiAI-ppt-skill` | 中文 AI PPT skill，生成可浏览器编辑的 HTML deck，并导出 PDF / 可编辑 PPTX。 | [GitHub](https://github.com/chuspeeism/dashiAI-ppt-skill) |

## 完整索引与每日热点

- 全量项目目录：[`projects/`](./projects/)
- 最近日报：
  - [`2026-07-13`](./daily/2026-07-13/ai-hotspots.md)
  - [`2026-07-12`](./daily/2026-07-12/ai-hotspots.md)
  - [`2026-07-11`](./daily/2026-07-11/ai-hotspots.md)
  - [`2026-07-10`](./daily/2026-07-10/ai-hotspots.md)
  - [`2026-07-09`](./daily/2026-07-09/ai-hotspots.md)
  - [`2026-07-08`](./daily/2026-07-08/ai-hotspots.md)
  - [`2026-07-07`](./daily/2026-07-07/ai-hotspots.md)
  - [`2026-07-06`](./daily/2026-07-06/ai-hotspots.md)
  - [`2026-07-05`](./daily/2026-07-05/ai-hotspots.md)
  - [`2026-07-04`](./daily/2026-07-04/ai-hotspots.md)
  - [`2026-07-03`](./daily/2026-07-03/ai-hotspots.md)
  - [`2026-07-02`](./daily/2026-07-02/ai-hotspots.md)
  - [`2026-07-01`](./daily/2026-07-01/ai-hotspots.md)
  - [`2026-06-30`](./daily/2026-06-30/ai-hotspots.md)
  - [`2026-06-29`](./daily/2026-06-29/ai-hotspots.md)
  - [`2026-06-28`](./daily/2026-06-28/ai-hotspots.md)
  - [`2026-06-27`](./daily/2026-06-27/ai-hotspots.md)
  - [`2026-06-26`](./daily/2026-06-26/ai-hotspots.md)

如果你要找的是某个具体项目，而不是看分类，直接在 [`projects/`](./projects/) 中按名称查找会更快。

## 当前状态

- 状态：持续日更中。
- 最新更新：`2026-07-13`。
- 当前项目总数：`350`。
- 最近新增项目：`lapian-notes`、`exxperts`、`ditto`、`fable-method`、`Cognitive-Core-Skills`、`watch-skill`、`contextvc`、`codex-hygiene`。
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
