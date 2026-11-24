<!-- markdownlint-disable MD013 -->

# AI 热点日报｜2026-11-25

- 采样：2026-11-25（Asia/Shanghai）约 07:05–07:09；UTC 时间与北京时间区分。`stars today` 是滚动榜单快照，stars / forks / issues 与播放量为累计数，不是自然日增量，不合成跨平台排名。
- 范围：综合、Python、TypeScript、JavaScript、Rust、Go、C++、C、Shell、Jupyter Notebook 十个官方 daily 页的有界抽样；三份今日新增档案，不声称三项今天首次上榜或首次发布。
- 证据：A 为官方榜单、API、固定 SHA 文档 / 局部源码、发行与包元数据；B 为视频标题 / 作者 / 原生计数；C 为搜索、宽泛聚合和受限入口。静态判断、作者声明和本轮实测分开。
- 获取：Web 广搜主要为聚合、旧内容和相关讨论，定向搜索未取得本轮项目的可用当日社媒原帖。项目事实采用 GitHub 连接器 API / README / tree 与固定文件；长文件通过原生 HTTP 在本地局部核读，没有执行上游。搜索无有效当日样本不代表当天没有热点。
- 去重：目录、owner/repo、文内映射及仓库 ID 交叉检查，三项未见既有映射；已有热门项目仅记榜单观察。保留 `AGENTS.md` 原修改与历史身份 / 同名项目键待办。

## 今日重点

- **多端配置先对数据库版本。** `cc-switch-cli` Rust +8；最新发行 5.11.4 只支持到 schema 26，主线刚加入 27 兼容，不能把未发行修复当成现有包能力。[七节解读](../../projects/cc-switch-cli/README.md)
- **向量检索把排序、召回与过滤分开。** `pgvector` C +12；稳定示例固定 0.8.7，主线列出未发行 0.9.0；近似候选过滤可能使结果不足，strict order 也不保证真实 top-k 找全。[七节解读](../../projects/pgvector/README.md)
- **音乐生成先分代码、模型与试听。** `AudioCraft` Notebook +9；PyPI 1.3.0 与源码 1.4.0a2 有差异，MIT 代码与 CC-BY-NC 4.0 权重分开。此次上榜不是新模型发布。[七节解读](../../projects/audiocraft/README.md)

## GitHub：三项新增档案与榜单边界

| 项目 | 官方 daily 增星 | API 累计 stars / forks / open issues | 版本与观察 |
| --- | --- | --- | --- |
| [SaladDay/cc-switch-cli](https://github.com/SaladDay/cc-switch-cli) | Rust +8 | 5,573 / 383 / 86 | `v5.11.4` 于 11-17 发布；11-24 17:12 UTC 主线提交修 schema 27，属 Unreleased。MIT，ID `1102384337`。 |
| [pgvector/pgvector](https://github.com/pgvector/pgvector) | C +12 | 23,803 / 1,405 / 19 | 安装示例 / tag 0.8.7；主线 CHANGELOG 0.9.0 unreleased。API 许可 NOASSERTION，实际 PostgreSQL 风格条款；ID `359952601`。 |
| [facebookresearch/audiocraft](https://github.com/facebookresearch/audiocraft) | Jupyter Notebook +9 | 23,956 / 2,721 / 401 | PyPI 1.3.0（2024-06-03 上传），源码 1.4.0a2；默认分支提交 2025-03-13，API pushed_at 为 2026-03-03，不混作发布日期。ID `650945129`。 |

open issues 含 PR；API 数字与 Trending 展示可能采样不同。固定 SHA、版本、依赖、局部源码和许可见项目页。pgvector 与 AudioCraft 本轮 GitHub Releases 集合为空；这不表示没有 tag、包或历史版本。

综合榜中 [Ghost-Downloader-3](https://github.com/XiaoYouChR/Ghost-Downloader-3) +1,102、[NGINX](https://github.com/nginx/nginx) +158，本轮没有取得足以将它们归为 AI 项目的证据，未按增星机械收录。已有项目按目录去重，不重复建档；以下综合榜高热条目只更新本日报的热度观察，未发现需要同步其解读的新版本证据。

| 已收录项目 | 综合 daily 增星 | 本轮观察边界 |
| --- | --- | --- |
| [elementalsouls/Claude-BugHunter](https://github.com/elementalsouls/Claude-BugHunter) / [既有解读](../../projects/Claude-BugHunter/README.md) | +1,833 | 授权安全研究技能；增星不等于实际漏洞有效性。 |
| [HKUDS/CLI-Anything](https://github.com/HKUDS/CLI-Anything) / [既有解读](../../projects/CLI-Anything/README.md) | +1,075 | 软件 CLI 生成与 Agent 工具化；需按应用核可用范围。 |
| [obra/superpowers](https://github.com/obra/superpowers) / [既有解读](../../projects/superpowers/README.md) | +1,006 | 编码 Agent 工作流与技能；流程执行不等于结果验收。 |
| [firecrawl/firecrawl](https://github.com/firecrawl/firecrawl) / [既有解读](../../projects/firecrawl/README.md) | +990 | 网页抓取与内容入口；抓取得到不等于可任意使用内容。 |
| [mjmirza/app-store-compliance](https://github.com/mjmirza/app-store-compliance) / [既有解读](../../projects/app-store-compliance/README.md) | +936 | 应用合规检查技能；检查项不能代替平台最终审核。 |

来源：[综合](https://github.com/trending?since=daily)、[Python](https://github.com/trending/python?since=daily)、[TypeScript](https://github.com/trending/typescript?since=daily)、[JavaScript](https://github.com/trending/javascript?since=daily)、[Rust](https://github.com/trending/rust?since=daily)、[Go](https://github.com/trending/go?since=daily)、[C++](https://github.com/trending/c++?since=daily)、[C](https://github.com/trending/c?since=daily)、[Shell](https://github.com/trending/shell?since=daily)、[Jupyter Notebook](https://github.com/trending/jupyter-notebook?since=daily)。十页本轮均 HTTP 200；此为有限采样，榜单会变化。

## X：项目搜索均转登录

| 入口 | 本轮可复核状态 | 证据边界 |
| --- | --- | --- |
| [cc-switch-cli live 搜索](https://x.com/search?q=%22cc-switch-cli%22&f=live) | HTTP 200 后转 login onboarding，没有取得帖文列表。 | C 级访问入口，没有当日原帖、日期、互动或回复样本。 |
| [pgvector live 搜索](https://x.com/search?q=%22pgvector%22&f=live) | 同样转 login onboarding。 | 无法据此评价今日传播、赞同或争议规模。 |

定向 Web 搜索出现的 [GBrain 聚合故事](https://x.com/i/trending/2042548896367546602) 标为 Apr 10 / 旧索引，是另一个项目的自动摘要；没有将其“perfect recall”描述当成 pgvector 实测或今天共识。未取得可独立读取的当日原帖，保留缺口。

## Instagram：聚合热度与项目讨论分开

- [aiagents 标签](https://www.instagram.com/explore/tags/aiagents/)本轮 HTTP 200 转 popular，标题 **129K reels**；这是宽泛主题的累计约数，不是本日新增、独立作者数或三项目的传播。
- [musicgen 标签](https://www.instagram.com/explore/tags/musicgen/)转 accounts/login，HTTP 429；没有取得帖文、时间、互动或评论。没有沿用旧访问结果补作本轮项目证据。
- 两者只列为 C 级入口 / 访问状态，没有项目级 Instagram 热度或争议结论。

## YouTube：两条历史教程元数据，未完整观看

原生搜索页初始数据提供累计播放、相对时间和时长；oEmbed 交叉核视频 ID、标题与作者。两条 watch 页 HTTP 200，但页面可达不等于内容已经观看或技术步骤已验证。

| 固定视频 | 本轮元数据 | 关联与限制 |
| --- | --- | --- |
| [PGVector: Turn PostgreSQL Into A Vector Database](https://www.youtube.com/watch?v=j1QcPSLj7u0) | NeuralNine；**66,700 views / 2y ago / 20:04**；[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=j1QcPSLj7u0&format=json)。 | 第三方历史教程，不能证明 0.8.7 或主线 0.9.0 的具体行为与性能。 |
| [Como Utilizar MusicGen de META AI](https://www.youtube.com/watch?v=8C5XiF9Ba74) | AI Nature；**1,248 views / 3y ago / 12:38**；[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=8C5XiF9Ba74&format=json)。 | 搜索页显示英文译题“How to Use MusicGen from META AI”，oEmbed 为上述原题；ID / 作者一致。Web 索引的旧数 1,220 不作当前值；不是本轮新效果或试听证据。 |

搜索入口：[pgvector](https://www.youtube.com/results?search_query=pgvector)、[MusicGen / AI Nature](https://www.youtube.com/results?search_query=MusicGen+AI+Nature)、[cc-switch-cli](https://www.youtube.com/results?search_query=cc-switch-cli)。后者结果多指桌面 CC Switch，未取得可明确归属 SaladDay CLI 分支的视频，未挪用其播放量。没有采评论、下载媒体、完整观看或听评。

## 讨论与争议：把上游差异化为验证问题

以下为固定资料引出的**工程判断 / 待验证项**，不是已统计的社媒观点。出处见对应项目页。

| 议题 | 已核事实 | 应补验证 |
| --- | --- | --- |
| 支持同步是否等于跨版可恢复 | CLI 5.11.4 到 schema 26，主线新增 27，旧版不能打开新库。 | 在备份副本核每台设备版本、恢复与回退；数据库兼容不代表 CLI 有全部桌面功能。 |
| 临时启动是否等于系统隔离 | 共享历史、持久 provider 目录与凭据变化均有路径；受管理官方账户不支持该启动模式。 | 实际文件差异、会话锁、凭据生命周期和目标服务接受旧历史的条件。 |
| 精确排序是否等于完整召回 | pgvector strict order 约束返回顺序；近似扫描与过滤、扫描上限影响候选。 | 同数据 / 距离 / 过滤条件的精确 top-k、recall@k、结果不足率与 P95。 |
| 版本字符串是否证明稳定制品 | pgvector 主线 control 为 0.8.7，CHANGELOG 已有未发行 0.9.0；AudioCraft PyPI 与源码版本不同。 | 固定实际安装 tag / SHA、数据库 / Python / CUDA 版本，检查制品来源。 |
| 开源代码是否等于模型可商用 | AudioCraft MIT 代码，所查 MusicGen 权重 CC-BY-NC 4.0。 | 针对权重、输入音频与最终用途分别核权利，保留出处。 |
| token 步数是否等于实时生成与音乐质量 | MusicGen 的 50 自回归步 / 音频秒来自 token 布局；模型卡提示人声、语言与静音局限。 | 目标设备墙钟 / 显存、完整试听、结构 / 旋律遵循与失败分母。 |

## 验证范围与接续

- 三个仓库的 ID、默认 SHA、非截断 tree、README 与发行 / 包对象已核；tree 完整不等于全仓审计。新增三份七节页、日报，复用首页三个既有分类，项目实际目录 `1061 → 1064`，同步最新日期与 TODO。
- 已通过 21 个项目章节、日报七节、1,064 个实际目录与首页索引 / 日期、377 个本地链接检查。62 个来源 / 访问状态 URL 已核，61 个 HTTP 200，MusicGen Instagram 标签 429 已单列；HTTP 200 的登录页仍不视为内容可读。六文件 Markdown lint 与 diff 空白检查通过；仅暂存本轮六文件，推送后再核远端 master。静态核读不替代运行测试。
- 接续：CLI 跨版恢复 / 共享历史 / 代理日志与计费；pgvector 真实过滤负载 / 召回 / VACUUM / 恢复；AudioCraft 环境 / 权重 revision / 短片段 / 完整听评；当日社媒原帖、回复与视频具体版本。
- 本轮未安装运行上游、登录或授权账户、改宿主 / MCP 配置、切换 provider、迁移 / 同步数据库、开启代理、连接真实业务库、下载权重 / 安装包 / 媒体、调用模型、生成音频、测性能或完整观看。许可与文档事实、工程推断、运行验收分别记录。
