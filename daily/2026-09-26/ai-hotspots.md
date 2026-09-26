<!-- markdownlint-disable MD013 -->

# 2026-09-26 AI 热点日报

> 抓取时间：2026-09-26（Asia/Shanghai）。GitHub Trending 的 `stars today` 是抓取时点的短期公开关注信号；stars、forks、open issues、release、tag、manifest、许可证和更新时间来自 GitHub REST API / 上游文件快照，后续会变化。`search-layer` CLI 对最近 24 小时 GitHub AI 项目、Agent 开发工具和 2026-09-26 Trending 的三组查询返回 0 条可用结果，因此发现透明降级到 GitHub 官方综合及 Python / TypeScript / JavaScript / Go / Rust / Jupyter Notebook / C++ Trending，再以 REST API、README、docs、security、release、manifest 与 LICENSE 复核。X、Instagram、YouTube 没有统一可比的项目级口径，本报只记录可交叉识别的上游账号、oEmbed 可核验视频和动态搜索 / 标签入口，不把 GitHub stars 换算为社媒热度。

## 今日判断

- `openrig` 与 `desktop-cc-gui` 都在聚合多种 coding-agent harness：前者偏声明式团队拓扑和恢复，后者偏跨引擎桌面交互。控制面提升可见性，但不会自动收窄底层 CLI 的 shell、Git、网络、provider 或 secret 权限。
- `follow-builders` 将 X、YouTube 与博客的抓取集中为公共 feed，降低个人 API 成本，也把来源选择、抓取完整性、prompt injection 和中心服务可用性集中到新的信任边界。
- `Pentest-Swarm-AI` 的约 +34 当日 stars 是高风险工具信号而非能力证明；上游明确将 swarm、dashboard 等标为 alpha，真实目标只能在书面授权 scope 内测试。
- `nobodywho` 与 `audio.cpp` 分别把本地多模态 LLM、跨平台 binding 和广泛音频模型统一到原生 runtime；代码许可、模型权重、backend 覆盖、设备性能和生成内容权利必须分层验证。
- `ai-usagebar` 解决多 provider 额度观察，但会读取或刷新多个 CLI / Keychain 的高价值凭据；usage endpoint 与配额口径也可能随服务变化。
- `tick-stock-panel` 将数据路由、因子、回测、监控和只读 AI 助手收进本地量化工作台；回测、模型分析和数据供应商输出均不构成投资建议或真实收益证明。
- 八个项目均未在本机安装、运行或接入真实账号 / 数据；正确性、隔离、性能、隐私、安全和生产可用性只按静态上游证据记录。

## GitHub 热点项目

| 项目 | 可核验信号 | 分类 | 评价 |
| --- | --- | --- | --- |
| [openrig](../../projects/openrig/README.md) | 官方 TypeScript Trending 约 +80 当日 stars；API 快照 454 stars、59 forks、31 open issues，Apache-2.0，Release `v0.5.15`。 | Agent 框架与技能生态 | 用 RigSpec、稳定 seat、tmux、daemon、队列和快照编排 Claude Code / Codex；会写用户级 trust、hooks 与 skills，必须先在专用用户中审计。 |
| [desktop-cc-gui](../../projects/desktop-cc-gui/README.md) | 官方 TypeScript Trending 约 +16；API 快照 4,383 stars、396 forks、310 open issues；Release `v1.0.9`、package `1.1.0`；README 称 MIT，但根 LICENSE 缺失。 | Coding Agents 与终端助手 | 专用 protocol adapter 汇总十类 CLI 的 session、permission、provider 和 Git UI；GUI 不是 sandbox，各引擎能力与风险并不一致。 |
| [follow-builders](../../projects/follow-builders/README.md) | 官方 JavaScript Trending 约 +7；API 快照 6,794 stars、887 forks、57 open issues；无 Release / tag，README 称 MIT，但根 LICENSE 缺失。 | 办公、商业与行业应用 | 以中心 feed 向本地 Agent 提供 X / YouTube / blog digest；来源策展、转录、中心 feed 和消息交付需要 provenance 与注入防护。 |
| [Pentest-Swarm-AI](../../projects/Pentest-Swarm-AI/README.md) | 官方 Go Trending 约 +34；API 快照 2,622 stars、480 forks、15 open issues，AGPL-3.0，Release `v0.2.26`。 | 办公、商业与行业应用 | 共享 blackboard、pheromone 与真实安全工具构成 alpha 级 offensive swarm；只可在授权靶场使用，默认服务配置也须加固。 |
| [nobodywho](../../projects/nobodywho/README.md) | 官方 Rust Trending 约 +30；API 快照 1,414 stars、87 forks、20 open issues，EUPL-1.2；bindings 独立发布。 | 模型、训练与推理基础设施 | 以 Rust core、llama.cpp、ONNX Runtime 向 Python / Kotlin / Swift / RN / Flutter / Godot 暴露本地多模态推理；版本、模型和设备矩阵须固定。 |
| [ai-usagebar](../../projects/ai-usagebar/README.md) | 官方 Rust Trending 约 +12；API 快照 575 stars、122 forks、5 open issues，MIT，Release `v1.25.0`。 | Coding Agents 与终端助手 | 统一显示 Claude、Codex、Copilot、OpenRouter 等用量；凭据读取 / refresh、非公开 endpoint 和 Keychain ACL 是关键边界。 |
| [tick-stock-panel](../../projects/tick-stock-panel/README.md) | 官方综合 / Python Trending 约 +44；API 快照 5,159 stars、1,259 forks、17 open issues，MIT；无 Release、tag `v0.3.1`、`VERSION=v0.2.2`。 | 办公、商业与行业应用 | 自托管 A 股数据、策略、回测、监控与 AI 问答闭环；数据源、版本漂移、样本外验证和非投资建议边界须显式保留。 |
| [audio.cpp](../../projects/audio.cpp/README.md) | 官方 C++ Trending 约 +23；API 快照 3,031 stars、344 forks、19 open issues；API `NOASSERTION`、根 Apache-2.0，Release `v0.8.2-audio8-perf-hotfix`。 | 语音、视频与多模态 | 用 ggml 统一 80+ 音频模型 family 的 CLI / server / WebUI；权重许可、声音同意、backend 差异与作者性能数字需逐模型复核。 |
| `paperclip`、`hindsight`、`starnet`、`univer`、`Model-Optimizer`、`superpowers`、`skills`、`claude-plugins-official`、`orca`、`open-seo`、`youtube-automation-agent`、`deja-vu`、`RuView`、`hydradb`、`liteparse`、`buzz`、`stable-diffusion.cpp`、`spirula-studio` 等 | 官方综合 / Python / TypeScript / JavaScript / Go / Rust / C++ Trending 再次出现。 | 既有分类 | 均已有项目页或历史记录，本轮不重复建档。`google/ax` 仍是同名不同上游冲突：`projects/ax` 指向 `Necmttn/ax`，在 owner-aware key 落地前不覆盖；`BuilderIO/skills` 同样不覆盖既有 `projects/skills`。通用网络、媒体和系统工具不因榜位强行收录。 |

以上可回到 [GitHub Trending](https://github.com/trending)、[Python Trending](https://github.com/trending/python?since=daily)、[TypeScript Trending](https://github.com/trending/typescript?since=daily)、[JavaScript Trending](https://github.com/trending/javascript?since=daily)、[Go Trending](https://github.com/trending/go?since=daily)、[Rust Trending](https://github.com/trending/rust?since=daily)、[Jupyter Notebook Trending](https://github.com/trending/jupyter-notebook?since=daily)、[C++ Trending](https://github.com/trending/c%2B%2B?since=daily) 与各项目 [API：openrig](https://api.github.com/repos/mvschwarz/openrig)、[desktop-cc-gui](https://api.github.com/repos/zhukunpenglinyutong/desktop-cc-gui)、[follow-builders](https://api.github.com/repos/zarazhangrui/follow-builders)、[Pentest-Swarm-AI](https://api.github.com/repos/Armur-Ai/Pentest-Swarm-AI)、[nobodywho](https://api.github.com/repos/nobodywho-ooo/nobodywho)、[ai-usagebar](https://api.github.com/repos/akitaonrails/ai-usagebar)、[tick-stock-panel](https://api.github.com/repos/shy3130/tick-stock-panel)、[audio.cpp](https://api.github.com/repos/0xShug0/audio.cpp) 复核。

## X 观察

| 入口 | 讨论点与评价 | 可复核状态 |
| --- | --- | --- |
| [@zarazhangrui](https://x.com/zarazhangrui) | Follow Builders 的维护者账号也是默认 feed 来源之一；可观察来源策展与 digest 设计讨论，但不能证明中心 feed 完整、中立或及时。 | B 级上游账号；GitHub user profile 可交叉识别，只证明身份入口存在，未取得同日项目级原帖或统一互动量。 |
| [@armur_ai](https://x.com/armur_ai)、[@nobodywho_ai](https://x.com/nobodywho_ai)、[@akitaonrails](https://x.com/akitaonrails) | 分别对应 offensive-security swarm、本地推理 SDK 和 usage monitor；可跟踪发布、兼容性和安全讨论。 | B 级上游账号；GitHub organization / user profile 提供同名 X 字段，未将动态 followers / views 写入热度。 |
| [OpenRig 搜索](https://x.com/search?q=%22mvschwarz%2Fopenrig%22&src=typed_query)、[Desktop CC GUI 搜索](https://x.com/search?q=%22desktop-cc-gui%22&src=typed_query)、[TSP 搜索](https://x.com/search?q=%22tick-stock-panel%22&src=typed_query)、[audio.cpp 搜索](https://x.com/search?q=%220xShug0%2Faudio.cpp%22&src=typed_query) | 用于发现 agent 控制面、桌面 CLI、量化研究与本地音频 runtime 的实际反馈。 | C 级动态搜索入口；排序受登录、地区与推荐影响，未据搜索壳层声称采用率、性能、安全性或投资效果。 |

## Instagram 观察

| 入口 | 讨论点与评价 | 可复核状态 |
| --- | --- | --- |
| [`aiagents`](https://www.instagram.com/explore/tags/aiagents/)、[`codingagents`](https://www.instagram.com/explore/tags/codingagents/) | 对应 OpenRig、Desktop CC GUI 与 Follow Builders 的 Agent / coding 主题；宽泛标签常混入课程、产品广告和无法复现实例。 | C 级主题入口；抓取时均 HTTP 200，但 `codingagents` 重定向登录，未取得可独立映射到本轮项目的稳定帖子或互动量。 |
| [`cybersecurity`](https://www.instagram.com/explore/tags/cybersecurity/)、[`localllm`](https://www.instagram.com/explore/tags/localllm/) | 对应 Pentest Swarm 与 NobodyWho；短演示不证明授权、scope enforcement、推理质量或设备兼容。 | C 级热门标签入口；抓取时 HTTP 200，内容排序和项目关联不稳定。 |
| [`quantitativeanalysis`](https://www.instagram.com/explore/tags/quantitativeanalysis/)、[`voiceai`](https://www.instagram.com/explore/tags/voiceai/) | 对应 TSP 与 audio.cpp；收益截图和生成音频通常缺少数据口径、模型、seed、声音同意及许可证。 | C 级主题入口；抓取时均 HTTP 200，但 `quantitativeanalysis` 重定向登录，未据标签内容推断项目级热度或结果真实性。 |

## YouTube 观察

| 入口 | 讨论点与评价 | 可复核状态 |
| --- | --- | --- |
| [I Run A Cross-Harness Fleet As A Software Factory](https://www.youtube.com/watch?v=KlzyePs3bSk) | OpenRig 上游频道展示跨 harness fleet 的产品叙事，可辅助理解 topology / seat / software-factory 工作流；不是权限、恢复、生产吞吐或软件质量的独立验证。 | B 级上游视频；README 链接频道，YouTube oEmbed 可核验标题与作者 `OPENRIG`，未把动态 views / likes 纳入排名。 |
| [Follow Builders 默认播客清单](https://github.com/zarazhangrui/follow-builders#default-sources) | 上游 README 明列 Latent Space、No Priors、Training Data 等 YouTube 来源，证明默认策展范围，不证明每期 transcript 完整、授权或摘要准确。 | B 级上游配置入口；可读取固定频道 / playlist 链接，但未逐视频核验 feed 收录和转录质量。 |
| [Pentest Swarm 搜索](https://www.youtube.com/results?search_query=Pentest+Swarm+AI+Armur)、[NobodyWho 搜索](https://www.youtube.com/results?search_query=NobodyWho+on-device+AI)、[ai-usagebar 搜索](https://www.youtube.com/results?search_query=ai-usagebar)、[TSP 搜索](https://www.youtube.com/results?search_query=tick-stock-panel)、[audio.cpp 搜索](https://www.youtube.com/results?search_query=audio.cpp+ggml) | 用于观察安装、模型 / backend、靶场、量化工作流和额度面板反馈。 | C 级动态搜索入口；未取得可由上游交叉识别且与今日相关的统一项目视频，不编造日期、播放量或项目关联。 |

## 评价与争议

1. **控制面不是权限边界。** OpenRig、Desktop CC GUI 与 usage monitor 都让多工具更易操作，却也汇集 trust、hooks、session、OAuth、Keychain 和 provider；可见性增加不等于 blast radius 缩小。
2. **中心化 feed 用便利交换可审计性。** Follow Builders 省去了个人 X / YouTube API，但用户需要信任来源表、转录、去重、更新节奏和 feed 服务；原始链接与抓取时间必须随摘要保留。
3. **offensive Agent 的“scope”必须对抗验证。** Pentest Swarm 的法律免责声明、双层 scope check 和 cleanup 都是有价值设计，但 DNS、redirect、代理、子进程、错误配置和模型 prompt injection 仍可能越界。
4. **local / self-hosted 仍然有网络与供应链。** NobodyWho 的模型下载、audio.cpp 的 model manager、TSP 的数据源 / LLM、OpenRig 的 provider / MCP 和 ai-usagebar 的 usage endpoints 都会连接外部系统。
5. **发布版本位于不同平面。** Desktop CC GUI 的 Release / package、NobodyWho 的各 binding、TSP 的 tag / VERSION、audio.cpp 的 hotfix / 正式 tag 都要求把文档、源码和 artifact 固定到同一 commit。
6. **代码许可证不覆盖权重、内容和数据。** audio.cpp / NobodyWho 的模型、Follow Builders 的帖子 / transcript、TSP 的行情、桌面 Agent 生成代码和 provider 服务条款均需独立审查。

## 证据等级与方法

- A 级：GitHub 官方 Trending、GitHub REST API、上游 README / docs / security / manifest / release / tag / LICENSE。
- B 级：README / GitHub profile 可交叉识别的上游社媒账号、固定来源表，或标题 / 作者可由 YouTube oEmbed 核验的上游视频；只证明入口 / 内容存在，不证明同日热度或主张已独立复现。
- C 级：X / Instagram / YouTube 动态搜索和主题标签，只作观察入口，不用于项目级排名或互动量结论。
- 本次未安装、运行、登录或向任何项目写入真实数据；未验证 Agent 权限、摘要正确性、渗透能力、模型性能、provider usage、量化收益、声音权利与生产可用性。

## 本次仓库更新

- 新增 8 个项目说明：`openrig`、`desktop-cc-gui`、`follow-builders`、`Pentest-Swarm-AI`、`nobodywho`、`ai-usagebar`、`tick-stock-panel`、`audio.cpp`。
- 全部归入现有分类；未新增首页分类。
- 首页最新日报更新为 2026-09-26，项目总数按 `projects/` 实际目录重算为 `739`。
- `google/ax`、`BuilderIO/skills` 作为同名冲突候选继续只在日报记录，不覆盖现有不同上游项目页。
