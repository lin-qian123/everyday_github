<!-- markdownlint-disable MD013 -->

# 2026-09-22 AI 热点日报

> 抓取时间：2026-09-22（Asia/Shanghai）。GitHub Trending 的 `stars today` 是抓取时点的短期公开关注信号；stars、forks、open issues、release、许可证和更新时间来自 GitHub REST API / 上游文件快照，后续会变化。`search-layer` CLI 对近一周 GitHub AI、Agent 新闻、X 与 YouTube 的四组扩展查询返回 0 条可用结果，通用 Web 检索主要返回 GitHub 官方页、聚合榜和既有项目资料，因此发现透明降级到 GitHub 官方综合及 Python / TypeScript / JavaScript / Go / Rust Trending，再用 API、README、docs、release、manifest 与 LICENSE 复核。X、Instagram、YouTube 没有统一可比的项目级口径，本报只记录上游可交叉识别账号、视频与动态搜索 / 标签入口，不把 GitHub stars 换算成社媒热度。

## 今日判断

- `substrate` 与 `destructive_command_guard` 分别把 Agent 安全问题放在执行基础设施与命令入口处理：前者面向高密度 sandbox / snapshot / routing，后者在 hook 阶段阻止已知危险命令。二者都不能替代最小权限、备份、网络策略和人工批准。
- `thinking-orbs` 反映 Agent 产品正在把“工作、检索、连接、创作”做成可区分的 UI 状态；动效仍只是应用状态映射，不能证明真实进度或模型内部过程。
- `Crucix` 把多源 OSINT、变化检测和可选 LLM 分析放进本地 dashboard，但“zero cloud”不能覆盖外部 feed、模型和消息平台的数据流；高关注回潮也发生在默认分支数月未更新的背景下。
- `PanWatch` 与 `easyeda-agent` 展示 Agent 向金融和 EDA 高后果行业流程延伸：前者的多 Agent 辩论不是持牌投资建议，后者的软件 DRC / 回读也不是实物电气、安规、EMC 或可制造性认证。
- `New API` 将多模型协议、路由、认证、配额和计费集中起来；集中化同时扩大了密钥、日志、账单与协议转换错误的影响半径。
- `claude-code-templates` 把 agents、hooks、MCP、skills 与 settings 做成第三方组件目录；易安装并不等于每个组件同来源、同许可或已完成安全审计。
- 八个项目均未在本机安装、运行或接入真实账号 / 数据；功能、安全、隐私、性能、投资与工程质量只按静态上游证据记录。

## GitHub 热点项目

| 项目 | 可核验信号 | 分类 | 评价 |
| --- | --- | --- | --- |
| [substrate](../../projects/substrate/README.md) | 官方 Go Trending 约 +438 当日 stars；API 快照 2,595 stars、357 forks、521 open issues，Apache-2.0，`v0.1.0`。 | Agent 框架与技能生态 | actor / worker 复用、快照与路由切中 stateful Agent 执行成本；threat model 明写当前实现几乎未安全加固，性能与隔离都需独立复现。 |
| [thinking-orbs](../../projects/thinking-orbs/README.md) | 官方 TypeScript Trending 约 +203；API 快照 3,107 stars、249 forks、20 open issues，MIT，无 GitHub Release，最后 push 2026-08-16。 | 前端、UI 与 Agent 交互层 | 九种 Canvas 2D 状态、reduced motion 与不可见暂停适合产品界面；状态动画不是进度或真实推理证据。 |
| [Crucix](../../projects/Crucix/README.md) | 官方 JavaScript Trending 约 +37；API 快照 11,837 stars、1,840 forks、79 open issues，AGPL-3.0，无 Release，最后 push 2026-05-20。 | RAG、检索与知识处理 | 27 源 OSINT、delta、告警与 rule / LLM fallback 便于监控；来源误差、外部数据流和交易建议须严格分层。 |
| [easyeda-agent](../../projects/easyeda-agent/README.md) | 官方 Go Trending 约 +13；API 快照 499 stars、67 forks、15 open issues，API `NOASSERTION`、根 MIT 且局部 Apache-2.0，`v1.5.2`。 | 办公、商业与行业应用 | typed actions、写前守卫与写后回读优于坐标点击；无通用 undo，DRC 不等于实物和生产验证。 |
| [PanWatch](../../projects/PanWatch/README.md) | 官方 Python Trending 约 +45；API 快照 1,156 stars、252 forks、63 open issues，MIT，`0.14.0`。 | 办公、商业与行业应用 | 持仓、规则、Agent、模拟盘和通知形成统一工作台；行情 / 模型误差与金融合规边界不能由“多 Agent 风控”代替。 |
| [new-api](../../projects/new-api/README.md) | 官方 Go Trending 约 +103；API 快照 48,610 stars、11,664 forks、1,338 open issues，AGPL-3.0，`v1.0.0-rc.40`。 | 模型、训练与推理基础设施 | 多协议、路由、配额与计费集中管理实用；协议转换、密钥 / 日志集中和公网转售义务是核心风险。 |
| [claude-code-templates](../../projects/claude-code-templates/README.md) | 官方 Python Trending 约 +45；API 快照 30,891 stars、3,521 forks、261 open issues，MIT，`v1.29.6`。 | Coding Agents 与终端助手 | 组件目录和安装 CLI 提高 Claude Code 扩展可发现性；第三方 hook / MCP / skill 必须逐项做来源、权限与许可审计。 |
| [destructive_command_guard](../../projects/destructive_command_guard/README.md) | 官方 Rust Trending 约 +11；API 快照 6,032 stars、246 forks、11 open issues，API `NOASSERTION`，自定义 OpenAI / Anthropic rider，`v0.14.4`。 | Coding Agents 与终端助手 | 多 Agent pre-tool 命令护栏有实际价值；规则会误报 / 漏报，且非标准许可对采用主体有实质限制。 |
| `cua`、`OpenStock`、`agent-native`、`financial-services`、`ai-memory`、`coder`、`autoclip`、`project-nomad`、`docling`、`book-to-skill`、`browser-use`、`json-render`、`open-science`、`OpenCreator`、`claude-code`、`pi`、`agent-skills`、`webcodex`、`Codex-X`、`multica`、`openhuman`、`ragflow`、`tunnel-client`、`awesome-free-llm-apis`、`lark-cli` 等 | 官方综合 / Python / TypeScript / JavaScript / Go / Rust Trending 再次出现。 | 既有分类 | 均已有项目页或历史记录，本轮不重复建档。`Leonxlnx/taste-skill` 是新上榜的同名不同上游，但 `projects/taste-skill` 已指向 `KOHbDS/taste-skill`；在 owner-aware key 落地前不覆盖旧目录。 |

以上可回到 [GitHub Trending](https://github.com/trending)、[Python Trending](https://github.com/trending/python?since=daily)、[TypeScript Trending](https://github.com/trending/typescript?since=daily)、[JavaScript Trending](https://github.com/trending/javascript?since=daily)、[Go Trending](https://github.com/trending/go?since=daily)、[Rust Trending](https://github.com/trending/rust?since=daily) 与各项目 [API：substrate](https://api.github.com/repos/agent-substrate/substrate)、[thinking-orbs](https://api.github.com/repos/Jakubantalik/thinking-orbs)、[Crucix](https://api.github.com/repos/calesthio/Crucix)、[easyeda-agent](https://api.github.com/repos/zhoushoujianwork/easyeda-agent)、[PanWatch](https://api.github.com/repos/TNT-Likely/PanWatch)、[new-api](https://api.github.com/repos/QuantumNous/new-api)、[claude-code-templates](https://api.github.com/repos/davila7/claude-code-templates)、[destructive_command_guard](https://api.github.com/repos/Dicklesworthstone/destructive_command_guard) 复核。

## X 观察

| 入口 | 讨论点与评价 | 可复核状态 |
| --- | --- | --- |
| [@crucixmonitor](https://x.com/crucixmonitor) | Crucix README 直接链接的项目账号，可继续跟踪 source health、告警与 token 冒名提醒。 | B 级上游账号；入口可访问，但本轮未取得同日项目帖或统一 views / likes / reposts，账号存在不等于项目今天在 X 高热。 |
| [Agent Substrate 搜索](https://x.com/search?q=%22Agent%20Substrate%22&src=typed_query)、[DCG 搜索](https://x.com/search?q=%22Destructive%20Command%20Guard%22&src=typed_query) | 对应 Agent sandbox 密度、snapshot 隔离与 coding-agent 命令护栏两条基础设施讨论线。 | C 级动态搜索入口；排序受登录、地区和推荐影响，未据搜索页声称采用率、安全性或传播规模。 |
| [easyeda-agent 搜索](https://x.com/search?q=%22easyeda-agent%22&src=typed_query)、[PanWatch 搜索](https://x.com/search?q=PanWatch%20TradingAgents&src=typed_query)、[New API 搜索](https://x.com/search?q=%22QuantumNous%2Fnew-api%22&src=typed_query) | 用于观察 EDA 自动化、AI 金融工作台和多模型 gateway 的真实使用反馈。 | C 级动态搜索入口；本轮未取得可稳定复核的项目级同日原帖和互动量。 |

## Instagram 观察

| 入口 | 讨论点与评价 | 可复核状态 |
| --- | --- | --- |
| [`aiagents`](https://www.instagram.com/explore/tags/aiagents/)、[`generativeui`](https://www.instagram.com/explore/tags/generativeui/) | 与 substrate、thinking-orbs、claude-code-templates 的 Agent infra / UI 主题相关；宽泛标签会混入品牌营销和无上游关联内容。 | C 级主题入口；抓取时 `aiagents` 可访问，`generativeui` 返回 429，未取得项目级帖子或同口径互动量。 |
| [`fintech`](https://www.instagram.com/explore/tags/fintech/)、[`pcbdesign`](https://www.instagram.com/explore/tags/pcbdesign/) | 分别对应 PanWatch / New API 的金融与平台侧议题、easyeda-agent 的 PCB 工程内容；主题热度不能反推项目热度。 | C 级宽泛标签入口；页面可访问但排序随账号、地区和算法变化，本报不记录动态库存数。 |

## YouTube 观察

| 入口 | 讨论点与评价 | 可复核状态 |
| --- | --- | --- |
| [Agent Substrate OSS Launch Demo](https://www.youtube.com/watch?v=ZEzkCFJkzjY)、[上游频道](https://www.youtube.com/@agent-substrate) | README 以该视频展示约 250 actors 复用 8 pods、暂停 / 恢复与状态保留；它是理解架构的直接演示，不是独立第三方 benchmark。 | B 级上游视频；YouTube oEmbed 可核验标题和作者为 `agent-substrate`，本轮未记录动态 views / likes。 |
| [Crucix 搜索](https://www.youtube.com/results?search_query=Crucix+AI+intelligence)、[PanWatch 搜索](https://www.youtube.com/results?search_query=PanWatch+TradingAgents)、[easyeda-agent 搜索](https://www.youtube.com/results?search_query=easyeda-agent) | 用于发现 dashboard、金融分析和 EDA 操作演示，后续应区分上游 demo、第三方复现和只读 README 的自动视频。 | C 级动态搜索入口；本轮定向 Web 搜索没有返回可独立核验的近期项目视频，未编造日期或播放量。 |
| [Claude Code hooks 搜索](https://www.youtube.com/results?search_query=Claude+Code+hooks+skills+MCP)、[AI gateway 搜索](https://www.youtube.com/results?search_query=self-hosted+AI+gateway+OpenAI+Anthropic+Gemini) | 对应 claude-code-templates / DCG 的扩展供应链与 New API 的协议路由；搜索结果只能作为话题观察，不能代替项目文档。 | C 级主题搜索入口；结果动态、品牌词噪声高，没有构造跨平台排名。 |

## 评价与争议

1. **安全口号与当前成熟度要拆开。** Substrate README 写 secure-by-default，但 threat model 同时承认当前实现几乎没有安全加固；应以版本化 threat closure 和对抗测试为准。
2. **本地托管不是零外发。** Crucix、PanWatch、New API 和 claude-code-templates 都能本地运行，但外部 feed、provider、通知、MCP、tunnel 与 telemetry 会重新引入第三方边界。
3. **Agent 进入行业工具后，软件检查不是专业签字。** EDA 的 DRC、金融的 Agent debate、OSINT 的 confidence 都只覆盖部分错误类型，不能替代工程师、投顾 / 合规或一手来源复核。
4. **供应链便利与执行权限同步增加。** 一键安装 templates、hooks、MCP、connector 和 shell guard 越方便，越要固定版本、保留 diff、审计许可与验证卸载 / 回滚。
5. **许可证标签不能只看 API。** easyeda-agent 的 API 是 `NOASSERTION` 但根目录给出 MIT + 局部 Apache-2.0；DCG 同样是 `NOASSERTION`，实际却是含公司排除 rider 的自定义条款，两者都需要读正文。
6. **同名仓库仍是索引结构问题。** 新 `Leonxlnx/taste-skill` 不能覆盖既有 `KOHbDS/taste-skill`；在 owner-aware key 确定前，宁可日报保留候选也不破坏旧链接。

## 证据等级与方法

- A 级：GitHub 官方 Trending、GitHub REST API、上游 README / docs / manifest / release / LICENSE、可由 oEmbed 验证的上游视频。
- B 级：README 直接链接的项目社媒账号或视频，只证明入口归属，不证明同日热度或主张已独立复现。
- C 级：X / Instagram / YouTube 动态搜索和主题标签，只作观察入口，不用于项目级排名或互动量结论。
- 本次未安装、运行、登录或向任何项目写入数据；未验证 benchmark、生成质量、投资表现、PCB 实物、协议等价、安全隔离和生产可用性。

## 本次仓库更新

- 新增 8 个项目说明：`substrate`、`thinking-orbs`、`Crucix`、`easyeda-agent`、`PanWatch`、`new-api`、`claude-code-templates`、`destructive_command_guard`。
- 全部归入现有分类；未新增首页分类。
- 首页最新日报更新为 2026-09-22，项目总数按 `projects/` 实际目录重算为 `711`。
- `Leonxlnx/taste-skill` 作为同名冲突候选保留在日报，不覆盖既有项目页。
