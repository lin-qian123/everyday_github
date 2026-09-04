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
  - [AI 学习与教育资源](#ai-学习与教育资源)
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

- 最新日报：[`daily/2026-09-05/ai-hotspots.md`](./daily/2026-09-05/ai-hotspots.md)
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
| `portless` | 用稳定 `.localhost` 与 worktree 子域名替代本地端口，方便人和 agents 复用开发入口；本地 CA、sudo 服务与共享模式须审计。 | [GitHub](https://github.com/vercel-labs/portless) |
| `nodeterm` | 把真实终端、coding-agent sessions、画布、Kanban、Git 与远程监督合并；tmux 不是隔离，当前许可证为 BUSL-1.1。 | [GitHub](https://github.com/eneskirca/nodeterm) |
| `atlas` | 面向 coding agents 的 source-control 桌面工作台，将共享记忆、会话、工具调用与 Git checkpoint 关联；本地默认和 secret scrub 仍需独立验证。 | [GitHub](https://github.com/pacifio/atlas) |
| `superset` | 以独立 worktree、终端、diff、自动化和远端 host 编排多路 CLI agents；worktree 不是 OS 隔离，ELv2 权利边界须审查。 | [GitHub](https://github.com/superset-sh/superset) |
| `openclaude` | 跨云端 API、本地模型和多类工具的 coding-agent CLI；对话 fork 不是文件隔离，派生代码与 MIT 修改部分的许可边界须分别审查。 | [GitHub](https://github.com/Gitlawb/openclaude) |
| `maka` | Apache 孵化中的 local-first agent 工作区，把桌面、CLI、工具审批和评测统一到可恢复的执行记录；sandbox、网络和日志仍需独立治理。 | [GitHub](https://github.com/apache/maka) |
| `claudish-to-english` | Claude Code 显示层改写插件，默认以本地 Ollama 将助手输出转成更直白的表述；云端 provider 会产生额外数据外发。 | [GitHub](https://github.com/Leutenegger/claudish-to-english) |
| `agent-link` | 以私有 Git 分支或 relay 在跨机 coding agents 间传递加密协作消息；仍须防范元数据、明文 transcript 与未可信输入。 | [GitHub](https://github.com/Riccardo8888/agent-link) |
| `ai-smart-contract-auditor` | 面向 Claude Code 的智能合约审计技能/MCP 组合；PoC、基准与链上动作必须独立人工复核。 | [GitHub](https://github.com/iktok90-design/ai-smart-contract-auditor) |
| `desktop-harness` | macOS 上以 Accessibility 树优先的本地 GUI 控制 CLI；高权限自动化必须最小授权。 | [GitHub](https://github.com/xfreeze2/desktop-harness) |
| `pi-from-scratch` | 用 600 行 TypeScript 和可回放 Trace 拆解最小 coding agent；真实工具调用需在隔离工作区审查。 | [GitHub](https://github.com/SaladDay/pi-from-scratch) |
| `hud-mode` | 面向 Claude Code、Codex、OpenCode 的紧凑终端 HUD，以事件流呈现状态、token 与可排队交互；会改动用户级配置。 | [GitHub](https://github.com/adrida/hud-mode) |
| `Fuxi` | 单二进制终端 coding agent，提供多模型路由、MCP、持久会话与工具调用；需控制凭据、费用与自动更新。 | [GitHub](https://github.com/fuxicodex/Fuxi) |
| `diri` | macOS 原生多 agent 编排器，用 worktree、持久 PTY、状态识别和远端 host 管理并行会话。 | [GitHub](https://github.com/cristicretu/diri) |
| `codex-ds-sub-agents` | 以本地任务文件、原子领取和回执让 Codex Desktop 试用 DeepSeek 子 agent 的第三方集成。 | [GitHub](https://github.com/wongchisum/codex-ds-sub-agents) |
| `Tigriden` | 专为监督终端 coding agents 设计的轻量 macOS IDE，合并会话、文件树、编辑器与查看器。 | [GitHub](https://github.com/Sompote/Tigriden) |
| `hybrid-cli-ai` | 在 Ollama 与 Groq 间切换、默认先预览再执行的跨平台自然语言终端助手。 | [GitHub](https://github.com/HereIsMuhammad/hybrid-cli-ai) |
| `proxybaby` | 面向 AI/SSE/ACP 会话的跨平台代理调试器；仅可在授权抓包范围内使用。 | [GitHub](https://github.com/imcuttle/proxybaby) |
| `LiteCoder` | 终端优先 coding agent，结合持久会话、项目记忆、权限、trace、MCP 与协作。 | [GitHub](https://github.com/ikooky/litecoder) |
| `llm-endpoint-doctor` | 探测 LLM 中继的协议、SSE 与工具循环能力，并生成可复用诊断报告。 | [GitHub](https://github.com/xinlizhu/llm-endpoint-doctor) |
| `ponytail-improved` | 用 skills 与 hook 让 coding agent 先复用、后新增的“反过度工程”规则包。 | [GitHub](https://github.com/0xwilliamortiz/ponytail-improved) |
| `succubus` | 为同仓库并行 coding agents 提供共享任务板、问题区与带 TTL 的文件租约。 | [GitHub](https://github.com/enowdev/succubus) |
| `openclaude-improved` | 主打跨环境、可替换工具接入的开源 agent 项目。 | [GitHub](https://github.com/0xwilliamortiz/openclaude-improved) |
| `cursor-bridge` | 连接 Claude Code 与 Cursor 订阅工作流的单 Rust 二进制桥接工具。 | [GitHub](https://github.com/hkc5/cursor-bridge) |
| `ctx-diet` | Claude Code 的 PostToolUse hook，在工具输出入模前压缩冗余内容以控制长会话 token 成本。 | [GitHub](https://github.com/illuwa/ctx-diet) |
| `VinvAI` | 以真实运行 trace、代码图谱和独立验收验证 coding agent 修复的本地工具。 | [GitHub](https://github.com/VinvAI/VinvAI) |
| `agent-notify` | macOS 上给并行终端 agent 会话使用的自清理通知注意力队列。 | [GitHub](https://github.com/yauyauyauhen/agent-notify) |
| `AgentBar` | 统一显示 coding agent 状态、并可处理 Claude Code 权限请求的 macOS 菜单栏应用。 | [GitHub](https://github.com/michalstrnadel/AgentBar) |
| `sigbound` | 用 Git 并行运行 coding agents，并以构建/测试作为自动合并门槛。 | [GitHub](https://github.com/surya-koritala/sigbound) |
| `aidd` | 本地优先的跨 CLI AI coding agent 监督控制面。 | [GitHub](https://github.com/NomadicDaddy/aidd) |
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
| `tura` | 本地开源 coding agent，强调用更少 turn / token 完成长时程工程任务并保留 benchmark 证据。 | [GitHub](https://github.com/Tura-AI/tura) |
| `grok-build` | xAI/SpaceXAI 开源的终端 coding agent harness，支持 TUI、headless/CI 与 ACP。 | [GitHub](https://github.com/xai-org/grok-build) |
| `clodex-ide` | 本地优先、强调受控执行和用户审查的开源 agentic IDE。 | [GitHub](https://github.com/mereyabdenbekuly-ctrl/clodex-ide) |
| `klaatcode` | KlaatAI 的终端原生 coding agent，用服务端模型路由和代码图谱降低长任务成本。 | [GitHub](https://github.com/KlaatAI/klaatcode) |
| `codex-router` | Codex 外部模型路由器，把 Kimi、DeepSeek 等 provider 接入 Codex model picker。 | [GitHub](https://github.com/duolahypercho/codex-router) |
| `ego-lite` | 为外部 coding agent 提供独立 browser Space 的 macOS 浏览器；迁移登录态前须隔离 profile、最小权限并审计网络数据流。 | [GitHub](https://github.com/citrolabs/ego-lite) |
| `munder-difflin` | 以真实终端 CLI、文件型消息/记忆与人工闸门编排本地多 agent 的桌面 harness；不是沙箱，须审计权限和许可证。 | [GitHub](https://github.com/chaitanyagiri/munder-difflin) |

### Agent 框架与技能生态

| 项目 | 简介 | 链接 |
| --- | --- | --- |
| `agentdesktop` | Solo.io 的桌面 AI 工具治理层，清点并管理 harness、MCP、skills、sandbox 意图、身份和 gateway 凭据；client label 不是进程级证明。 | [GitHub](https://github.com/agentdesktop-dev/agentdesktop) |
| `loopx` | 跨 Codex、Claude Code 等 harness 保存 goal、gate、evidence、quota 与 handoff 的长时程控制层；不是 OS sandbox 或自主生产控制器。 | [GitHub](https://github.com/huangruiteng/loopx) |
| `text-to-cad` | CAD、DXF、URDF / SRDF / SDF、DfAM、G-code 与打印交接的 agent skills；生成与 watertight 不能替代工程审核和物理安全。 | [GitHub](https://github.com/earthtojake/text-to-cad) |
| `humanizer` | 用 35 类可审阅写作规则减少 AI 腔的跨宿主 skill；自然度不能替代事实、原创、语义保持和 AI 辅助披露审核。 | [GitHub](https://github.com/blader/humanizer) |
| `skills-manager` | 以中央库、CLI、Git 备份和多设备同步管理 53 个上游列出的 agent/tool skills；跨宿主写入与后台 push 是高权限边界。 | [GitHub](https://github.com/xingkongliang/skills-manager) |
| `ui-skills` | 通过 Web、CLI 与 MCP 分发设计工程 skills；规则不能替代品牌、无障碍、视觉回归和用户验证。 | [GitHub](https://github.com/ibelick/ui-skills) |
| `skills-hub` | 以中央库和 symlink/copy 管理 47 个上游列出的 coding-tool skills；自动更新与批量同步会扩大供应链风险。 | [GitHub](https://github.com/qufei1993/skills-hub) |
| `agent-browser` | 面向 agents 的 Rust 浏览器自动化 CLI，提供 accessibility refs、CDP、MCP 与 experimental WebMCP；页面工具与后果性动作须独立授权。 | [GitHub](https://github.com/vercel-labs/agent-browser) |
| `arcbox` | 在 macOS 上以独立内核 Firecracker microVM 运行 agents 与不可信代码；需 M3+/macOS 15+，网络、凭据和控制面仍须对抗验证。 | [GitHub](https://github.com/arcboxlabs/arcbox) |
| `OpenShell` | NVIDIA 的 agent 隔离运行时，在进程外用 gateway、sandbox、策略与推理路由约束文件、网络和凭据；真实隔离强度须按后端对抗验证。 | [GitHub](https://github.com/NVIDIA/OpenShell) |
| `reverse-skill` | 面向授权逆向、CTF、取证和渗透测试的 agent 技能路由包，以 scope、场景 playbook 和证据链约束执行；不能替代书面授权与隔离靶场。 | [GitHub](https://github.com/zhaoxuya520/reverse-skill) |
| `paperclip` | 用组织图、目标、任务、心跳、预算和日志协调外部 agents 的控制面；预算与审计记录不是 OS sandbox，外部动作仍需人工闸门。 | [GitHub](https://github.com/paperclipai/paperclip) |
| `archify` | 将代码库或系统描述转换为带 schema、验证和多格式导出的交互式系统图；图形正确性仍需回到源码和运行时核验。 | [GitHub](https://github.com/tt-a1i/archify) |
| `garden-skills` | 面向 Claude Code、Cursor、Codex 等宿主的网页设计、检索、图像和文章生成技能集合；skill 不是沙箱或事实核验器。 | [GitHub](https://github.com/ConardLi/garden-skills) |
| `netwalk` | 用代码级只读命令策略与范围限制辅助 agent 做已授权网络巡检；配置、扫描与报告仍须最小权限和人工复核。 | [GitHub](https://github.com/ripmilla/netwalk) |
| `GamePhanes` | Godot 游戏 coding agent 的构建、试玩、测试与修复环境，借助外置 harness 做确定性断言；临时副本不等同于 OS 级隔离。 | [GitHub](https://github.com/GamePhanes/GamePhanes) |
| `obsidian-skills` | 让 Claude Code、Codex、OpenCode 等 agent 按技能规范处理 Obsidian Markdown、Bases、Canvas 与 CLI；真实 vault 仍需最小写入权限和可回滚审查。 | [GitHub](https://github.com/kepano/obsidian-skills) |
| `sprix-sage-router` | 面向开放 A2A 网络的多 agent 路由研究预览，比较独立执行、协作与交接，并显式约束权限、预算、任务 DAG 与上下文转移。 | [GitHub](https://github.com/wang2122/sprix-sage-router) |
| `openwork` | 跨 agent 复用 skills、MCP 与企业连接的桌面工作区/远程 MCP；接入业务系统前应单独核验 OAuth、执行权限与许可。 | [GitHub](https://github.com/different-ai/openwork) |
| `HERO-Anti-OverDefense` | 用四类模式约束 agent 过度防御；不覆盖真实安全和用户指定验证。 | [GitHub](https://github.com/wanshuiyin/HERO-Anti-OverDefense) |
| `toolpermit` | 给本地 MCP `stdio` 调用加 YAML 策略、一次性审批与脱敏审计；不是 OS sandbox。 | [GitHub](https://github.com/sunhao123456sun-svg/toolpermit) |
| `constitution` | 可固定版本的 coding-agent 工作原则；应在下游审阅合并，不能取代权限或沙箱。 | [GitHub](https://github.com/kenn-io/constitution) |
| `inside-coding-agents` | 将 coding-agent 机制、来源证据与可重放实验组织成双语教材和图谱。 | [GitHub](https://github.com/vpromise/inside-coding-agents) |
| `hermes-starter-profile` | Hermes 的最小权限入门 profile，默认关闭终端、文件、浏览器控制和自动化；仍不是 OS 沙箱。 | [GitHub](https://github.com/teknium1/hermes-starter-profile) |
| `KADATH` | 以可锁定基准、冻结证据和种群选择探索 agent 策略的进化 runtime；须约束模型成本、容器和外部权限。 | [GitHub](https://github.com/i3T4AN/KADATH) |
| `unreal-mcp` | 用 MCP 对 UE 5.6/5.8 Blueprint 做分级读取、增量索引和可撤销编辑的本地 bridge。 | [GitHub](https://github.com/ZiggyMar/unreal-mcp) |
| `remove-chinese-ai-tics` | 将中文模型化口癖审计和改写封装为 agent skill；仍需人工核验语义、事实和声口。 | [GitHub](https://github.com/AAzzAAzzAAzzAA/remove-chinese-ai-tics) |
| `macos-disk-cleanup` | 为 coding agent 提供唯读扫描与三级删除风险规则的 macOS 磁盘清理 skill；任何清理动作须人工核验与备份。 | [GitHub](https://github.com/himynameisben/macos-disk-cleanup) |
| `human-writing` | 将中文写作的材料门槛、段落推进与修订硬规则打包为 agent skill；不能替代事实、版权与作者审核。 | [GitHub](https://github.com/KKKKhazix/human-writing) |
| `portable-agent-skills` | 三个跨宿主 skills，覆盖证据型研究、部署前执行 gate 与安装前静态安全审查。 | [GitHub](https://github.com/ch1109/portable-agent-skills) |
| `LongHorizon-Harness` | 用管理、执行、独立审计三角色保存长时程 agent 的已验证状态；外接 MCP 与真实权限仍须另行约束。 | [GitHub](https://github.com/AMAP-ML/LongHorizon-Harness) |
| `ironcode` | 面向 Claude Code/Codex 的工程质量 gate skill，要求用实际测试、构建或运行证据支持完成声明。 | [GitHub](https://github.com/djfksjd/ironcode) |
| `CUSTODY-framework` | 面向组织内自治 agent 的 containment 控制框架，用 Level/Mandate/Reach 盘点权限与可达性。 | [GitHub](https://github.com/malwarejake/CUSTODY-framework) |
| `phoenix` | Hermes Agent 的第三方治理插件，组合模型路由、熔断、自愈、长任务守护与复核；需审阅非商业许可证和 provider 数据边界。 | [GitHub](https://github.com/xyaz1313/phoenix) |
| `codex-agent-team` | 为 Codex 选择最小协作拓扑、验证方式与人工闸门的第三方 skill 及校验脚本。 | [GitHub](https://github.com/youngfor-shoot/codex-agent-team) |
| `celln` | 用 microVM、只读借用工具与 agent/tool 执行通道隔离来运行 agent 生成程序的早期工具。 | [GitHub](https://github.com/sympozium-ai/celln) |
| `impeccable-lite` | 面向 coding agent 的单文件前端设计 judgment skill，刻意不携带插件和运行时 machinery。 | [GitHub](https://github.com/ilindaniel/impeccable-lite) |
| `architect-agent` | 研究型 BPMN 到工具、代码与测试生成工作流，强调确定性流程与评测。 | [GitHub](https://github.com/Commonwealth-Bank-of-Australia/architect-agent) |
| `doubt` | 用可定位的支持、反驳、限定与缺失证据生成可审阅的交互式图谱。 | [GitHub](https://github.com/alsoleg89/doubt) |
| `empathy` | 约束 agent 在对人发布前披露身份、尊重注意力，并判断是否应发送。 | [GitHub](https://github.com/danielroe/empathy) |
| `video-to-skill` | 将有权访问的视频或课程转为带时间戳证据、可安装的 Claude Code/Codex skill。 | [GitHub](https://github.com/Lum1104/video-to-skill) |
| `skill-audit-router` | 盘点可加载 skills、重复/遮蔽项与难路由描述，并支持重测改进。 | [GitHub](https://github.com/rushindrasinha/skill-audit-router) |
| `letsfinddomain-skill` | 为 Codex/Claude Code/Cursor 生成域名候选、批量检查可用性与续费价的只读 skill。 | [GitHub](https://github.com/meepo-it/letsfinddomain-skill) |
| `ai-design-skills` | 将落地页结构、视觉 token 与动效约束写成 coding agent 可读取的设计 skill 集。 | [GitHub](https://github.com/elayadesign/ai-design-skills) |
| `lit-review-skill` | 为 Claude/Codex 等 agent 提供文献检索、书目核验与主张支持度审计。 | [GitHub](https://github.com/Zachariah9420/lit-review-skill) |
| `frieren-dast-ai` | 将 MITM 代理、规则扫描、多 agent 检查与仪表板组合的授权 DAST 工具。 | [GitHub](https://github.com/knowbe4/frieren-dast-ai) |
| `oil-tone` | 面向中英写作的 agent skill，以明确规则和轻量 lint 压制无信息文案。 | [GitHub](https://github.com/oil-oil/oil-tone) |
| `deer-workflow` | 将 TypeScript 编排与可替换 agent runtime 解耦的动态工作流 runtime。 | [GitHub](https://github.com/deerwork-ai/deer-workflow) |
| `llmwiki-harness` | 面向知识组织与 LLM 任务循环的早期 harness 观察项。 | [GitHub](https://github.com/cookyman74/llmwiki-harness) |
| `crucible-agent-skill` | 以减少冗余和收缩 diff 为目标的 coding agent skill。 | [GitHub](https://github.com/ryanelian/crucible-agent-skill) |
| `Verchestra` | 用策略门、只读探针、签名证据与人工审查组织可移植 AI 软件交付的早期 harness。 | [GitHub](https://github.com/accd/verchestra) |
| `capybara` | 本地终端 trace debugger，接收 OTLP/会话记录来定位 agent 工具失败、漂移、循环和成本尖峰。 | [GitHub](https://github.com/tonquoc0407/capybara) |
| `openhub` | 终端内发现、安装并导出 AI 工具、MCP 与 agent skills 的本地目录中心。 | [GitHub](https://github.com/24KaratAu/openhub) |
| `AxisAgentic` | 可扩展的长时程 agent runtime 与评测框架，保留状态忠实 trace 和可重放产物。 | [GitHub](https://github.com/XYZ-AI-Lab/AxisAgentic) |
| `handoff-skill` | 将 AI 对话与任务状态整理为结构化交接文档的 Claude skill。 | [GitHub](https://github.com/ToolMonsters/handoff-skill) |
| `OptiMCP` | 用确定性规则校验 agent 数学与逻辑输出的 MCP。 | [GitHub](https://github.com/ProfessionalQwerty/OptiMCP) |
| `minos` | 为 coding agent 编写的硬规则集合。 | [GitHub](https://github.com/FlavioZanoni/minos) |
| `content-core` | 组合 LLM、RAG、MCP、workflow 与评测的 AI 平台内核。 | [GitHub](https://github.com/sai-chaithanya-navuluri/content-core) |
| `Baker-Street` | 用多认知视角寻找论证冲突与盲区的 Claude Code 框架。 | [GitHub](https://github.com/tywinlu1988/Baker-Street) |
| `checkup` | 检查链接、依赖、CI 与文档衰退的 Claude Code skill。 | [GitHub](https://github.com/tokyubevoxelverse/checkup) |
| `repro` | 将偶发失败收敛为最小复现与回归测试的 Claude Code skill。 | [GitHub](https://github.com/tokyubevoxelverse/repro) |
| `skeptic` | 用对抗性测试审查 PR 声明的 Claude Code skill。 | [GitHub](https://github.com/tokyubevoxelverse/skeptic) |
| `fence` | 用 Git 历史调查代码删除风险的 Claude Code skill。 | [GitHub](https://github.com/tokyubevoxelverse/fence) |
| `bisect` | 驱动隔离 `git bisect` 定位回归提交的 Claude Code skill。 | [GitHub](https://github.com/tokyubevoxelverse/bisect) |
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
| `awesome-mcp-servers` | MCP server 目录入口，收集本地、云端、数据库、浏览器、API 等工具接入能力。 | [GitHub](https://github.com/punkpeye/awesome-mcp-servers) |
| `reverse-flow-skill` | 面向 Codex / AI Agent 的本地 CTF 逆向工程流程 skill，覆盖样本分诊、静态分析、深度逆向和报告输出。 | [GitHub](https://github.com/lingbol088-spec/reverse-flow-skill) |
| `loopkit` | 可落盘的 `.claude/` harness 与 49 个小 skill，用 Plan-Act-Verify、hooks 和 verifier subagent 约束 coding agent。 | [GitHub](https://github.com/Archive228/loopkit) |
| `homerail` | 语音优先的本地 agent DAG runtime，用 CLI、Docker worker、scorecard 和 replay 管理可审计工作流。 | [GitHub](https://github.com/xiaotianfotos/homerail) |
| `OpenTag` | Slack-first 团队 agent gateway，把 Codex、Claude Code、OpenCode 等 runtime 接进线程、审批、记忆和审计流。 | [GitHub](https://github.com/linxidnju/OpenTag) |
| `eve` | Vercel 的 filesystem-first agent framework，用文件约定组织 instructions、tools、skills、channels 和 schedules。 | [GitHub](https://github.com/vercel/eve) |
| `loopy` | AI-agent loop library 与可安装 skill，把重复工作写成带反馈、度量和停止条件的流程。 | [GitHub](https://github.com/Forward-Future/loopy) |
| `fable-method` | 把 think / act / prove 写成可安装 skills 与 judge eval 的 agent 工作流方法论。 | [GitHub](https://github.com/Sahir619/fable-method) |
| `Cognitive-Core-Skills` | 面向 LLM / SLM / agents / world models 的认知能力 taxonomy、schema 和 159 张 skill cards。 | [GitHub](https://github.com/eli-labz/Cognitive-Core-Skills) |
| `contextvc` | Git-native agent 上下文控制面，用 `.context/` 渲染 AGENTS、CLAUDE、Cursor、Copilot、Gemini 等规则文件。 | [GitHub](https://github.com/HaochengLu/contextvc) |
| `lobehub` | 多 agent control plane，把 agent 创建、调度、协作、汇报和 7x24 运行组织到同一工作台。 | [GitHub](https://github.com/lobehub/lobehub) |
| `daytona` | 面向 AI-generated code 的安全弹性 sandbox / runtime 基础设施，公开仓库已声明停止维护。 | [GitHub](https://github.com/daytonaio/daytona) |
| `CowAgent` | 多渠道个人 AI agent harness，整合任务规划、记忆、知识库、skills、MCP 和多模型接入。 | [GitHub](https://github.com/zhayujie/CowAgent) |
| `learn-harness-engineering` | Harness engineering 项目式课程，覆盖环境、状态、验证、控制机制与 loop engineering。 | [GitHub](https://github.com/walkinglabs/learn-harness-engineering) |
| `langflow` | 可视化 agent/workflow builder，可把流程部署为 API 或 MCP server。 | [GitHub](https://github.com/langflow-ai/langflow) |
| `semantic-kernel` | Microsoft 的模型无关 agent SDK，正向 Microsoft Agent Framework 迁移。 | [GitHub](https://github.com/microsoft/semantic-kernel) |
| `awesome-llm-apps` | 可运行的 AI agents、agent skills 与 RAG 应用模板集合。 | [GitHub](https://github.com/Shubhamsaboo/awesome-llm-apps) |
| `composio` | 面向 AI agents 的工具接入、认证、per-user session 与 sandbox 网关。 | [GitHub](https://github.com/ComposioHQ/composio) |
| `fastmcp` | 用 Python 快速构建 MCP servers 和 clients 的框架。 | [GitHub](https://github.com/PrefectHQ/fastmcp) |
| `mastra` | 面向 TypeScript 的 agent 应用框架，覆盖 workflows、memory、MCP、evals 与 observability。 | [GitHub](https://github.com/mastra-ai/mastra) |
| `awesome-copilot` | GitHub Copilot 的 agents、instructions、skills、hooks、plugins 与 workflows 资源目录。 | [GitHub](https://github.com/github/awesome-copilot) |
| `fable5-mode` | Claude Code skill 与 guard hooks，用 plan gate、验收命令和自检约束 coding agent 工作纪律。 | [GitHub](https://github.com/cozytab/fable5-mode) |
| `bridgebench` | 面向 vibe coding 模型的可复核 arena benchmark，用盲评、journal 和 Elo 记录工程任务表现。 | [GitHub](https://github.com/bridge-mind/bridgebench) |
| `Flawless` | AI-native SRE control plane，把告警、证据、审批、修复预演和恢复验证接成 AgenticOps 闭环。 | [GitHub](https://github.com/William-Lu-stack/Flawless) |
| `mindwalk` | 本地回放 Claude Code / Codex session log，用代码地图复盘 agent 搜索、阅读和编辑轨迹。 | [GitHub](https://github.com/cosmtrek/mindwalk) |
| `clawk` | 给 coding agent 分配 disposable Linux VM，用虚拟机边界、网络 allow-list 和可销毁环境隔离执行。 | [GitHub](https://github.com/clawkwork/clawk) |
| `pilotfish` | Claude Code 多模型编排配置层，让强模型规划、便宜模型执行，并用 fresh-context verifier 控制质量。 | [GitHub](https://github.com/Nanako0129/pilotfish) |
| `coder_eval` | 用 YAML 任务、sandbox、连续评分和 CI 验证 coding agents 与 agent skills 的评测框架。 | [GitHub](https://github.com/UiPath/coder_eval) |
| `waku-agent` | 可读的本地个人 agent harness，覆盖 loop、memory、eval 和 dashboard。 | [GitHub](https://github.com/ShenSeanChen/waku-agent) |
| `managed-agents` | 本地优先的 agent runtime/control plane，覆盖 session、审批、sandbox、凭据、审计和 MCP。 | [GitHub](https://github.com/sandbaseai/managed-agents) |
| `harness-engineering` | Ryan Lopopolo 的 agent harness 工程资料库，把上下文、工具、权限和验证组织成可复用环境。 | [GitHub](https://github.com/lopopolo/harness-engineering) |
| `agentsmith` | 模型无关的 agent operating harness，用 core + profile 组合 Codex、Claude Code、Gemini 等规则文件。 | [GitHub](https://github.com/PromptPartner/agentsmith) |
| `fastctx` | Rust MCP runtime，把仓库读取、搜索、替换和命令执行封装成结构化 agent 工具。 | [GitHub](https://github.com/yc-duan/fastctx) |
| `machine-genome` | 面向模型、agent、harness、数据集和产物的开放身份与 provenance 协议。 | [GitHub](https://github.com/paxlabs-inc/machine-genome) |
| `software-periodic-table` | 把常见业务软件拆成 115 个可复用元素，供 LLM coding agent 检索与组合。 | [GitHub](https://github.com/NullLabTests/software-periodic-table) |
| `open-kritt` | 开源 agentic security scanner，用多 agent workflow 查找、验证并构建漏洞 PoC。 | [GitHub](https://github.com/Kritt-ai/open-kritt) |
| `fabrica` | 基于 Kubernetes、Kata Containers 和 Cloud Hypervisor 的 agent microVM sandbox 平台。 | [GitHub](https://github.com/mitkox/fabrica) |
| `graphkit` | Claude Code graph engineering skill，用 executor、supervisor、ledger 拆解长时程 coding 任务。 | [GitHub](https://github.com/levi-qiao/graphkit) |

### 记忆层与个人 AI 基础设施

| 项目 | 简介 | 链接 |
| --- | --- | --- |
| `OB1` | 以数据库、向量检索、MCP / gateway、导入 recipe 与治理 schema 让多种 AI 共享个人记忆；当前为 FSL-1.1-MIT，RLS、来源和删除须审计。 | [GitHub](https://github.com/NateBJones-Projects/OB1) |
| `claude-obsidian` | 将来源、主张、链接笔记与 Obsidian vault 组织成 local-first 知识系统；模型、检索和批量写入仍须审计。 | [GitHub](https://github.com/AgriciDaniel/claude-obsidian) |
| `Evaan_Personal_Intelligence_Engine` | 用小型本地模型、prompt、规则式语气与 JSON 状态实现陪伴式聊天示例；明文记忆、心理陪伴边界与许可证须先审计。 | [GitHub](https://github.com/Tahirpathan-AiLab/Evaan_Personal_Intelligence_Engine) |
| `sessiontrove` | 私有归档 Claude Code、Codex 等 agent 的原始会话；其中可能含密钥、路径与第三方材料，训练或同步前必须脱敏治理。 | [GitHub](https://github.com/maedmatt/sessiontrove) |
| `ai-memory` | 用 Markdown/Git wiki、MCP 与生命周期 hook 让 coding agent 跨会话、跨宿主交接上下文；敏感采集、权限隔离和过期 handoff 须独立治理。 | [GitHub](https://github.com/akitaonrails/ai-memory) |
| `zeromem` | Rust 的 agent 记忆实现，从原始对话 turn 重建图、时间和混合检索；检索效果与隐私仍须独立验证。 | [GitHub](https://github.com/ptaranat/zeromem) |
| `reflection-engine` | 要求 AI 基于既有个人上下文生成带证据、置信度与行动建议的反思 prompt；输出敏感。 | [GitHub](https://github.com/kropdx/reflection-engine) |
| `agent-inbox` | 将手机或浏览器发现的链接投递到 REST 队列，交给任意 agent/MCP client 后续处理。 | [GitHub](https://github.com/OGZamasu/agent-inbox) |
| `Project Continuity Memory` | 用仓库内稳定记忆与当前交接双文件，让 agent 从已验证项目状态恢复工作。 | [GitHub](https://github.com/YSjandj-design/project-continuity-memory) |
| `anchor-memory` | SQLite-first 的本地 agent 记忆链，覆盖混合召回、belief 与夜间维护。 | [GitHub](https://github.com/anhe2021212-spec/anchor-memory) |
| `zhixin-companion` | 用事实、感受、解释三层框架辅助个人记录与反思的本地提示词/agent 配置。 | [GitHub](https://github.com/LotusDecoder/zhixin-companion) |
| `dreamvault` | 将 companion 的未锚定生成隔离在主记忆检索路径之外的治理规范与参考实现。 | [GitHub](https://github.com/SilviaYue/dreamvault) |
| `TokenScope` | 解析 Claude Code 本地 transcript 的 token profiler，定位可量化的上下文浪费。 | [GitHub](https://github.com/AviVAvi/TokenScope) |
| `RAG-OS` | 用 Git/Markdown 知识库构建的自托管个人 agent/RAG 工作台。 | [GitHub](https://github.com/csnyder256/RAG-OS) |
| `not-goldfish` | SQLite/FTS5 驱动的跨 agent 本地记忆与上下文卫生层。 | [GitHub](https://github.com/vmelooo/not-goldfish) |
| `XPC.md` | 用 Markdown 维护跨会话、跨模型项目记忆的 prompt 框架。 | [GitHub](https://github.com/tk-wxy/XPC.md) |
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
| `oh-my-ai-company` | 持续更新的 AI 公司对象图谱和研究库，把公司、产品、投资人、流量信号和证据来源结构化。 | [GitHub](https://github.com/yan5xu/oh-my-ai-company) |
| `deja-vu` | 本地索引 Claude Code、Codex、opencode 等会话日志，并通过搜索、MCP recall 和自动上下文注入复用历史经验。 | [GitHub](https://github.com/vshulcz/deja-vu) |
| `personal-model` | 本地优先的 Personal Model / HUMAN.md，通过 MCP 给 agent 提供带证据的用户工作方式与偏好上下文。 | [GitHub](https://github.com/Intuition-Lab/personal-model) |
| `memmy-agent` | 跨 Codex、Claude Code、Cursor 等 agent 的个人长期记忆中心和本地 runtime。 | [GitHub](https://github.com/MemTensor/memmy-agent) |
| `mentor` | 读取 Claude Code 与 Codex 本地历史的 session-insights skill，生成个人 agent 使用复盘报告。 | [GitHub](https://github.com/smixs/mentor) |

### RAG、检索与知识处理

| 项目 | 简介 | 链接 |
| --- | --- | --- |
| `pdf-inspector` | Rust PDF 分类、位置感知抽取和选择性 OCR 路由层，覆盖 CLI、Python、Node 与 Wasm；关键数字、表格和阅读顺序仍须版面对照。 | [GitHub](https://github.com/firecrawl/pdf-inspector) |
| `datahub` | 面向数据发现、治理、血缘和可观测性的 AI data catalog，以 metadata graph 为 agent/RAG 提供上下文；连接器、权限、数据新鲜度和生产部署须独立核验。 | [GitHub](https://github.com/datahub-project/datahub) |
| `research-radar` | workspace-first 的自托管研究订阅、去重、透明排序与本地检索工具；当前为 v0.1 alpha，真实订阅/反馈数据须独立保护。 | [GitHub](https://github.com/researchradar/research-radar) |
| `semantica` | 将数据、知识图谱、向量检索与 agent 决策 provenance 组织为可查询的 Context Graph；关键事实与审批仍要回到原始证据。 | [GitHub](https://github.com/semantica-agi/semantica) |
| `rag-ci` | 以配对 bootstrap、置信区间和最小效应门控 RAG 回归的 CLI/CI 工具；结论仍受 golden set 质量限制。 | [GitHub](https://github.com/Nokimalos/rag-ci) |
| `research-evidence-agent` | 本地生成证据 manifest 并审计 claim—evidence 类型对应关系的科研发布预检工具。 | [GitHub](https://github.com/zxxasdfrty/research-evidence-agent) |
| `SparkFetch` | 自托管网页抓取与清洗 API，输出适合 LLM/RAG 的 Markdown 和结构化数据；需单独约束授权与注入风险。 | [GitHub](https://github.com/Sparkfetch/sparkfetch) |
| `IngestReasonCreate` | 本地文档工作流 playbook：抽取为带页码 Markdown、推理、真实引擎构建、回读核验，避免 agent 编造文档事实。 | [GitHub](https://github.com/shinmingh/IngestReasonCreate) |
| `Docvion` | 为 Docling、Tesseract、PaddleOCR 等解析器提供统一文档 schema 与结构感知 chunking 的 Python 适配层。 | [GitHub](https://github.com/prolixis/docvion) |
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
| `graphiti` | Zep 的 temporal context graph 引擎，为 agents 提供可追踪、可随时间变化的图谱记忆。 | [GitHub](https://github.com/getzep/graphiti) |

### 前端、UI 与 Agent 交互层

| 项目 | 简介 | 链接 |
| --- | --- | --- |
| `BrowserOS` | 同仓库提供 agent 专用第二浏览器与内置 agent 的 Chromium fork，可复用真实登录态并本地回放；真实账号副作用与日志隐私须严格治理。 | [GitHub](https://github.com/browseros-ai/BrowserOS) |
| `scroll-craft` | Claude Code 的滚动网页设计与验证 skill，使用浏览器截图检查交互和显示问题；不替代无障碍与人工设计验收。 | [GitHub](https://github.com/nateherkai/scroll-craft) |
| `chatbot-template` | shadcn-ui 的 Next.js/AI SDK 聊天模板，含流式消息、工具状态与人机问卷；公开部署前须补认证、限流和预算保护。 | [GitHub](https://github.com/shadcn-ui/chatbot-template) |
| `moli` | Rust agent 浏览器，默认 DOM/结构化数据、布局和像素按需计算；需实测兼容性与数据边界。 | [GitHub](https://github.com/lexmount/moli) |
| `AbaoPal` | Android 原生手机自动化 agent，结合无障碍 UI、截图、多 agent 循环、录制回放与 skills。 | [GitHub](https://github.com/banye-technology/AbaoPal) |
| `council-lab` | 本地优先的多模型顺序审议工作台，支持人类中途介入、预算与过程导出。 | [GitHub](https://github.com/loveramarois-byte/council-lab) |
| `fingertips` | 将打字时长、停顿等非内容节律信号接入对话 AI 的轻量组件。 | [GitHub](https://github.com/eveacla11/fingertips) |
| `MagicTeX-mcp` | 面向 agent 的 LaTeX MCP 工作区，用 WASM 编译、PDF 锚定评论和可视化编辑构成改稿闭环。 | [GitHub](https://github.com/ZoeLinUTS/MagicTeX-mcp) |
| `mission-control-board` | 单 HTML 的依赖感知任务板，将人/agent 任务和阻塞关系可视化为可推导状态。 | [GitHub](https://github.com/rockthemike712/mission-control-board) |
| `promptamp` | 浏览器输入框的开源 BYOK prompt 增强器。 | [GitHub](https://github.com/Sina-Amare/promptamp) |
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
| `hig-mcp` | 把 Apple HIG、Liquid Glass 约束和 SwiftUI 映射转成结构化 MCP design tokens。 | [GitHub](https://github.com/aka-kika/hig-mcp) |
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
| `browser-harness` | Browser Use 的真实浏览器 CDP harness，让 agent 在运行中沉淀 helper 与 domain skill。 | [GitHub](https://github.com/browser-use/browser-harness) |
| `kill-ai-slop` | 把 AI 生成产品的视觉/文案套路整理成 taxonomy，并提供 agent skill 扫描与修复。 | [GitHub](https://github.com/yetone/kill-ai-slop) |
| `bolt-slides` | StackBlitz 的 agent 友好型 React/Web slide 框架，让演示文稿成为可运行 Web app。 | [GitHub](https://github.com/stackblitz/bolt-slides) |
| `diagram-design` | 面向 Claude Code、Codex、Pi 的图表设计 skill，输出可审阅 HTML/SVG；品牌 URL 抽取与事实准确性需独立审查。 | [GitHub](https://github.com/cathrynlavery/diagram-design) |

### 语音、视频与多模态

| 项目 | 简介 | 链接 |
| --- | --- | --- |
| `VoiceStudio` | 本地优先的语音克隆、配音、转写、听写与长音频工作台；声音同意、模型许可、可选网络功能和水印效果须独立审查。 | [GitHub](https://github.com/debpalash/VoiceStudio) |
| `clipfactory` | 自托管短视频流水线，保存脚本、镜头、字幕和渲染中间产物；无认证 API、外部 provider、费用与 Elastic 2.0 条款需审查。 | [GitHub](https://github.com/feyzilim/clipfactory) |
| `modly` | 本地 GPU 图像/提示词到 3D mesh 桌面工作台，带工作流、扩展与 CLI；扩展供应链、模型许可和输出网格须独立验收。 | [GitHub](https://github.com/lightningpixel/modly) |
| `speech-to-speech` | 组合可替换 VAD、STT、LLM、TTS 的本地语音 agent 链路；需分别管理语音同意、数据流和模型许可。 | [GitHub](https://github.com/huggingface/speech-to-speech) |
| `Scene Card Studio` | 将个人照片转为可编辑 Scene Card、版本化提示和生成审阅链的视觉叙事管线；需审查同意、版权和 provider 数据流。 | [GitHub](https://github.com/swping999/scene-card-studio) |
| `Cove Sensory MCP` | 以本地 stdio MCP 和授权路径为文本 agent 提供图像、视频、音频、音乐感知；云端 provider 数据边界需单独审查。 | [GitHub](https://github.com/moonlin1213/cove-sensory-mcp) |
| `hbg-classical-poem-silk-video` | 将古诗词转为国风竖屏动态视频的 agent skill，覆盖分镜、I2V、书法字幕与成片 QA。 | [GitHub](https://github.com/Mr-funny/hbg-classical-poem-silk-video) |
| `Resonant` | Windows 本地优先音乐工作站，可选本地 ACE-Step 生成、MCP 辅助创作与 WAV 导出；发布构建目前未签名。 | [GitHub](https://github.com/calesthio/Resonant) |
| `gbro-collage-info` | 基于 HyperFrames 的中文口播拼贴信息动画 skill，以本地 HTML/CSS/GSAP 输出 MP4。 | [GitHub](https://github.com/pyang5166/gbro-collage-info) |
| `hbg-life-simulation` | 将中文人生叙事组织为角色一致、TTS 对齐、字幕完整且经过 MP4 QA 的视频 skill。 | [GitHub](https://github.com/Mr-funny/hbg-life-simulation) |
| `project-echo` | 把档案录像的转写、关键帧描述与摘要存为可检索知识库的多模态管线。 | [GitHub](https://github.com/Commonwealth-Bank-of-Australia/project-echo) |
| `mubai-ears` | 本地转写并提取音高、能量、停顿等韵律摘要的语音预处理工具。 | [GitHub](https://github.com/hmh323/mubai-ears) |
| `stackchan-cloud-mcp` | 通过 OAuth、VPS 与 MCP 将 StackChan 桌面机器人接入 claude.ai 的工程实现。 | [GitHub](https://github.com/tianyupaipai-cmd/stackchan-cloud-mcp) |
| `OpenEyes-Live` | 可插拔端侧多模态运行时，按需组合视觉、VAD、ASR 与声纹引擎处理实时相机/麦克风输入。 | [GitHub](https://github.com/vfvincentwong2026/-OpenEyes-Live) |
| `blinkface` | 以双手取景框控制的 FLUX 实时人像风格化实验，采用 GPU server 与浏览器客户端分离架构。 | [GitHub](https://github.com/xcc3641/blinkface) |
| `scientific-illustrator` | Codex 插件，在 PowerPoint/draw.io 中用原生对象绘制、审查并修正可编辑科研插图。 | [GitHub](https://github.com/icebird1998/scientific-illustrator) |
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
| `generative-media-skills` | 生成媒体 agent skill 套件，覆盖图像、视频、音频、3D、avatar、权利和交付 QA。 | [GitHub](https://github.com/calesthio/generative-media-skills) |
| `video-shotcraft` | 面向 Claude Code / Codex 的 Remotion 视频制作 skill，沉淀镜头卡、动效预览和产品宣传片模板。 | [GitHub](https://github.com/Vincentwei1021/video-shotcraft) |

### 模型、训练与推理基础设施

| 项目 | 简介 | 链接 |
| --- | --- | --- |
| `miles` | 用 SGLang rollout、Megatron-LM / FSDP2、MoE routing replay 与低精度训练组织大规模 agent / VLM 后训练；性能和稳定性须固定集群复现。 | [GitHub](https://github.com/radixark/miles) |
| `magnitude` | 探测本机硬件、推荐 GGUF 并把本地推理接入多种 agent harness；“best”、估计 tok/s 和离线边界须实测。 | [GitHub](https://github.com/magnitudedev/magnitude) |
| `Personal-AI-Router` | NVIDIA PAIR 在局域网多节点间路由独立 Ollama/LM Studio 请求；不合并 VRAM，PIN、telemetry 与本地 API 仍需治理。 | [GitHub](https://github.com/NVIDIA/Personal-AI-Router) |
| `deep-swe` | 用 113 个长时程原始工程任务、隔离 verifier 和 trajectory 评测 coding agents；公开榜单仍需污染、版本、成本和人工质量审计。 | [GitHub](https://github.com/datacurve-ai/deep-swe) |
| `sie` | 为 agents 统一服务 embedding、rerank、抽取与生成等任务模型的自托管推理引擎；模型目录与 MTEB 信息不能替代私有任务验证。 | [GitHub](https://github.com/superlinked/sie) |
| `ODS` | 将本地推理、Web UI、工作流、RAG、语音和图像服务组织成可安装/运维的私有 AI 栈；安装脚本、端口、网络出口和升级恢复须审计。 | [GitHub](https://github.com/Osmantic/ODS) |
| `Soup` | 用单份 YAML 组织 LoRA/QLoRA、数据、评测与交付的消费级硬件微调 CLI；低显存演示须以固定模型和硬件独立复现。 | [GitHub](https://github.com/MakazhanAlpamys/Soup) |
| `microduck_rl` | 面向 Microduck 双足机器人的 RL、执行器/齿隙建模、ONNX 导出与 sim2real 环境；真机须在保护架、限幅和急停下验证。 | [GitHub](https://github.com/pollen-robotics/microduck_rl) |
| `Megatron-LM` | NVIDIA 的 GPU 优化 Transformer 大规模训练库，覆盖 TP/PP/DP/EP/CP、混合精度、MoE、checkpoint 与推理；规模、性能和许可证须按固定环境独立核验。 | [GitHub](https://github.com/NVIDIA/Megatron-LM) |
| `freellmapi` | 本地优先的单用户 LLM 统一路由器，提供多 provider 兼容端点、限额跟踪、健康检查和自动回退；免费额度、ToS、数据代理与无 SLA 边界须独立核验。 | [GitHub](https://github.com/tashfeenahmed/freellmapi) |
| `cutlass` | NVIDIA 的 CUDA 高性能 GEMM、CuTe 和 CuTe DSL 抽象库；适合构建/调优训练与推理 kernel，性能与兼容性依赖 GPU、CUDA、形状和编译选项。 | [GitHub](https://github.com/NVIDIA/cutlass) |
| `transformers` | Hugging Face 的文本、视觉、音频、视频和多模态模型定义与训练/推理框架；模型代码、权重、数据和 benchmark 仍需逐项审计。 | [GitHub](https://github.com/huggingface/transformers) |
| `fiftyone` | 面向视觉数据集和模型质量的可视化、标注、清洗、评估与错误分析工具；数据隐私、标签 schema 和评测切分须独立治理。 | [GitHub](https://github.com/voxel51/fiftyone) |
| `marin` | 记录数据、训练、评测和失败过程的 foundation model 研究框架，支持从 CPU 教程到 GPU/TPU 实验；复现性和数据许可仍需独立核验。 | [GitHub](https://github.com/marin-community/marin) |
| `aura` | 用硬件探测、预算规划和 OS 级约束协调 Ollama/GGUF/llama.cpp 的低内存本地推理；实际内存边界与质量须独立复现。 | [GitHub](https://github.com/Grevix/aura) |
| `modelprint` | 在浏览器对 OpenAI 兼容端点跑 tokenizer、错误与响应形状探针；相似指纹只支持基础设施层面的推断。 | [GitHub](https://github.com/unclecode/modelprint) |
| `omlx` | Apple Silicon 本地 LLM 推理服务器与菜单栏管理工具，提供连续批处理、分层 KV cache 和 OpenAI 兼容 API。 | [GitHub](https://github.com/jundot/omlx) |
| `llmfit` | 用本机 RAM、CPU、GPU/VRAM 和 runtime 为本地 LLM 做适配与速度估计，并支持真实基准；估计须以实际模型、负载和质量任务复验。 | [GitHub](https://github.com/AlexsJones/llmfit) |
| `unsloth` | 本地运行、训练和部署模型的 Desktop/Studio/Core 工具栈；安装脚本、远程访问和 agent 工具权限均需独立审计。 | [GitHub](https://github.com/unslothai/unsloth) |
| `Switchyard` | NVIDIA NeMo 的预览期 LLM 路由/协议适配层；代理凭据、数据流、兼容性与路由回退需独立验证。 | [GitHub](https://github.com/NVIDIA-NeMo/Switchyard) |
| `Distillery` | 多 provider LLM API 网关，集中路由、代理凭据、配额、用量与可选脱敏/采集；提示词和日志仍需独立治理。 | [GitHub](https://github.com/TonicAI/distillery) |
| `ai-evals` | Rails 发布的早期 AI 模型评测入口；任务、数据与许可信息仍需审计，不能据此推导模型排名。 | [GitHub](https://github.com/rails/ai-evals) |
| `time-to-first-token` | 以一个可部署服务串起 LLM 推理、TTFT/成本观测、压测、量化和可复现 benchmark 的十周实践路线。 | [GitHub](https://github.com/patchy631/time-to-first-token) |
| `slopsource` | 持续发布可自托管 AI 应用替代实现的单仓库计划；功能与许可需逐项核验。 | [GitHub](https://github.com/micahc123/slopsource) |
| `open-free-router` | 聚合多个免费模型上游、按模型 ID 路由的本地代理和同步工具。 | [GitHub](https://github.com/NoelJudeNoel/open-free-router) |
| `deltafin` | 在 Apple Silicon 上以按需 MoE expert 缓存探索运行 Kimi K3 的本地推理实验。 | [GitHub](https://github.com/gavamedia/deltafin) |
| `jaxotron` | 用 JAX/Equinox 展示数据、全分片、张量 3D 并行的极简 LLM 训练器。 | [GitHub](https://github.com/rishiraj/jaxotron) |
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
| `auto` | 记录并编译 LLM agent 重复行为为受能力约束的 WASM fast path，探索 agent 成本和安全边界。 | [GitHub](https://github.com/RightNow-AI/auto) |
| `conversation-steganography` | LLM 隐写 proof of concept，把加密消息伪装成普通聊天文本，双重用途风险高。 | [GitHub](https://github.com/nethical6/conversation-steganography) |
| `nativ` | Apple Silicon 本地 AI 工作台，用 SwiftUI 封装 MLX 模型服务、性能监控和兼容 API。 | [GitHub](https://github.com/Blaizzy/nativ) |
| `needle` | 面向端侧受约束工具调用和结构化抽取的小模型；schema 约束不能替代工具权限、参数校验或人工确认。 | [GitHub](https://github.com/cactus-compute/needle) |

### AI 学习与教育资源

| 项目 | 简介 | 链接 |
| --- | --- | --- |
| `Hands-On-AI-Engineering` | 覆盖 agent、OCR、音频、多模态、RAG 和微调的实践样例库；“production-ready”须逐项目验证，README 的 MIT 声明缺少根目录 LICENSE 支撑。 | [GitHub](https://github.com/Sumanth077/Hands-On-AI-Engineering) |
| `agent_tutorial` | 中文八章智能体教程，按模型调用、RAG、工具、记忆、harness 与协作递进；生产级安全、评测和依赖仍须逐章补齐。 | [GitHub](https://github.com/gitzyong812/agent_tutorial) |
| `ai-agent-book` | 覆盖上下文、工具、评估、后训练与协作的开源 AI Agent 书稿，配有 10 章和 103 个实验入口。 | [GitHub](https://github.com/bojieli/ai-agent-book) |
| `AI-For-Beginners` | Microsoft 的 12 周、24 课 AI 入门课程，覆盖经典 AI、深度学习、视觉、NLP、多智能体与伦理；课程时效与外部依赖须另行复核。 | [GitHub](https://github.com/microsoft/AI-For-Beginners) |
| `OpenMAIC` | 清华 THU-MAIC 的多智能体互动课堂平台，把主题/材料生成课程、幻灯片、测验、交互场景和课堂讨论；教育效果、材料、模型和导出结果须独立审核。 | [GitHub](https://github.com/THU-MAIC/OpenMAIC) |

### 办公、商业与行业应用

| 项目 | 简介 | 链接 |
| --- | --- | --- |
| `MathModelAgent` | 数学建模、代码、图表、Typst 与验收的 skills / 桌面工作流；功能表与 TODO 状态不一致，且当前许可限制商业用途。 | [GitHub](https://github.com/jihe520/MathModelAgent) |
| `Sequoia-X` | 基于 baostock、SQLite 和规则策略的 A 股收盘后筛选系统；形态不是收益证据，README 的 MIT 声明与缺失 LICENSE 文件须复核。 | [GitHub](https://github.com/sngyai/Sequoia-X) |
| `geo-seo-claude` | 将 GEO / SEO、crawler、schema 与报告封装成 Claude Code skills；复合分数和营销数字不能证明 AI 搜索引用或转化。 | [GitHub](https://github.com/zubair-trabzada/geo-seo-claude) |
| `openresearch-cli` | 本地优先的科研 agent 工作区，用 worktree、实验树、commit archive 与多类计算后端保存运行谱系；记录完整不等于科学结论成立。 | [GitHub](https://github.com/alphaXiv/openresearch-cli) |
| `open-seo` | 将关键词、排名、链接、站点审计和 AI visibility 数据通过 Web、MCP 与 skills 提供给人和 agent；自托管仍依赖付费数据 API。 | [GitHub](https://github.com/every-app/open-seo) |
| `robin` | 通过 Tor、搜索/抓取模块和 LLM 组织暗网 OSINT 调查；仅限书面授权与合法范围，摘要不能替代证据复核。 | [GitHub](https://github.com/apurvsinghgautam/robin) |
| `OpenBB` | 面向分析师、量化人员和 AI agent 的金融数据集成层，统一连接 provider、Python、Workspace、Excel、MCP 与 REST；数据许可、金融风险和 AGPL 义务须分别审查。 | [GitHub](https://github.com/OpenBB-finance/OpenBB) |
| `patent-disclosure-skill` | 中文专利交底、专利解读、政策观察和审查答复辅助 skill，结合项目扫描、图示、Obsidian 与案例 RAG；法律判断、机密材料和查新证据必须人工核验。 | [GitHub](https://github.com/handsomestWei/patent-disclosure-skill) |
| `ai-job-search` | 在本机用 Claude Code 组织职位搜索、匹配、CV/求职信、面试和结果追踪；个人资料、职位站点条款与自动提交须人工控制。 | [GitHub](https://github.com/MadsLorentzen/ai-job-search) |
| `ToolJet` | 构建内部工具、工作流与 agent 的低代码平台；连接器、脚本、服务账号、行列级权限和 AGPL-3.0 义务须分别审计。 | [GitHub](https://github.com/ToolJet/ToolJet) |
| `ai-nuclear-spectroscopy` | 从公开核数据到 GCD 寿命估计的可审计人机协同参考流程；当前为合成数据 alpha，不能替代真实实验验证。 | [GitHub](https://github.com/JWP-p/ai-nuclear-spectroscopy) |
| `Lophius` | 语言模型研究工作台观察项；公开 README 尚无可复核安装/架构细节，AGPL-3.0 义务须按部署评估。 | [GitHub](https://github.com/p-e-w/lophius) |
| `Aetheris` | 面向学术研究流程的 Web/桌面 Agent，覆盖检索、写作、分析和子 agent；生成结论、引文与数据必须独立核验。 | [GitHub](https://github.com/shiqiaoshangxue/aetheris) |
| `open-kimi-ppt-skill` | 非官方 Kimi Slides 兼容 skill，生成可续改 PPTD 与 PPTX，并提供本地编辑器；协议兼容性与安装范围需核验。 | [GitHub](https://github.com/Binaryify/open-kimi-ppt-skill) |
| `qiaomu-seo` | 覆盖技术 SEO、迁移、流量诊断与 AI 搜索可见性边界的 agent skill。 | [GitHub](https://github.com/joeseesun/qiaomu-seo) |
| `InduSecAgent` | 将工业流程、PLC 点位与时序建为工业时空图，用于异常检测和溯源原型。 | [GitHub](https://github.com/yuhuangerdi/InduSecAgent) |
| `agent` | Talivia 的 MCP agent kit，协助将网站追踪、事件核验和支付归因接入代码项目。 | [GitHub](https://github.com/talivia-group/agent) |
| `ai-stock-pool` | 覆盖美股/A 股映射与产业链线索的 AI 行业股票池研究工具。 | [GitHub](https://github.com/yaoleifly/ai-stock-pool) |
| `geolook` | 本地自托管的 GEO 工作台，覆盖生成式引擎采样、诊断、工单与验收。 | [GitHub](https://github.com/bingqiang2021/geolook) |
| `dreampaper` | 本地模板驱动的科研图与学术幻灯片生成应用。 | [GitHub](https://github.com/dream-rec/dreampaper) |
| `Kition` | 将关联 Markdown、表格、浏览器研究、AI agent 与可视化自动化放入同一桌面工作区。 | [GitHub](https://github.com/KitionAI/kition) |
| `slide-meme-inserter` | Claude Code / Codex 共享的 HTML 演示文稿 skill，用明确叙事角色和审计流程插入梗图。 | [GitHub](https://github.com/amnotyoung/slide-meme-inserter) |
| `job-search-workflow` | 本地优先的 AI 辅助求职框架，覆盖职位分诊、材料起草、决策记录和申请追踪。 | [GitHub](https://github.com/rcnsnr/job-search-workflow) |
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
| `openscience` | Synthetic Sciences 的开源科研 AI workbench，把文献、代码、实验、科学数据库和报告写作接入同一浏览器工作区。 | [GitHub](https://github.com/synthetic-sciences/openscience) |
| `CSSwitch` | Claude Science 的第三方模型接入切换工具，用本地代理连接 DeepSeek、Qwen、GLM、Kimi 等端点。 | [GitHub](https://github.com/SuperJJ007/CSSwitch) |
| `meetily` | 隐私优先的本地 AI 会议助手，覆盖实时转写、说话人分离、Ollama 摘要和自托管会议记录。 | [GitHub](https://github.com/Zackriya-Solutions/meetily) |
| `Vibe-Research` | 个人 AI 投研看板，整合 A 股/美股/港股数据、资讯、持仓、研报和本地 AI 分析入口。 | [GitHub](https://github.com/simonlin1212/Vibe-Research) |
| `dashiAI-ppt-skill` | 中文 AI PPT skill，生成可浏览器编辑的 HTML deck，并导出 PDF / 可编辑 PPTX。 | [GitHub](https://github.com/chuspeeism/dashiAI-ppt-skill) |
| `GemType` | 开源 BYOK AI 写作助手和 Grammarly 替代品，覆盖浏览器扩展与 Word add-in。 | [GitHub](https://github.com/riponcm/GemType) |
| `moore-wechat-article-downloader` | 本地优先的微信公众号内容情报库，把文章、评论和互动数据沉淀成可搜索资料。 | [GitHub](https://github.com/Moore-developers/moore-wechat-article-downloader) |
| `cue` | 开源 macOS 悬浮 AI copilot，面向屏幕、会议和 BYOK 实时辅助场景。 | [GitHub](https://github.com/Blueturboguy07/cue) |
| `agent-pulse` | 证据驱动 AI 行业情报项目，把来源、事件、判断和刷新节奏分离。 | [GitHub](https://github.com/barretlee/agent-pulse) |
| `circuit-framework` | 面向 crypto paper trading 的多 agent 研究框架，用确定性风险门控约束交易提案。 | [GitHub](https://github.com/PengZhang64/circuit-framework) |

## 完整索引与每日热点

- 全量项目目录：[`projects/`](./projects/)
- 最近日报：
  - [`2026-09-05`](./daily/2026-09-05/ai-hotspots.md)
  - [`2026-09-04`](./daily/2026-09-04/ai-hotspots.md)
  - [`2026-09-03`](./daily/2026-09-03/ai-hotspots.md)
  - [`2026-09-02`](./daily/2026-09-02/ai-hotspots.md)
  - [`2026-09-01`](./daily/2026-09-01/ai-hotspots.md)
  - [`2026-08-31`](./daily/2026-08-31/ai-hotspots.md)
  - [`2026-08-28`](./daily/2026-08-28/ai-hotspots.md)
  - [`2026-08-27`](./daily/2026-08-27/ai-hotspots.md)
  - [`2026-08-26`](./daily/2026-08-26/ai-hotspots.md)
  - [`2026-08-25`](./daily/2026-08-25/ai-hotspots.md)
  - [`2026-08-24`](./daily/2026-08-24/ai-hotspots.md)
  - [`2026-08-23`](./daily/2026-08-23/ai-hotspots.md)
  - [`2026-08-22`](./daily/2026-08-22/ai-hotspots.md)
  - [`2026-08-21`](./daily/2026-08-21/ai-hotspots.md)
  - [`2026-08-20`](./daily/2026-08-20/ai-hotspots.md)
  - [`2026-08-19`](./daily/2026-08-19/ai-hotspots.md)
  - [`2026-08-18`](./daily/2026-08-18/ai-hotspots.md)
  - [`2026-08-17`](./daily/2026-08-17/ai-hotspots.md)
  - [`2026-08-16`](./daily/2026-08-16/ai-hotspots.md)
  - [`2026-08-15`](./daily/2026-08-15/ai-hotspots.md)
  - [`2026-08-14`](./daily/2026-08-14/ai-hotspots.md)
  - [`2026-08-13`](./daily/2026-08-13/ai-hotspots.md)
  - [`2026-08-12`](./daily/2026-08-12/ai-hotspots.md)
  - [`2026-08-11`](./daily/2026-08-11/ai-hotspots.md)
  - [`2026-08-10`](./daily/2026-08-10/ai-hotspots.md)
  - [`2026-08-09`](./daily/2026-08-09/ai-hotspots.md)
  - [`2026-08-07`](./daily/2026-08-07/ai-hotspots.md)
  - [`2026-08-06`](./daily/2026-08-06/ai-hotspots.md)
  - [`2026-08-05`](./daily/2026-08-05/ai-hotspots.md)
  - [`2026-08-04`](./daily/2026-08-04/ai-hotspots.md)
  - [`2026-08-03`](./daily/2026-08-03/ai-hotspots.md)
  - [`2026-08-02`](./daily/2026-08-02/ai-hotspots.md)
  - [`2026-08-01`](./daily/2026-08-01/ai-hotspots.md)
  - [`2026-07-31`](./daily/2026-07-31/ai-hotspots.md)
  - [`2026-07-30`](./daily/2026-07-30/ai-hotspots.md)
  - [`2026-07-29`](./daily/2026-07-29/ai-hotspots.md)
  - [`2026-07-28`](./daily/2026-07-28/ai-hotspots.md)
  - [`2026-07-27`](./daily/2026-07-27/ai-hotspots.md)
  - [`2026-07-26`](./daily/2026-07-26/ai-hotspots.md)
  - [`2026-07-25`](./daily/2026-07-25/ai-hotspots.md)
  - [`2026-07-24`](./daily/2026-07-24/ai-hotspots.md)
  - [`2026-07-23`](./daily/2026-07-23/ai-hotspots.md)
  - [`2026-07-22`](./daily/2026-07-22/ai-hotspots.md)
  - [`2026-07-21`](./daily/2026-07-21/ai-hotspots.md)
  - [`2026-07-20`](./daily/2026-07-20/ai-hotspots.md)
  - [`2026-07-18`](./daily/2026-07-18/ai-hotspots.md)
  - [`2026-07-17`](./daily/2026-07-17/ai-hotspots.md)
  - [`2026-07-16`](./daily/2026-07-16/ai-hotspots.md)
  - [`2026-07-15`](./daily/2026-07-15/ai-hotspots.md)
  - [`2026-07-14`](./daily/2026-07-14/ai-hotspots.md)
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

如果你要找的是某个具体项目，而不是看分类，直接在 [`projects/`](./projects/) 中按名称查找会更快。

## 当前状态

- 状态：持续日更中。
- 最新更新：`2026-09-05`。
- 当前项目总数：`609`。
- 最近新增项目：`miles`、`loopx`、`text-to-cad`、`MathModelAgent`、`OB1`、`Hands-On-AI-Engineering`、`agentdesktop`。
- 覆盖平台：GitHub、X、Instagram、YouTube。

## 维护约定

- 默认直接在当前分支更新，不新建分支。
- 所有项目目录统一收纳到 `projects/`。
- 每日自动化不仅更新 `daily/` 与 `projects/`，还要同步维护首页分类导航、项目简介和链接。
- 新项目优先归入既有分类；只有在现有分类明显不合适时才新增分类。
- 自动化成功完成后，默认提交并推送到 `origin/master`。
- 热点内容优先采用官方来源与主流媒体交叉验证。
- 社媒条目须标注可复核状态；无法独立读取原帖时，只能作为观察入口，不得虚构互动量或传播结论。
- 对争议性结论明确区分“事实、判断、不确定性”。
- 若 GitHub 头部热点已在仓库中建立目录，则优先刷新既有项目说明，并在当日日报中显式说明取舍。
