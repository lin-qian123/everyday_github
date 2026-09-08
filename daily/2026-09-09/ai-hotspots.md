<!-- markdownlint-disable MD013 -->

# 2026-09-09 AI 热点日报

> 抓取时间：2026-09-09（Asia/Shanghai）。GitHub Trending 的 `stars today` 是抓取时点的短期关注信号；stars、forks、open issues、release、许可证与更新时间来自 GitHub REST API / 上游页面快照，后续会变化。`search-layer` 对近一周 AI 开源发布的多源检索本轮返回 0 条可用项目候选，因此项目选择透明降级到 GitHub 官方综合及分语言 Trending、REST API、README、ROADMAP、CHANGELOG、release 与 LICENSE。X 定向搜索未返回可独立读取的项目帖子卡片；Instagram 只提供主题热门页；YouTube 可读取若干项目或主题视频的相对发布时间与动态播放量，三类社媒信号均不与 GitHub stars 合并。

## 今日判断

- `teamai-cli`、`superplane` 与 `agentic-api` 分别把 agent 能力推向团队配置分发、工程流水线和推理 gateway；它们解决的是控制面与协议层问题，不自动证明执行结果正确或权限已隔离。
- `i-have-adhd` 显示“输出与交互设计”正在成为独立 skill 热点；更短、更行动导向可能降低认知负担，也可能省略风险、前提和不确定性。
- `notfair-plugin` 与 `feynman` 都把通用 agent 变成领域工作台：前者接近广告 / 分析账户，后者接近论文、研究资产和 compute。领域化带来更清晰流程，也带来更高的数据、许可、费用和证据责任。
- 许可证元数据仍需人工复核：`teamai-cli` API 为 `NOASSERTION`，根 LICENSE 则明确是 MIT。六个项目均未在本机安装或运行，功能、性能、安全、隐私和科学 / 业务效果都只按静态上游证据记录。

## GitHub 热点项目

| 项目 | 可核验信号 | 分类 | 评价 |
| --- | --- | --- | --- |
| [i-have-adhd](../../projects/i-have-adhd/README.md) | 官方综合 / Python Trending 约 +422 当日 stars；API 快照 30,225 stars、1,845 forks、31 open issues，MIT，无 GitHub release，根 package 版本 `0.2.0`。 | Agent 框架与技能生态 | 用十条规则让 coding agent 先给行动、少铺垫；它是沟通 policy，不是 ADHD 医疗工具，且压缩不能覆盖关键 caveat。 |
| [teamai-cli](../../projects/teamai-cli/README.md) | 官方 TypeScript Trending 约 +1,215 当日 stars；API 快照 2,311 stars、153 forks、26 open issues，`v0.23.0`；API `NOASSERTION`，根 LICENSE 为 MIT。 | Agent 框架与技能生态 | 用 Git/MR 在多个宿主间同步 skills、rules、hooks、MCP 与知识；自动 pull 和用户级注入会把共享仓库变成高信任供应链。 |
| [notfair-plugin](../../projects/notfair-plugin/README.md) | 官方 TypeScript Trending 约 +51 当日 stars；API 快照 3,680 stars、467 forks、14 open issues，MIT，无 GitHub release。 | 办公、商业与行业应用 | 45 个 SEO/GEO/广告/分析 skills 加 hosted OAuth MCP；行为 guardrail 不能替代账户 scope、预算上限、readback 和人工批准。 |
| [agentic-api](../../projects/agentic-api/README.md) | 官方 Rust Trending 约 +22 当日 stars；API 快照 232 stars、62 forks、67 open issues，`v0.5.0`，Apache-2.0。 | 模型、训练与推理基础设施 | 在 vLLM 前实现 stateful Responses、transport 与 tool ownership；production storage / observability 尚在 roadmap，兼容协议不等于模型语义等价。 |
| [superplane](../../projects/superplane/README.md) | 官方 Go Trending 约 +244 当日 stars；API 快照 6,308 stars、629 forks、609 open issues，`v0.30.0`，Apache-2.0；README 标注 beta。 | Agent 框架与技能生态 | 以 factory/work order/line/run 组织 backlog 到 PR；官网比例是未独立复现的营销指标，高权限 connector 与 retry 必须做幂等和授权验证。 |
| [feynman](../../projects/feynman/README.md) | 官方 TypeScript Trending 约 +268 当日 stars；API 快照 9,233 stars、1,053 forks、6 open issues，`v0.3.48`，MIT；main package 已为 `0.3.49`。 | RAG、检索与知识处理 | 将 paper access、literature review、citation graph、audit 与 replication planning 合入 research agent；source-grounded、下载或运行都不等于科学结论已复现。 |
| `diagram-design`、`openai/skills`、`ECC`、`hyperframes`、`marketingskills`、`superpowers`、`andrej-karpathy-skills`、`camofox-browser`、`browser-use`、`context-mode`、`AutoHedge`、`9router`、`ponytail`、`Open-Generative-AI`、`openwhispr`、`OpenBidKit_Yibiao`、`open-science`、`OmniVoice`、`WeKnora`、`RuView`、`caveman` 等 | 官方综合 / Python / TypeScript / JavaScript / Rust / Go Trending 再次出现，部分仍有显著当日新增。 | 既有分类 | 均已有项目页或历史日报记录，本轮不重复建档。 |

以上可回到 [GitHub Trending](https://github.com/trending)、[Python Trending](https://github.com/trending/python?since=daily)、[TypeScript Trending](https://github.com/trending/typescript?since=daily)、[JavaScript Trending](https://github.com/trending/javascript?since=daily)、[Rust Trending](https://github.com/trending/rust?since=daily)、[Go Trending](https://github.com/trending/go?since=daily) 与各项目 [API：i-have-adhd](https://api.github.com/repos/ayghri/i-have-adhd)、[teamai-cli](https://api.github.com/repos/Tencent/teamai-cli)、[notfair-plugin](https://api.github.com/repos/nowork-studio/notfair-plugin)、[agentic-api](https://api.github.com/repos/vllm-project/agentic-api)、[superplane](https://api.github.com/repos/superplanehq/superplane)、[feynman](https://api.github.com/repos/advaitpaliwal/feynman) 复核。

## X、Instagram、YouTube 观察

### 近期讨论主题

| 主题 | 可追溯来源 | 讨论点与评价 | 可复核状态 |
| --- | --- | --- | --- |
| 团队开始把 skills、rules、hooks、MCP 与 knowledge 当成可版本化的共享 harness | [teamai-cli README](https://github.com/Tencent/teamai-cli)、[X `teamai-cli` 搜索](https://x.com/search?q=%22teamai-cli%22&src=typed_query)、[YouTube「CLI vs MCP」主题视频](https://www.youtube.com/watch?v=g9JIUM0MHgQ) | YouTube 搜索页本轮显示 IBM Technology 主题视频约 4 个月前、127,777 次播放，但它没有评测 TeamAI。核心争议是自动同步能否兼顾一致性、review、最小权限与可回滚。 | GitHub 可直接读；X 搜索只返回客户端壳层。YouTube 视频可回溯但只说明 CLI/MCP 主题受关注。 |
| 输出风格本身正在被打包为 agent skill | [i-have-adhd README](https://github.com/ayghri/i-have-adhd)、[项目相关第三方视频](https://www.youtube.com/watch?v=EpU0Cj4jlVg)、[Instagram `aiagents` 热门页](https://www.instagram.com/explore/tags/aiagents/) | YouTube 搜索页显示该项目视频约 1 个月前、11,354 次播放；Instagram 页面标题显示约 129k reels，仅为标签库存。行动优先可能提升可读性，也可能把复杂问题压成过度确定的指令。 | 项目视频可回溯，播放量会变化；Instagram 无项目关联，不能当该 skill 的传播量。 |
| Stateful agentic API 正与推理引擎分层 | [agentic-api README](https://github.com/vllm-project/agentic-api)、[vLLM Office Hours agent 主题视频](https://www.youtube.com/watch?v=tdoZ5-xq2GE)、[X `vLLM Agentic API` 搜索](https://x.com/search?q=%22vLLM%20Agentic%20API%22&src=typed_query) | YouTube 搜索页显示 office hours 约 3 个月前、690 次播放，讨论 vLLM 与 agent applications，不是 `agentic-api v0.5.0` benchmark。争议在于 gateway 该拥有多少 state / tool execution，以及兼容层是否掩盖模型差异。 | GitHub / YouTube 可回溯；X 未独立读取帖子、日期或互动量。 |
| “AI software factory”从单次 coding agent 扩展到 backlog qualification 与 PR 流水线 | [superplane README](https://github.com/superplanehq/superplane)、[SuperPlane 官方 X](https://x.com/superplanehq)、[官方 Beta Launch 视频](https://www.youtube.com/watch?v=iMC2Uk2gVLg)、[近期第三方访谈](https://www.youtube.com/watch?v=ImmGPFNju8c) | YouTube 搜索页显示官方视频约 2 个月前、143 次播放；第三方访谈约 15 小时前、3,080 次播放。公开讨论存在，但不能据此验证官网的 one-shot 比例、PR 质量或节省工时。 | 官方 X profile 可识别，未读取具体帖文指标；两个 YouTube 页面可回溯，数字为抓取时点。 |
| AI research agent 把检索、排序、代码审计与复现计划收进本地 workbench | [feynman README](https://github.com/advaitpaliwal/feynman)、[第三方项目介绍视频](https://www.youtube.com/watch?v=EAk4hAuFTqs)、[Instagram `airesearch` 热门页](https://www.instagram.com/explore/tags/airesearch/) | 视频索引本轮显示约 5 个月前、999 次播放与 34 likes；Instagram 页面标题显示约 362k reels，仅为宽泛主题库存。最重要的分歧不是功能多少，而是全文、引用、代码运行与科学结论能否保持分级。 | 视频点名 Feynman，但属于第三方且较旧；Instagram 未确认任何项目内容或互动。 |
| 营销 agent 从写文案走向 live analytics 与广告账户 connector | [notfair-plugin README](https://github.com/nowork-studio/notfair-plugin)、[AI marketing agent 主题视频](https://www.youtube.com/watch?v=eorc3jLBqIA)、[Instagram `aimarketing` 热门页](https://www.instagram.com/popular/aimarketing/?utm_source=explore_tag) | YouTube 搜索页显示主题视频约 6 个月前、252,715 次播放；Instagram 页面标题显示约 1.3m reels。两者都不是 NotFair 的效果或采用证据。账户写入、归因、平台政策与 hosted MCP 数据流需要分别治理。 | 主题视频和标签页可打开；未确认项目级帖子、日期或互动量。 |

### 平台入口与状态

| 平台 | 本轮入口 | 热度信号与边界 |
| --- | --- | --- |
| GitHub | [官方综合 Trending](https://github.com/trending)及 Python / TypeScript / Rust / Go 分榜、六个仓库 API / README / release / LICENSE | 六个新建档项目均有抓取时点 `stars today`；这只说明短期公开关注度，不证明安装、性能、安全、隐私、业务效果或科研复现。 |
| X | [`teamai-cli`](https://x.com/search?q=%22teamai-cli%22&src=typed_query)、[`vLLM Agentic API`](https://x.com/search?q=%22vLLM%20Agentic%20API%22&src=typed_query)、[`i-have-adhd`](https://x.com/search?q=%22i-have-adhd%22&src=typed_query) 搜索与 [SuperPlane 官方 profile](https://x.com/superplanehq) | 搜索请求返回客户端 / 登录壳层；SuperPlane profile 标题可识别，但本轮未独立读取具体帖子、发布时间或互动量，全部只作入口。 |
| Instagram | [`aiagents`](https://www.instagram.com/explore/tags/aiagents/)、[`airesearch`](https://www.instagram.com/explore/tags/airesearch/)、[`aimarketing`](https://www.instagram.com/popular/aimarketing/?utm_source=explore_tag) | 页面标题在抓取时分别显示约 129k、362k、1.3m reels；这些是宽泛标签库存、会动态变化，也未确认与六个项目存在关联。 |
| YouTube | [i-have-adhd 项目视频](https://www.youtube.com/watch?v=EpU0Cj4jlVg)、[SuperPlane 官方视频](https://www.youtube.com/watch?v=iMC2Uk2gVLg)、[Feynman 项目视频](https://www.youtube.com/watch?v=EAk4hAuFTqs)、[vLLM agent 主题视频](https://www.youtube.com/watch?v=tdoZ5-xq2GE) | 搜索页可读取标题、频道、相对发布时间与动态播放量；只用于说明相关项目 / 主题存在讨论，不把第三方视频写成上游验证或统一热度。 |

## 跨平台综合观察

- 今日最强的新项目信号来自 GitHub：团队 harness、软件工厂与 stateful agentic API 同时上榜，显示焦点继续从单个 agent 转向配置、状态、审批和执行基础设施。
- 沟通 skill 与领域 plugin 说明 agent 生态正在细化到“怎么回答”和“如何按行业证据做事”；prompt 规则越可复用，版本、优先级与遗漏审计越重要。
- YouTube 对 `i-have-adhd`、SuperPlane、Feynman 和 vLLM agent 主题提供了可回溯但时间跨度不同的讨论信号；X 没有可比的帖子级数据，Instagram 只有宽泛标签库存，因此本日报不构造跨平台总热度排名。
- 任何“有 MR review”“有 tool ownership”“source-grounded”“read-only first”都只是设计起点；外部 enforcement、失败注入和真实数据回读才是运行证据。

## 后续跟踪

- 用固定任务集比较 `i-have-adhd` 的行动可见度与 caveat 漏失率，并在一次性 profile 审阅安装 diff。
- 对 `teamai-cli` 建最小测试组织，验证 auto pull、role/tag/source、hook/MCP 注入、privacy scrub、回滚和卸载残留。
- 只用脱敏 export / 低预算 sandbox 复现 `notfair-plugin` 的 read-only analysis、proposal、approval、mutation 与 post-readback。
- 对 `agentic-api` 做未知 tool、重复 continuation、SSE/WS 断流、OIDC、SQLite retention 和模型 parser contract 测试。
- 用低后果 backlog 与 mock integrations 测 SuperPlane 的 qualification precision、幂等、CI 假阳性和人工返工；用熟悉论文测 Feynman 的全文、引用、代码与复现状态分级。

## 来源与证据等级

- **A：平台原始页**——GitHub Trending、六个仓库 REST API、README、ROADMAP、CHANGELOG、release、LICENSE、SuperPlane 官方网站 / 文档 / X profile 与官方 YouTube 视频。
- **B：可回溯直接页面**——项目文档与点名项目的第三方 YouTube 视频；用于观察传播和设计，不替代安装、性能、安全、隐私、营销或科研实测。
- **C：间接信号**——X 搜索、Instagram 标签 / 热门页和 YouTube 主题搜索排序；不据此编写项目级互动量、传播范围、采用、效果或质量结论。
