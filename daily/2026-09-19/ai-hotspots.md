<!-- markdownlint-disable MD013 -->

# 2026-09-19 AI 热点日报

> 抓取时间：2026-09-19（Asia/Shanghai）。GitHub Trending 的 `stars today` 是抓取时点的短期公开关注信号；stars、forks、open issues、release、许可证和更新时间来自 GitHub REST API / 上游文件快照，后续会变化。`search-layer` CLI 对近一周 AI 开源发布与社媒讨论的四组扩展查询返回 0 条可用项目结果，通用 Web 检索只补充到周榜聚合和宽泛新闻，因此项目发现透明降级到 GitHub 官方综合及分语言 Trending，再用 REST API、README、docs、release、manifest 与 LICENSE 复核。X、Instagram、YouTube 没有统一可比的项目级数据，本报保留可追溯原帖、profile、oEmbed 视频或搜索 / 标签入口，不把 GitHub stars 换算成社媒热度。

## 今日判断

- `code-review-graph` 与 `skill-up` 分别把 Coding Agent 的上下文选择、Agent Skill 的评测迭代做成可复现工件；前者公开承认 benchmark 基线和 recall 循环性，后者仍须防止 Agent judge 与自动改 eval 形成过拟合。
- `cc-haha`、`Plannotator` 与 `power-platform-skills` 代表三种人机交互面：桌面控制台、计划 / Diff 人审界面和真实企业平台技能。GUI、批注或官方插件都不能替代最小权限、数据流和写后验证。
- `Memoh` 与 `Buzz` 把 Agent 当作长期在线 workspace / channel 成员；容器、独立 keypair、签名事件和 audit log 提供机制，但不自动证明强隔离、内容真实或副作用完整可追溯。
- `Weave Router` 将模型选择下沉到 action 级；仓库给出了可复跑 benchmark，并显示部分对照胜出、部分落后或统计近似持平，说明“动态路由必然更省且更好”不能脱离任务和费用口径。
- 八个项目均未在本机安装、运行或接入真实账号；功能、安全、隐私、隔离、成本和 benchmark 只按静态上游证据记录。

## GitHub 热点项目

| 项目 | 可核验信号 | 分类 | 评价 |
| --- | --- | --- | --- |
| [code-review-graph](../../projects/code-review-graph/README.md) | 官方 Python Trending 约 +50 当日 stars；API 快照 31,592 stars、2,872 forks、132 open issues，MIT，`v2.3.9` 于 9 月 18 日发布。 | RAG、检索与知识处理 | Tree-sitter + SQLite 图 + MCP / CI 返回 blast radius 和最小上下文；63 倍是相对完整语料的上游快照，recall ground truth 具有循环性。 |
| [cc-haha](../../projects/cc-haha/README.md) | 官方 TypeScript Trending 约 +38；API 快照 14,626 stars、8,567 forks、192 open issues，MIT，`v0.6.4`。 | Coding Agents 与终端助手 | 集成多会话、Worktree、Diff、权限、SubAgent、Computer Use、IM 与 H5；worktree 不是 sandbox，本地优先也不等于 provider / IM 零外发。 |
| [plannotator](../../projects/plannotator/README.md) | 官方 TypeScript Trending 约 +33；API 快照 8,789 stars、660 forks、164 open issues，API Apache-2.0、package `MIT OR Apache-2.0`，`v0.27.16`。 | 前端、UI 与 Agent 交互层 | 把计划、文档、HTML 与 Diff 变成可批注人工闸门；Ask AI、URL 抓取、分享与 hosted Workspaces 是不同网络 / 数据边界。 |
| [Memoh](../../projects/Memoh/README.md) | 官方 Go Trending 约 +35；API 快照 2,499 stars、236 forks、58 open issues，AGPL-3.0，`v0.20.0`。 | 记忆层与个人 AI 基础设施 | 每 Bot workspace container 集成长期记忆、浏览器、桌面、MCP 与渠道；容器 backend、egress、credential 与 OOM 边界需实测。 |
| [router](../../projects/router/README.md) | 官方 Go Trending 约 +31；API 快照 4,464 stars、123 forks、126 open issues，API `NOASSERTION` / 根 ELv2，无 GitHub Release。 | 模型、训练与推理基础设施 | Anthropic / OpenAI / Gemini 兼容 action-level router；hosted 与 self-hosted 数据流、三种费用口径和公开 benchmark caveats 必须分别阅读。 |
| [skill-up](../../projects/skill-up/README.md) | 官方 Go Trending 约 +12；API 快照 968 stars、75 forks、21 open issues，Apache-2.0，`v0.12.0` 于 9 月 18 日发布。 | Agent 框架与技能生态 | 用 YAML case、多 engine、rule / script / Agent judge 与 CI 评测 Skill；自动修 Skill / eval 需要隐藏 holdout 和人工审查。 |
| [buzz](../../projects/buzz/README.md) | 官方 Rust Trending 约 +124；API 快照 33,626 stars、4,409 forks、3,615 open issues，Apache-2.0，`desktop-v0.5.23`。 | Agent 框架与技能生态 | Nostr relay 统一人类、Agent、workflow、Git 与 audit；架构文档明确 rate limiter 尚未实现、部分 workflow action 仍为 stub。 |
| [power-platform-skills](../../projects/power-platform-skills/README.md) | 官方 JavaScript Trending 约 +11；API 快照 895 stars、182 forks、135 open issues，MIT，无 GitHub Release。 | 办公、商业与行业应用 | 微软官方 Power Platform 插件市场可操作 PAC、Azure、Dataverse、Canvas MCP 与 cloud flow；Power Pages telemetry 默认开启，真实租户写入必须人工闸门。 |
| `security-audit-skill`、`claude-code`、`open-code-review`、`ECC`、`BrowserSkill`、`agent-skills`、`Octop`、`OpenSpec`、`knowledge-work-plugins`、`supermemory`、`tradingview-mcp`、`Graphify`、`hyperframes`、`OpenShell`、`agent-browser`、`webcodex`、`OpenResearch` 等 | 官方综合 / Python / TypeScript / JavaScript / Go / Rust Trending 再次出现。 | 既有分类 | 均已有项目页或历史记录，本轮不重复建档。`anki`、`rustfs`、`hister`、`tty7` 等虽上榜，但上游核心定位不是 AI 或与今日优先主题关联较弱，本轮未收录。 |

以上可回到 [GitHub Trending](https://github.com/trending)、[Python Trending](https://github.com/trending/python?since=daily)、[TypeScript Trending](https://github.com/trending/typescript?since=daily)、[JavaScript Trending](https://github.com/trending/javascript?since=daily)、[Go Trending](https://github.com/trending/go?since=daily)、[Rust Trending](https://github.com/trending/rust?since=daily) 与各项目 [API：code-review-graph](https://api.github.com/repos/tirth8205/code-review-graph)、[cc-haha](https://api.github.com/repos/NanmiCoder/cc-haha)、[Plannotator](https://api.github.com/repos/backnotprop/plannotator)、[Memoh](https://api.github.com/repos/felinics/Memoh)、[Weave Router](https://api.github.com/repos/weave-os/router)、[skill-up](https://api.github.com/repos/alibaba/skill-up)、[Buzz](https://api.github.com/repos/block/buzz)、[Power Platform Skills](https://api.github.com/repos/microsoft/power-platform-skills) 复核。

## X 观察

| 入口 | 讨论点与评价 | 可复核状态 |
| --- | --- | --- |
| [Plannotator 批注会话帖](https://x.com/plannotator/status/2088688374790160503) | 上游 8 月 15 日博客直接引用该帖，用于展示 `/plannotator-last` 的交互批注；可确认项目传播入口，但不是 9 月 19 日同日热度证明。 | B 级原帖 URL；本轮 X 直连不可稳定读取，未写 views / likes / reposts。 |
| [@memoh_ai](https://x.com/memoh_ai)、[@relakkesyang](https://x.com/relakkesyang)、[@tirth_8205](https://x.com/tirth_8205) | 分别由 Memoh README 与 GitHub owner profile 交叉识别；用于继续观察持久 Agent、桌面工作台和代码图谱发布。 | B / C 级 profile；profile 存在不证明今天项目级高热，未取得同口径互动量。 |
| [@blockopensource](https://x.com/blockopensource)、[@OpenAtMicrosoft](https://x.com/OpenAtMicrosoft) | GitHub 组织资料对应的开源账号，可作为 Buzz 与 Power Platform Skills 的上游观察入口。 | C 级组织 profile；未识别到可独立复核的同日项目发布帖。 |

## Instagram 观察

| 入口 | 讨论点与评价 | 可复核状态 |
| --- | --- | --- |
| [`aiagents`](https://www.instagram.com/explore/tags/aiagents/)、[`codingagents`](https://www.instagram.com/explore/tags/codingagents/)、[`opensourceai`](https://www.instagram.com/explore/tags/opensourceai/) | 对应多 Agent、Coding Agent 与开源 AI 主题内容池，可观察桌面工作台、协作界面和自托管工具的视觉化传播。 | C 级主题入口；登录、地区和推荐算法会改变结果，未取得今天八个项目的稳定帖子或互动量。 |
| [`powerplatform`](https://www.instagram.com/explore/tags/powerplatform/)、[`code review`](https://www.instagram.com/explore/tags/codereview/) | 分别对应企业低代码 / 自动化与代码审阅主题；标签共现不能证明 `power-platform-skills` 或 `code-review-graph` 项目关联。 | C 级主题入口；不写项目级传播规模。 |

## YouTube 观察

| 视频 / 入口 | 抓取时信号 | 讨论点与评价 |
| --- | --- | --- |
| [Claude Code Plan Mode Plugin - Plannotator](https://www.youtube.com/watch?v=a_AT7cEN_9I) | YouTube oEmbed 可识别标题与作者 `Michael`；上游 README 直接引用。 | 官方演示可帮助理解 plan review surface，不是独立可用性、安全或采用率评测。 |
| [Pi Coding Agent - Visual Plan Mode Extension](https://www.youtube.com/watch?v=XqFun9XCXPw) | YouTube oEmbed 可识别标题与作者 `Michael`；上游 README 标为 Pi plan review demo。 | 展示同一批注模型进入 Pi；不证明跨宿主 hook 与反馈语义完全一致。 |
| [Plannotator - OpenCode Plugin for interactive planning](https://www.youtube.com/watch?v=_N7uo0EFI-U) | YouTube oEmbed 可识别标题与作者 `Michael`；OpenCode plugin README 直接引用。 | 提供 OpenCode 适配入口；本轮无法稳定读取日期、views 或 likes，因此不做同日热度排序。 |
| [Memoh 搜索](https://www.youtube.com/results?search_query=Memoh+AI+agent)、[Weave Router 搜索](https://www.youtube.com/results?search_query=Weave+Router+AI)、[Block Buzz 搜索](https://www.youtube.com/results?search_query=Block+Buzz+AI+agents)、[skill-up 搜索](https://www.youtube.com/results?search_query=Alibaba+skill-up+Agent+Skills) | 搜索入口；结果随时间、地区、账号与排序变化。 | C 级发现入口；没有把宽泛主题视频写成具体项目采用或独立验证。 |

YouTube oEmbed 只能稳定确认这三条视频的标题、作者和可访问性；本轮 player metadata 被登录 / bot check 限制，因此不编造日期、播放量或点赞数，也不与 GitHub stars、X 或 Instagram 指标合并。

## 跨平台综合观察

- GitHub 仍是今天唯一具有统一短期数值口径的平台；X 只有一条上游引用旧帖与若干 profile，Instagram 只有 topic，YouTube 只有同一作者的三条 Plannotator 演示，因此不存在“八项目四平台同步爆发”的证据。
- Agent 工程热点从单一聊天 / coding loop 分解为 context graph、human review、persistent workspace、communication substrate、model router 与 skill eval；这些层都可能记录 prompt、代码、凭据和工具副作用，必须先画数据流与 authority map。
- `local-first`、`self-hosted`、`workspace container`、`signed event`、`audit log` 与 `official plugin` 是不同机制标签，不能互相替代安全、隐私、正确性或合规结论。
- 上游主动公开限制是正面信号：code-review-graph 标注 benchmark circularity，Router 给出负向 / 持平对照，Buzz 标注未完成和无 rate limit，Power Platform Skills 说明 telemetry 差异；选型时应把这些限制保留在结论里。

## 后续跟踪

- 在固定大型仓库对比 code-review-graph、grep / LSP 与人工 ground truth，复跑 token、F1、延迟和配置写入。
- 用专用系统用户、测试浏览器 profile 与低额度 key 验证 cc-haha 的 Worktree、权限、Computer Use、H5 / IM 和清理路径。
- 在副本仓库测试 Plannotator 的 minimal install、hook、Ask AI、分享与卸载，检查批注是否被 Agent 完整理解。
- 用两个测试用户 / Bot 对 Memoh 做 workspace、memory、network、credential、渠道和资源上限对抗测试。
- 按 Weave benchmark harness 先 smoke 后 full run，同时报告 pass、置信区间、费用口径、wall time 与失败分类。
- 给 skill-up 保留隐藏 holdout，并区分“修 Skill”和“修 eval”的人工审批；judge 与被测模型尽量分离。
- 给 Buzz relay 外置限流，测试跨 community 搜索、异步 audit 失败、workflow stub、Agent crash 与 Git policy。
- 在非生产 Power Platform tenant 手工安装单插件，默认关闭 telemetry transmission，验证 RBAC、flow 幂等、rollback 与本地 mirror。

## 来源与证据等级

- **A：平台原始页**——GitHub Trending、八个仓库 REST API、README、docs、release、manifest 与 LICENSE，以及 YouTube oEmbed 返回的标题 / 作者。
- **B：可回溯直接页面**——项目 README / 博客引用的 X 原帖、项目与作者 profile、上游直接引用的演示视频；用于理解发布与传播，不替代安装、benchmark、安全或隐私验证。
- **C：间接信号**——X profile、YouTube 搜索和 Instagram topic 入口；未取得项目级指标时只保留线索，不据此编写采用、收益或传播规模结论。
