<!-- markdownlint-disable MD013 -->

# AI 热点日报｜2026-11-24

- 采样：2026-11-24（Asia/Shanghai）约 06:59–07:07；历史内容、UTC 发行日期与北京时间单列。`stars today` 是榜单滚动快照，API / 阅读 / 播放为累计值，不是自然日结算，不合成跨平台排行榜。
- 范围：综合、Python、TypeScript、JavaScript、Go、Rust、C++、Swift、Jupyter Notebook、Shell 十个官方 daily 页的有界抽样；两项新增、一项原位刷新，不声称穷尽所有新上榜项目。
- 证据：A 为官方榜单、API、固定 SHA 文件与发行；B 为可关联的作者身份 / 视频元数据；C 为搜索、宽泛聚合和受限入口。作者自测、本文静态判断与本轮实跑分别记录。
- 获取：`search-layer` 日内查询无结果；Web 广搜多为聚合、定向搜索主要为历史视频。项目事实以 GitHub 连接器、固定 SHA 文档 / 局部源码和 npm 元数据为准。连接器无法读约 1.7 MB 的 Resolve server 文件，改用原生 HTTP 取得同一 SHA 后局部搜索；没有全仓审计。
- 去重：核对目录、owner/repo、旧名及仓库 ID；CozyClay 旧 owner API 指向相同 ID，续写既有页。保留原 `AGENTS.md` 修改及既有同名项目键 / taste-skill 身份待办。

## 今日重点

- **刚发布的预演工具更新，先看工程兼容和费用。** CozyClay JavaScript +21；3.3.0 北京时间 06:57 发布，移除 storyboard project、更新镜头格式，新增第二 motion writer，面板费用仍不显示它的 tokens。[更新解读](../../projects/CozyClay/README.md)
- **“分析素材”默认可能回写工程。** DaVinci Resolve MCP Python +19；分析默认包括元数据 / 标记发布与宿主视觉模型路径，safe mode 缺省 false，归档保护随 server 模式与动作而异。[新增解读](../../projects/davinci-resolve-mcp/README.md)
- **教程需拆开离线演示、真实云调用和许可。** GenAI_Agents Jupyter Notebook +8；离线 trace fixtures 与真实社媒 API 例子的边界不同，仓库为自定义非商业许可。[新增解读](../../projects/GenAI_Agents/README.md)

## GitHub 热点项目

API 累计依次为 stars / forks / open issues（含 PR）；项目收录日期不代表首次发布。

| 项目与动作 | 本轮可核热度 / 版本 | 沿用分类 | 工程关注 |
| --- | --- | --- | --- |
| [davinci-resolve-mcp](../../projects/davinci-resolve-mcp/README.md)，新增 | Python **+19**；4,312 / 493 / 6；[API](https://api.github.com/repos/samuelgursky/davinci-resolve-mcp)；正式 [v5.4.0](https://github.com/samuelgursky/davinci-resolve-mcp/releases/tag/v5.4.0)，UTC 11-20 03:33。 | 语音、视频与多模态 | Studio / free 分版本，分析写回、safe mode / strict、播放 provider、覆盖率分母。 |
| [GenAI_Agents](../../projects/GenAI_Agents/README.md)，新增 | Jupyter Notebook **+8**；25,095 / 4,200 / 21；[API](https://api.github.com/repos/NirDiamant/GenAI_Agents)；[book-v1.0](https://github.com/NirDiamant/GenAI_Agents/releases/tag/book-v1.0) 为 UTC 10-26 图书发行宣传，非 SDK 稳定版。 | AI 学习与教育资源 | 依赖区间、fixture / live 分开，审批持久化、dry-run 草稿和自定义许可。 |
| [CozyClay](../../projects/CozyClay/README.md)，原位刷新 | JavaScript **+21**；2,099 / 212 / 22；[API](https://api.github.com/repos/HaD0Yun/CozyClay)；正式 [v3.3.0](https://github.com/HaD0Yun/CozyClay/releases/tag/v3.3.0)，UTC 11-23 22:57 = 本地 11-24 06:57。 | 语音、视频与多模态 | owner 迁移、motion writer / 费用、v8 镜头兼容、托管 replay 与参考片。 |

- 两个新仓库 ID `950355259 / 854807707` 在既有页无对应上游 / ID；CozyClay [旧 API](https://api.github.com/repos/NomaDamas/CozyClay)返回迁移目标 `repositories/1315384578`，与新仓库 ID 相同。实际目录 **1,059 → 1,061**，刷新不计新增。
- CozyClay 3.3.0 的 npm 指定版本初查 404，07:06 复查[指定版本](https://registry.npmjs.org/cozyclay/3.3.0)与 [latest](https://registry.npmjs.org/cozyclay/latest)均 HTTP 200 / 3.3.0；GitHub Release、源码 manifest 与注册表就绪时间分开。Resolve [npm 5.4.0](https://registry.npmjs.org/davinci-resolve-mcp/5.4.0) HTTP 200；未下载包内容或验签。
- 综合榜已收录项目继续观察：Claude-BugHunter +2,037、Firecrawl +920、autoclip +908、Superpowers +838、minimind +828、last30days-skill +790、CLI-Anything +783、App Store Compliance +755、diagram-design +624。本轮只复读榜单，没有重新审计这些旧项目。Ghost-Downloader-3 +1,078 为普通下载器，未仅因热度新增 AI 项目页。
- 同名 `skills` 候选未仅凭目录名覆盖旧档案；未把普通 Web / 运维项目自动归为 AI 热点，也未把各语言榜当作综合榜排名。
- 来源：[综合](https://github.com/trending/?since=daily)、[Python](https://github.com/trending/python?since=daily)、[TypeScript](https://github.com/trending/typescript?since=daily)、[JavaScript](https://github.com/trending/javascript?since=daily)、[Go](https://github.com/trending/go?since=daily)、[Rust](https://github.com/trending/rust?since=daily)、[C++](https://github.com/trending/c++?since=daily)、[Swift](https://github.com/trending/swift?since=daily)、[Jupyter Notebook](https://github.com/trending/jupyter-notebook?since=daily)、[Shell](https://github.com/trending/shell?since=daily)，本轮均 HTTP 200；榜单随时间变化。

## X：作者身份可核，项目当日原帖缺口保留

| 来源 | 本轮结果 | 限制 |
| --- | --- | --- |
| [NirDiamantAI](https://x.com/NirDiamantAI) | HTTP 200、标题 NirD；身份由 GenAI_Agents 固定 README 直接回链。 | B 级身份来源，未取得本轮项目的当日原帖 / 可比较互动；账号简介中的社区数字不是项目热度。 |
| [CozyClay live 搜索](https://x.com/search?q=%22CozyClay%22&f=live) | HTTP 200 后转 login onboarding，无帖文。 | C 级访问证据，不能据 GitHub 增星推导 X 传播。 |
| [Resolve MCP live 搜索](https://x.com/search?q=%22davinci-resolve-mcp%22&f=live) | 同样转 login onboarding，无帖文。 | 未读到可归属该 owner/repo 的当日讨论或争议。 |

作者主页的置顶内容指向另一个已收录仓库 `agents-towards-production`，不挪作 GenAI_Agents 的传播样本；当天非项目内容也不纳入。没有足够原帖 / 回复样本，不能总结“X 用户普遍认为”。

## Instagram：聚合数不归属项目

- [aiagents 标签](https://www.instagram.com/explore/tags/aiagents/)本轮 HTTP 200 后进入 popular，标题显示 **129K reels**；这是宽泛话题四舍五入累计显示，不是今天新增、独立作者或三个项目的传播数。
- [cozyclay 标签](https://www.instagram.com/explore/tags/cozyclay/)转 accounts/login 并返回 HTTP 429；没有可关联项目的帖文、日期、互动和评论。黏土手工同名也不能直接当作软件讨论。
- 两者为 C 级入口 / 访问状态，未沿用旧采样替代本轮访问，没有可核的项目级 Instagram 争议样本。

## YouTube：三条历史元数据，标题与版本分别核

计数、相对时间、时长来自本轮原生搜索页初始数据，标题 / 作者经 oEmbed 交叉核；三条 watch 页均 HTTP 200。这里没有完整观看、试听、下载媒体或采评论。

| 固定视频 | 可核元数据 | 关联与限制 |
| --- | --- | --- |
| [Control DaVinci Resolve with AI — MCP + Codex Setup Guide](https://www.youtube.com/watch?v=a_20JvT7h2g) | Run Super35mm；**12,483 views / 4mo ago / 10:46**；[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=a_20JvT7h2g&format=json)。 | 第三方历史安装主题；Web 索引旧数 7,922 不作为当前值。视频说明含该 npm 入口，但不证明最新 5.4.0、free bridge 或新 provider 已演示。 |
| [Context Engineering Explained (Prompt to Production, Free Module)](https://www.youtube.com/watch?v=a7bteK6c3Ng) | DiamantAI；**500 views / 4mo ago / 3:13**；[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=a7bteK6c3Ng&format=json)。 | GenAI_Agents 固定教程索引直接关联同一 video ID，但索引标签仍为“Context Is the New Code”；记录标题漂移。它是概念模块，不是所有 notebook 的验收。 |
| [AI 영상의 구도를 직접 짜봤습니다｜CozyClay × H3](https://www.youtube.com/watch?v=BTTCUXpuW3s) | CoderRed；**320 views / 4w ago / 2:31**；[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=BTTCUXpuW3s&format=json)。 | 搜索页显示英文译题“I Designed the Composition for an AI Video Myself”；oEmbed 是韩文原题，ID / 作者一致。第三方历史示例，不能证明刚发布的 3.3.0 效果。 |

搜索入口：[Resolve](https://www.youtube.com/results?search_query=davinci+resolve+mcp+Run+Super35mm)、[DiamantAI](https://www.youtube.com/results?search_query=DiamantAI+Context+Is+the+New+Code)、[CozyClay](https://www.youtube.com/results?search_query=CozyClay)。累计播放不是日增量；同名手工频道、另一个 Resolve MCP 实现和 Blackmagic 原生 MCP 视频未混入本项目样本。

## 讨论与争议：落实成验证条件

以下是上游资料引出的**工程判断和待验证问题**，不是已统计的社媒共识；详细固定来源见各项目页。

| 议题 | 已核静态事实 / 作者声明 | 需要验证 |
| --- | --- | --- |
| 分析是否只读 | Resolve 默认分析可写项目摘要和媒体池标记，视觉帧需宿主模型处理。 | 源片 / 工程 / 模型出口分别核，预览和 commit 不混同。 |
| 归档是否保证恢复 | Resolve safe mode 缺省 false；非 strict 归档失败可继续，granular 不归档，README 和代码 strict 清单有出入。 | 单动作拒绝、归档失败和重开恢复，不依赖功能名称。 |
| API 覆盖是否等于端到端成功 | 361/361 legacy 覆盖、349/361 live 覆盖、349/349 已测通过率，分母不同。 | 当前 Resolve build / 功能 / provider 的实机证据。 |
| dry-run 是否无云写入 | 教程 Publora key 存在时 dry-run 创建云草稿，模型 review 到上限仍进入发布路径。 | mock 验证具体请求、独立授权和持久操作 ID；不以“自审通过”代替用户批准。 |
| 可运行教程是否等于模型改进 | 离线评测使用 planted fixtures；旧行业教程非全部 live 复跑。 | 冻结保留集、真实 trace、失败分母、依赖与账单。 |
| 预演升级是否能无损回退 | CozyClay 新镜头 v8 在 3.2.3 中没有镜头，writer tokens 不显示在面板费用。 | 工程副本重开、全费用对账、画面 / 动作误差及完整视频。 |
| 本地是否没有采集 | CozyClay 托管 `/app/` 2 fps viewport replay；npm 无 replay 但默认用量统计，模型另有数据出口。 | 按实际分发模式核 telemetry / replay / provider，不能只看一个开关。 |

## 验证范围与接续

- 已核十个 official daily 页面、三个仓库的身份 / 默认 SHA / 非截断 tree 与发行；tree 完整不代表全仓已读。CozyClay tag 与本轮 main 相同；核两种 npm 指定版本及包同步延迟。21 个项目章节、日报七节、1,061 个实际目录、六文件 374 个本地链接及 59 个来源 / 访问状态 URL 核对通过，其中 22 个固定 SHA 文件；58 个 URL HTTP 200，Instagram 项目标签 429 已单列。HTTP 200 的登录页不视为内容可读。
- 本轮交付两份新七节指南、一份原位刷新的七节指南、本日报及两个既有首页分类 / 日期 / 实际目录数和 TODO；只暂存本轮六个文件。Markdown lint、链接与空白检查后提交，推送后再核远端 master。
- 接续：Resolve 目标 build 的只读 / 写入 / strict / 归档恢复与 provider；教程的冻结依赖 / 真实评测 / 审核身份 / 云端草稿与许可；CozyClay 工程兼容、writer 实际账单、录屏模式及生成视频效果；今日社媒原帖 / 回复及视频具体版本。
- 未安装运行上游、登录 / 授权 provider 或社交账号、改 MCP / 宿主配置、调用模型、创建云草稿 / 排程、连接真实 Resolve、处理 / 上传素材、迁移工程、下载包 / 权重 / 媒体、执行隔离 / 性能实验或完整观看视频。静态核读、作者自测和本轮运行验收分开。
