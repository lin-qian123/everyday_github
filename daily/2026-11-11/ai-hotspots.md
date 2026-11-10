<!-- markdownlint-disable MD013 -->

# AI 热点日报｜2026-11-11

- 采样：2026-11-11（Asia/Shanghai）07 时段。GitHub daily 日增、累计 stars 与视频播放量是分时快照，不是自然日结算；历史发行 / 视频单独标明。
- 范围：官方综合、Python、TypeScript、Rust、Go、JavaScript、C++、Swift、Jupyter Notebook 九页；X、Instagram、YouTube 有界观察，不合成跨平台排名。
- 证据：A 为官方榜单 / API / 固定 SHA 文件；B 为平台原生元数据；C 为受限、聚合或同名观察入口。作者成绩、静态核读与实际运行分别表述。
- 获取：广泛搜索主要得到汇总与历史材料，项目定向社媒检索无可用结果；网页工具读取 Trending 受限，改用官方页面直接 HTTP 取得九页。GitHub 连接器核仓库 ID、主线 SHA、发行与引用文件；tags 查询接口不受支持，本轮不作无 tag 判断。无搜索命中不等于没有活动。

## 今日重点

- **游戏工作台要看实际权限**：OhMyGame TypeScript +201；beta.5.5 增插件市场，但原生插件不受 sandbox 限制，编码 CLI 默认模式也较宽。[解读](../../projects/ohmygame/README.md)
- **手机离线聊天与手机 API 分别验**：PocketPal TypeScript +50，UTC 11-10 发 1.23.0，新增本地 API POC；默认关闭 / loopback，LAN 与可选 key 是独立设置。[解读](../../projects/pocketpal-ai/README.md)
- **本机三维重建也有统计出口**：OOOSplat Rust +38；0.7.1 为预发行，默认匿名统计、无逐 Agent 身份的 loopback MCP，以及 macOS 分发哈希状态都需说明。[解读](../../projects/ooosplat/README.md)
- **财务账本的 AI 不止聊天**：Sure 综合 +184；聊天、后台分类和外部 MCP 分开配置，稳定 0.7.6 与 alpha 主线不能混写。[解读](../../projects/sure/README.md)
- **知识 Wiki 的引用与完整性分别审**：Claude Quickstarts 综合 +530；原位更新到当前动态工作流与 Daily Brief，保留作者披露的共享页覆盖、语料和成本条件。[解读](../../projects/claude-quickstarts/README.md)

## GitHub 热点项目

日增来自指定官方 daily 页；API 为 stars / forks / open issues（含 PR）。“新增”仅指本仓库首次建档，语言榜不是全站排名，stars 不代表部署、质量或安全证明。

| 项目与动作 | 可核热度与发行 | 沿用分类 | 工程观察 |
| --- | --- | --- | --- |
| [sure](../../projects/sure/README.md)，新增 | 综合 +184；11,878 / 886 / 891；[API](https://api.github.com/repos/we-promise/sure)；稳定 [v0.7.6](https://github.com/we-promise/sure/releases/tag/v0.7.6)，UTC 10-31；最新 [11-10 alpha](https://github.com/we-promise/sure/releases/tag/v2026.11.10-alpha)另列。 | 办公、商业与行业应用 | AI 双流水线、MCP read_write、Langfuse 内容、端口 / secret 与完整恢复。 |
| [ohmygame](../../projects/ohmygame/README.md)，新增 | TypeScript +201；2,033 / 257 / 25；[API](https://api.github.com/repos/WhiteTowerAI/ohmygame)；[beta.5.5](https://github.com/WhiteTowerAI/ohmygame/releases/tag/v0.0.0-beta.5.5)，UTC 11-06，预发行。 | 办公、商业与行业应用 | 原生插件 / UI 不同边界、CLI 默认权限、开环试玩、遥测与发布。 |
| [pocketpal-ai](../../projects/pocketpal-ai/README.md)，新增 | TypeScript +50；9,183 / 1,066 / 126；[API](https://api.github.com/repos/a-ghorbani/pocketpal-ai)；[v1.23.0](https://github.com/a-ghorbani/pocketpal-ai/releases/tag/v1.23.0)，UTC 11-10。 | 前端、UI 与 Agent 交互层 | 本地 / 远端 / 语音出口，API POC、Plus gate、LAN 与可选 key。 |
| [ooosplat](../../projects/ooosplat/README.md)，新增 | Rust +38；2,439 / 288 / 25；[API](https://api.github.com/repos/ooolabdev/ooosplat)；[0.7.1](https://github.com/ooolabdev/ooosplat/releases/tag/0.7.1)，UTC 10-28，预发行。 | 语音、视频与多模态 | COLMAP / Brush 后端分离、OOM 重试、统计、macOS 清单与几何 / 导出。 |
| [claude-quickstarts](../../projects/claude-quickstarts/README.md)，原位刷新 | 综合 / Python +530；20,464 / 3,468 / 241；[API](https://api.github.com/repos/anthropics/claude-quickstarts)；发行列表为空，UTC 11-06 主线更新 Wiki。 | AI 学习与教育资源 | 动态工作流、共享页内容丢失、混合语料、成本与 Daily Brief 权限。 |

- 去重：按实际目录、完整 owner/repo 链接及本轮五个唯一仓库 ID 核对，四个新目录、一个原位刷新；实际目录 1,019 → 1,023。Sure 为 Maybe 社区 fork，是独立仓库；同名 skills 问题继续保留，不覆盖旧页。
- 已有高热：综合 Astryx +3,111、Anthropic skills +1,676、agent-browser +775，Python HA-MCP +792；本轮仅记录榜单，未据此重审实现或推断增长原因。
- 选择为有界选样：Sherlock、Topcoat 等不因高日增就归入 AI 核心项目。Sure 以带可选 AI 的财务应用收录；OOOSplat 以视觉重建流水线收录，不混同文本生成模型。
- 官方榜单：[综合](https://github.com/trending?since=daily)、[Python](https://github.com/trending/python?since=daily)、[TypeScript](https://github.com/trending/typescript?since=daily)、[Rust](https://github.com/trending/rust?since=daily)、[Go](https://github.com/trending/go?since=daily)、[JavaScript](https://github.com/trending/javascript?since=daily)、[C++](https://github.com/trending/c++?since=daily)、[Swift](https://github.com/trending/swift?since=daily)、[Jupyter Notebook](https://github.com/trending/jupyter-notebook?since=daily)。

## X 观察

- [OhMyGame 实时搜索](https://x.com/search?q=OhMyGame&f=live)在网页工具返回 403；[PocketPal 搜索](https://x.com/search?q=PocketPal&f=live)与 [OOOSplat 搜索](https://x.com/search?q=OOOSplat&f=live)直接 HTTP 均转登录 onboarding，未读到原帖 / 评论。
- 项目定向搜索也未给出可独立核读的原帖。本轮没有取得作者身份、发帖日期与互动量可同时绑定的帖子，不报告 X 项目排名、当天增量、传播规模或社区共识。
- 这些只是观察入口；下面的工程争议来自固定文档与源码，不包装成 X 正在热议的结论。

## Instagram 观察

- [pocketpal 标签](https://www.instagram.com/explore/tags/pocketpal/)跳转 popular 聚合，标题为约 58K reels；名称可能指不同对象，未确认与 PocketPal AI 的关系。
- [gaussiansplatting 标签](https://www.instagram.com/explore/tags/gaussiansplatting/)也转 popular 聚合，标题约 32K reels；这是宽泛技术主题，不能归给 OOOSplat。
- 本轮无可绑定项目的原帖、作者身份、日期或互动量。聚合数字既不是项目热度也不是当天新增；原帖和评论覆盖仍缺失，未登录或发布。

## YouTube 观察

从原生 [OOOSplat 搜索](https://www.youtube.com/results?search_query=OOOSplat)和 [PocketPal AI 搜索](https://www.youtube.com/results?search_query=PocketPal+AI)读取列表，再以 oEmbed 核标题和作者，watch 页面可达。两条均为第三方历史视频；相对时间不反推精确日期，累计播放不是当天增长。

| 视频 | 可核元数据 | 讨论 / 内容边界 |
| --- | --- | --- |
| [OOOSplat：本地 3DGS 与内存概览](https://www.youtube.com/watch?v=y6BlXnqRIko) | Alex Hitt；294 views、3w ago；[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=y6BlXnqRIko&format=json) 标题 / 作者一致。 | 标题指向工程分析，但未完整观看，不能确认其内存解释或当前 0.7.1 覆盖。 |
| [PocketPal AI 手机设置教程](https://www.youtube.com/watch?v=eGF02pYlcXQ) | Shax Finds；6,956 views、5mo ago；[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=eGF02pYlcXQ&format=json) 标题 / 作者一致。 | 历史入门教程，不代表新 API POC、最新语音栈或 1.23.0 权限行为。 |

OhMyGame 原生搜索本次返回 HTTP 500，保留[查询入口](https://www.youtube.com/results?search_query=OhMyGame)并记录获取失败；不据此判断没有视频。未下载、完整观看、核全部评论或取得每日播放增量。

## 讨论与争议：事实、判断和待验证

下表是来源暴露的工程议题，未采集到足以统计社媒观点分布的评论样本。

| 议题 | 已核事实 | 判断 / 待验证 |
| --- | --- | --- |
| 一人游戏工作室与权限 | OhMyGame 文档说明原生插件完全受信任，CLI 接入默认可不询问。 | 试玩可见不等于隔离或成品质量；须独立审插件、素材权利与核心循环。 |
| 本地模型与网络服务 | PocketPal 本地 API 初始关闭；LAN 可绑定全接口，key 可选；存在 Plus gate。 | 离线聊天、联网工具、手机 API 分项验收；Origin 检查不能代替客户端身份。 |
| 本机重建与隐私 / 尺度 | OOOSplat 默认统计开启，MCP 本地共享权限；导出副本可能调尺度。 | 视觉质量、几何精度、坐标单位、数据出口和平台验证分别检查。 |
| 财务 AI 与账本可信度 | Sure 聊天和后台分类分离，MCP 有写工具；Langfuse 可收提示 / 回复。 | 先以可手算账本验证权限、分类和恢复，不能把自托管视作所有处理本地化。 |
| 引用来源与知识完整性 | Quickstarts Wiki 保留出处 / 冲突，但作者披露最繁忙共享页约 5% 已写行被覆盖；含两份合成辅助文件。 | 需逐源完整性检查和并发冲突测试；作者成本 / 得分不外推到新语料或当前计价。 |
| 自动日报与静默失败 | Daily Brief 文档说明预算触顶暂停，Slack 写范围依 bot 频道成员关系。 | 检查运行状态与实际凭据权限，不能用“没有消息”推断“没有新事项”。 |

具体来源和固定 SHA 入口见对应项目页；没有安装 / 性能 / 权限实测结论。

## 验证范围与接续

- 已核：九页官方 daily、五个唯一仓库 ID / 主线 SHA / 完整目录树、发行状态和各页引用的指定文件。
- 文档验证：五页 35 个固定章节、五个唯一 ID、四类首页入口、1,023 个实际目录与 321 个本地链接通过；68 个范围内外部 URL 有来源 / 访问证据，其中 32 个固定 SHA 文件已读取。X 登录 / 403、Instagram 聚合、OhMyGame YouTube 搜索 500 均按实际缺口记录。8 个 Markdown 文件 lint 零问题；本轮仅纳入 8 个任务文件，保留用户 AGENTS.md 原修改。
- 未做：上游安装 / 构建 / 测试、模型 / 素材下载、手机推理或采音、GPU 重建、人工试玩、全片观看、云 API 调用、账户登录、财务数据接入、MCP 写入、发布游戏或真实权限 / 网络隔离验收。
- 接续：Sure 稳定 / alpha、双 AI 流 / MCP / 恢复；OhMyGame 原生插件 / CLI 默认权 / 完整试玩；PocketPal Plus / LAN / key / 后台和断网；OOOSplat 平台引擎 / 统计 / 尺度；Quickstarts Wiki 并发完整性 / 语料 / 成本和 Daily Brief 暂停 / Slack 权限。skills owner-aware 映射仍待方案。
