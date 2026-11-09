<!-- markdownlint-disable MD013 -->

# AI 热点日报｜2026-11-10

- 采样：2026-11-10（Asia/Shanghai）06:58 起至07时段；daily 日增、累计 stars、Views 与播放量均为分时快照，不是自然日结算。历史发行与原帖单独标日期。
- 范围：GitHub 综合及 Python、TypeScript、Rust、Go、JavaScript、C++、Swift、Jupyter Notebook 九页；X、Instagram、YouTube 有界观察，不合成跨平台排名。
- 证据：A 为官方榜单 / API / 固定 SHA 文件；B 为官网回链、平台原帖和原生元数据；C 为同名候选、聚合或受限入口。作者成绩、静态核读与实际运行分别表述。
- 获取：广泛搜索以第三方汇总为主，项目定向社媒搜索无可用结果；网页工具读取 Trending 失败，改用官方页面直接 HTTP 成功取得九页。GitHub 连接器核仓库身份、SHA、发行和引用源文件；社媒用官网回链、平台页面及 oEmbed。无搜索命中不等于没有活动。

## 今日重点

- **物理仿真升级先核数值问题**：MuJoCo 综合 +579，11-06 发布4.0.0；主线 Upcoming 已记稀疏 Cholesky 回归修复，不能将未发行修复当成稳定版已解决。[解读](../../projects/mujoco/README.md)
- **智能家居管理要分清入口与身份**：HA-MCP 综合 +31；进程内 integration、普通 / readonly endpoint、OAuth / OIDC、管理员 token 分别核对。[解读](../../projects/ha-mcp/README.md)
- **团队 agent 的“人审”要看有效权限**：CompanyOS TypeScript +27；Guide 的 worker 自合并例外、默认 secret audience、Elastic License / 白标条件比宣传口号更影响部署。[解读](../../projects/CompanyOS/README.md)
- **地图在本机计算仍可能外发**：GeoLibre TypeScript +66，3.7.0 增室内地图等；AI 元数据、协作 GeoJSON、Share 上传和网站统计各有独立通路。[解读](../../projects/GeoLibre/README.md)
- **语音升级不只换模型名**：VoxCPM Python +423；原位补齐 VoxCPM2 / 1.5 / 0.5B、采样率、参考条件、后端与网络监听边界，未做合成或试听。[解读](../../projects/VoxCPM/README.md)

## GitHub 热点项目

日增来自指定官方 daily 页，累计为 stars / forks / open issues（含 PR）。“新增”指本仓库首次建档，不代表今天创建或首次上榜；语言榜不是全站排名，stars 不代表部署量、质量或安全认证。

| 项目与动作 | 可核热度与发行 | 现有分类 | 工程观察 |
| --- | --- | --- | --- |
| [mujoco](../../projects/mujoco/README.md)，新增 | 综合 +579；16,878 / 1,991 / 305；[API](https://api.github.com/repos/google-deepmind/mujoco)；[4.0.0](https://github.com/google-deepmind/mujoco/releases/tag/4.0.0)，UTC 11-06。 | 模型、训练与推理基础设施 | 推测接触忽略加速度、Python 包拆分、tendon / RK4 迁移及主线尚未发行修复。 |
| [ha-mcp](../../projects/ha-mcp/README.md)，新增 | 综合 +31；5,911 / 292 / 25；[API](https://api.github.com/repos/homeassistant-ai/ha-mcp)；[v9.1.2](https://github.com/homeassistant-ai/ha-mcp/releases/tag/v9.1.2)，UTC 11-08；9.2.0.dev 为预发行。 | Agent 框架与技能生态 | HA版本 / Python范围、标准单租户、OIDC共享身份、readonly URL与凭据权限。 |
| [CompanyOS](../../projects/CompanyOS/README.md)，新增 | TypeScript +27；20,604 / 3,468 / 62；[API](https://api.github.com/repos/kortix-ai/CompanyOS)；[v0.15.2](https://github.com/kortix-ai/CompanyOS/releases/tag/v0.15.2)，UTC 11-09；dev VERSION为0.15.3。 | 办公、商业与行业应用 | worker merge例外、secret默认共享 / 传递、云资源与白标独家计算协议。 |
| [GeoLibre](../../projects/GeoLibre/README.md)，新增 | TypeScript +66；8,522 / 955 / 20；[API](https://api.github.com/repos/opengeos/GeoLibre)；[v3.7.0](https://github.com/opengeos/GeoLibre/releases/tag/v3.7.0)，UTC 11-08。 | 办公、商业与行业应用 | GIS参数、MCP根目录与live、默认网络、AI / 协作 / 共享出口和部署策略。 |
| [VoxCPM](../../projects/VoxCPM/README.md)，原位刷新 | Python +423；42,107 / 4,799 / 173；[API](https://api.github.com/repos/OpenBMB/VoxCPM)；[2.0.3](https://github.com/OpenBMB/VoxCPM/releases/tag/2.0.3)，UTC **05-11**。 | 语音、视频与多模态 | VoxCPM2与旧模型、Python文档差异、附加资产、无认证Web默认监听和条件性RTF。 |

- 去重：实际目录与 owner/repo 映射核对，五个唯一仓库 ID；四个新目录、一个原位刷新，实际目录1,015 → 1,019，复用四类，并为此前首页缺少入口的 VoxCPM 补齐解读链接。
- 已有高热：综合 Astryx +3,324、OpenMausBot +1,589、agent-browser +914，Python VoiceStudio +1,247；本轮仅记榜单，不声称重审实现。同名 skills 的 owner-aware 映射问题继续保留。
- 选择范围：榜上仍有其他候选；这是有界选样。Sherlock、下载工具和通用软件不因高日增就被写成 AI 核心项目；MuJoCo 以学习环境基础设施身份收录，不将其本身称为生成式模型。
- 官方入口：[综合](https://github.com/trending?since=daily)、[Python](https://github.com/trending/python?since=daily)、[TypeScript](https://github.com/trending/typescript?since=daily)、[Rust](https://github.com/trending/rust?since=daily)、[Go](https://github.com/trending/go?since=daily)、[JavaScript](https://github.com/trending/javascript?since=daily)、[C++](https://github.com/trending/c++?since=daily)、[Swift](https://github.com/trending/swift?since=daily)、[Jupyter Notebook](https://github.com/trending/jupyter-notebook?since=daily)。

## X 观察

[官网](https://kortix.com)回链 [@kortix](https://x.com/kortix)，其置顶引用作者介绍帖。直接页面与 oEmbed 核作者、正文、日期；只使用明确标为 Views 的数字，不解释其余孤立数字。

| 原帖 | 可核内容与热度 | 讨论 / 争议边界 |
| --- | --- | --- |
| [Marko Kraemer 介绍 CompanyOS](https://x.com/markokraemer/status/2118817359485882729)，[oEmbed](https://publish.twitter.com/oembed?url=https://x.com/markokraemer/status/2118817359485882729) | 2026-11-06；91.5K Views；强调公司配置为代码、团队工作区、sovereign / multiplayer。 | 是产品介绍。源码可读、自托管、许可自由和实际数据主权是不同问题；根许可及白标条件见项目页。 |
| [Kortix 引用介绍帖](https://x.com/kortix/status/2118880204508614658)，[oEmbed](https://publish.twitter.com/oembed?url=https://x.com/kortix/status/2118880204508614658) | 2026-11-07；1,812 Views；正文为 CompanyOS 简短标识并引用前帖。 | 同一产品的官方传播，不计作两项独立社区验证，也不推断今天日增由这两帖导致。 |

没有取得可绑定本轮项目的当天原帖、完整评论样本或每日互动增量；以上历史累积数字不能支持 X 当天排名或社区共识。

## Instagram 观察

- [kortix 同名候选](https://www.instagram.com/kortix/)重定向登录页；本轮无官网身份回链，**账号身份未确认**，也未读到帖子、日期、互动量。
- [geospatial 标签入口](https://www.instagram.com/explore/tags/geospatial/)转 popular 聚合，页面标题为约455K reels；这是宽泛地理空间主题计数，不能归于 GeoLibre，也不是当天新增。
- 原帖覆盖仍有缺口。受限入口仅作观察，不写“爆火”“没有讨论”或跨平台传播规模；本轮未登录或发布。

## YouTube 观察

从原生 [GeoLibre 搜索](https://www.youtube.com/results?search_query=GeoLibre)及 [MuJoCo 4.0 搜索](https://www.youtube.com/results?search_query=MuJoCo+4.0)读取视频列表；以下标题、作者与 oEmbed 一致。相对时间不反推精确日期，累计播放不等于当天增长。

| 视频 | 可核元数据 | 内容边界 |
| --- | --- | --- |
| [GeoLibre 1.0 入门](https://www.youtube.com/watch?v=87Cm0QagtxI) | Open Geospatial Solutions；31,732 views、4mo ago；[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=87Cm0QagtxI&format=json)。 | README直接回链的历史教程，不能代表3.7全部行为。 |
| [GeoLibre v3.7.0 demo](https://www.youtube.com/watch?v=hia18EWcGTo) | 同一频道，oEmbed author_url均为 @giswqs；2,784 views、1d ago；[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=hia18EWcGTo&format=json)。 | 同频道新演示，关联到当前发行；未观看内容，不能证明全部新增功能或数据处理正确。 |
| [MuJoCo 4.0 与机器人周刊](https://www.youtube.com/watch?v=lBsP6_E6lvM) | The Tech Storyteller；26 views、1d ago；[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=lBsP6_E6lvM&format=json)。 | 第三方混合主题周刊；MuJoCo标题不代表官方背书，也未核其数值错误讨论。 |

未下载 / 完整观看视频、分析完整评论或取得每日播放增量；检索中的 Humanoid-v4 环境名不能当成 MuJoCo 4.0 版本介绍。

## 讨论与争议：事实、判断和待验证

下表主要是文档 / 实现暴露的工程问题，不是社媒观点分布统计。

| 议题 | 已核事实 | 判断 / 待验证 |
| --- | --- | --- |
| 新物理能力与结果可信度 | MuJoCo 4.0增加推测接触与弹塑性，主线另记4.0.0数值回归修复。 | 固定版本与模型，核步长 / 求解器和参考轨迹；仿真成功不等于实验复现。 |
| 管理面与最小权限 | HA-MCP标准模式共享权限，readonly为连接模式，OIDC共享HA身份。 | 使用测试HA，核有效工具策略、普通入口和撤销；工具隐藏不能承担凭据隔离。 |
| 人审承诺与例外 | CompanyOS Guide警告worker可自合并；secret默认audience为工作区所有人。 | 强制人审要核实际merge权限；秘密分发、审计和回滚需实测。 |
| 自托管与自由部署 | CompanyOS根许可为ELv2，白标另有Platinum独家计算协议。 | 托管、内部部署、重包装与供应商约束分别对照目标用途；不沿用无条件开源标签。 |
| 本地GIS与共享 | GeoLibre本地处理之外有AI元数据、relay、Share与网站统计通路。 | 敏感空间资料逐出口审；坐标、单位、NoData与算法应有独立参考。 |
| 声音质量与“实时” | VoxCPM2声明多语种 / 48kHz和条件性RTF，作者承认控制波动。 | 保留失败与重复次数，核首块延迟、CER/WER及人工听感；48kHz不证明真实高频。 |

## 验证范围与接续

- 已核：九页官方daily；五个唯一仓库ID、固定SHA、发行及引用文件，四个完整tree，CompanyOS因大树响应不可用改读根目录和指定文档；四个PyPI JSON及官方VoxCPM2 Hub许可元数据。
- 文档验证：五页35个固定章节、五个唯一ID、四类导航、1,019个实际目录与316个本地链接通过；74个范围内外部URL有来源 / 访问证据，其中28个固定SHA文件已读取，Instagram仍按登录 / 聚合限制记录。8个Markdown文件lint零问题，diff检查通过；本轮只提交8文件，保留用户AGENTS.md原修改。
- 未做：上游安装 / 构建 / 测试、权重 / 媒体下载、推理与试听、账户登录、云资源部署、家庭设备操作、GIS处理、真实权限 / 网络 / 隔离、性能或完整视频 / 评论验收。
- 接续：MuJoCo 4.0.0回归 / 迁移；HA入口 / token / readonly /策略；CompanyOS worker / secret /预算 /协议；GeoLibre CRS / MCP /分享与策略；VoxCPM模型 /环境 /后端 /完整听评。skills同名映射继续待owner-aware方案。
