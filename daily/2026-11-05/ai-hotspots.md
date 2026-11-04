<!-- markdownlint-disable MD013 -->

# AI 热点日报｜2026-11-05

- 采样：2026-11-05（Asia/Shanghai），约 07:04 起；日增和累计均为读取快照，不是自然日结算。发行和社媒内容另列其历史日期。
- 范围：GitHub 综合与 Python、TypeScript、Rust、Go、JavaScript、C++、Swift、Jupyter Notebook daily；X、Instagram、YouTube 有界观察，不合成跨平台排名。
- 证据等级：A 为官方榜单、API、固定 SHA 文件；B 为上游回链账号 / 视频与平台原生元数据；C 为同名候选、聚合或受限入口。作者宣传、静态核读与独立实测分开。
- 获取状态：web 工具打开 Trending 受限，直接 HTTP 成功取得九页；连接 GitHub 核五个唯一 ID、完整树、固定分支 SHA、发行列表与引用文件。广泛及项目定向 web 搜索未给出可用当前社媒原帖，随后核查官网 / README 回链、X 原生账号与 oEmbed、YouTube 列表与 oEmbed。检索缺口不表示平台没有活动。

## 今日重点

- **Auto Ontology 综合 +2,053，原位刷新身份与服务边界**：MCP 通过 OAuth 识别用户，后端却信任前端身份头，ingestion 自身无认证；3001 / 3002 必须私网。语义层可审阅不等于 SQL 自动正确。[解读](../../projects/auto-ontology/README.md)
- **“8 GB 跑 2.78T”需要同时展示磁盘和延迟**：kimi-k3-in-c 综合 +351，仍需约 1.7 TB 存储；顶部时延表来自同一 124 CPU 环境，Jetson 上游记录是约 949 秒生成一个 token。[解读](../../projects/kimi-k3-in-c/README.md)
- **日报自动化应保留原始证据与派生摘要的区别**：Horizon 综合 +121，以 Profile 路由、筛选和补充背景；当前提示词明确以前日报不是独立来源。[解读](../../projects/Horizon/README.md)
- **Agent 工作区和语音入口都需分层看数据出口**：open-duet Python +105，审批、可选 Docker 与桌面账号各有边界；SayAll Swift +78，回眸 / MCP 默认关闭，第三方 AI 仍可能外发读取内容。[Open Duet](../../projects/open-duet/README.md)、[SayAll](../../projects/remote-mic-app/README.md)

## GitHub 热点项目

日增来自指定官方 daily 页，累计按 stars / forks / open issues（含 PR）排列；语言榜选样不代表全站头部。星数是关注信号，不能证明用户量、效果或安全。

| 项目与动作 | 可核热度与发行 | 分类 | 工程观察 |
| --- | --- | --- | --- |
| [auto-ontology](../../projects/auto-ontology/README.md)，原位刷新 | 综合 +2,053；累计 4,829 / 387 / 42；发行列表为空。 | RAG、检索与知识处理 | 用户级 MCP OAuth、后端信任头、无认证 ingestion、Vault 和 API token。 |
| [kimi-k3-in-c](../../projects/kimi-k3-in-c/README.md)，新增 | 综合 +351；累计 10,255 / 1,625 / 26；[v1.1.0](https://github.com/FareedKhan-dev/kimi-k3-in-c/releases/tag/v1.1.0)，UTC 2026-10-02。 | 模型、训练与推理基础设施 | RSS / 磁盘 / CPU 与 I/O 分开；fixture、单 token 记录和完整质量评测分开。 |
| [Horizon](../../projects/Horizon/README.md)，新增 | 综合 +121；累计 12,457 / 1,817 / 26；发行列表为空。 | RAG、检索与知识处理 | Profile 配置、原始来源、历史摘要证据等级、可选搜索和投递出口。 |
| [open-duet](../../projects/open-duet/README.md)，新增 | Python +105；累计 6,771 / 868 / 8；[mobile-v0.3.0](https://github.com/Anil-matcha/open-duet/releases/tag/mobile-v0.3.0)，UTC 2026-11-04；主应用 [v0.8.1](https://github.com/Anil-matcha/open-duet/releases/tag/v0.8.1)，UTC 2026-11-02。 | Agent 框架与技能生态 | 单 owner 自托管、桌面账号、审批模式、默认无网络 Docker 和设备 manage scope。 |
| [remote-mic-app / SayAll](../../projects/remote-mic-app/README.md)，新增 | Swift +78；累计 2,435 / 256 / 110；列表首项 [v1.9.21](https://github.com/HD838A/remote-mic-app/releases/tag/v1.9.21)，UTC 2026-09-03。 | 语音、视频与多模态 | 主线候选与稳定制品分开；蓝牙 / 按键 / 第三方转写、历史只读授权和外发路径。 |

- **去重与首页**：以 projects 实际目录、大小写与 owner/repo 链接核对；五个本轮上游 ID 互异。新增四目录、原位更新一页，实际目录 992 → 996，复用四个现有分类并同步首页入口。
- **已有头部信号**：综合 agent-desktop +2,463、Scrapling +2,006、Claude-mem +1,165、MoneyPrinterTurbo +615、Worktrunk +524；Python OpenMontage +572。这些已有页面，部分近几日刚核读，本轮只记录榜单信号，不声称重审全部实现。
- **选择与身份边界**：mattpocock/skills 综合 +1,376、scenario-labs/skills +224，与既有 skills 目录映射不同，未凭同名覆盖。github/spec-kit 与 gstack 等已有目录继续去重；floci、DiscImageStudio 等不因上榜自动归为 AI 项目。本轮不是全部语言榜候选的穷尽收录。
- 官方榜单：[综合](https://github.com/trending?since=daily)、[Python](https://github.com/trending/python?since=daily)、[TypeScript](https://github.com/trending/typescript?since=daily)、[Rust](https://github.com/trending/rust?since=daily)、[Go](https://github.com/trending/go?since=daily)、[JavaScript](https://github.com/trending/javascript?since=daily)、[C++](https://github.com/trending/c++?since=daily)、[Swift](https://github.com/trending/swift?since=daily)、[Jupyter Notebook](https://github.com/trending/jupyter-notebook?since=daily)。

## X 观察

[SayAll 官网](https://sayall.app/) 回链 [getSayAll](https://x.com/getSayAll)，原生账号也回链项目。以下历史帖由原生页面与 oEmbed 核对作者、日期和文字；不采用账号页无明确语义的孤立数字作为赞 / 转 / 浏览量。

| 原帖 | 已核内容 | 热度与证据边界 |
| --- | --- | --- |
| [SayAll，2026-11-02](https://x.com/getsayall/status/2117287327676731709)，[oEmbed](https://publish.twitter.com/oembed?url=https://x.com/getsayall/status/2117287327676731709) | 作者感谢第三方推荐，引用先前的使用体验。 | 历史回复；不证明当日新版本、当前兼容性或传播规模，无可靠互动增量。 |
| [向阳乔木，2026-10-08](https://x.com/vista8/status/2108165930102702296)，[oEmbed](https://publish.twitter.com/oembed?url=https://x.com/vista8/status/2108165930102702296) | 第三方介绍遥控器、SayAll 与多款语音工具搭配的个人体验，项目账号引用。 | 个体体验和主观性价比判断，不是受控比较、普遍兼容证明或今日热点增量。 |

另探查 [AnilMatcha 同名候选](https://x.com/AnilMatcha)，未取得可用项目原帖或官网身份回链，未视为 Open Duet 官方账号。原帖与引用作者分开记录；本轮没有足够评论样本推断社区共识或争议强度。

## Instagram 观察

- [anilmatcha 同名候选](https://www.instagram.com/anilmatcha/) 跳登录并返回 429；未建立项目官网回链，不认定为 Open Duet 官方账号。
- [aiagents 主题入口](https://www.instagram.com/explore/tags/aiagents/) 转 popular/aiagents 聚合；标签聚合不能绑定本轮具体项目。
- 本轮未取得可独立复核的项目原帖、发布时间和赞评，故不报项目级热度或日增；这是访问 / 身份缺口，不代表没有讨论。

## YouTube 观察

下面两条由[原生搜索列表](https://www.youtube.com/results?search_query=Open+Duet+Anil+Matcha)与 oEmbed 交叉核对 ID、作者和标题。播放量为本轮累计快照，相对时间不能替代精确发布日期。

| 视频与来源 | 可核元数据 | 讨论边界 |
| --- | --- | --- |
| [Free Unlimited Grok Bot Alternative: Open-Source, Any Model, No Restrictions](https://www.youtube.com/watch?v=vtFy94DfETE)，Open Duet README 回链 | 作者 Anil Chandra Naidu Matcha；324 views、2d ago；[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=vtFy94DfETE&format=json) 一致。 | 项目演示入口；“免费 / 无限 / 无限制”是宣传标题。源码明确模型另计费且有审批，不能将标题当使用条款。 |
| [Open Duet: NEW FREE Claude Duet Alternative!](https://www.youtube.com/watch?v=qe6rb8_Ef-w)，第三方 | 作者 Julian Goldie SEO；6,707 views、12d ago；[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=qe6rb8_Ef-w&format=json) 一致。 | 历史第三方介绍，标题中的“新 / 免费”不是本轮验证结论；没有复核全片、评论或商业关系。 |

本轮没有全片观看、评论语料、精确发布日期或每日播放变化，不用累计量解释 GitHub 增星，也不从视频标题推断实际运行质量。

## 讨论与争议：事实、判断和待验证

以下为一手文档引出的工程审查议题，不是社群意见分布统计。

| 主题 | 已核文档事实 | 判断 / 待验证 |
| --- | --- | --- |
| 模型“装得下”与“用得快” | Kimi C 采用磁盘流式读取；顶部比较用同一 124 CPU 环境，完整权重约 1.56 TB。 | RSS、系统缓存、磁盘、时延与质量分别测；不能把 8 GB 标签等同普通笔记本的实测体验。 |
| 上游内部措辞不一致 | Kimi README 顶部称 128 GB+ 全部驻留，后文约 1.45 TB 专家仍按需读取。 | 以 I/O 计数、缓存与内存证据解释；本轮标出差异，未替作者裁定所有测量。 |
| 登录与内部服务边界 | Auto Ontology 后端信任身份头，ingestion 自身无认证；MCP 为用户级 OAuth。 | 网关身份与私网隔离都要落实，不能让公网直达内部服务；未做漏洞复现。 |
| 摘要是否能当独立证据 | Horizon 提示词明确以前日报是派生摘要，不是独立验证。 | 保留原始 URL 和抓取时间，避免模型把历史摘要循环背书；需人工抽查事实与评论引用。 |
| 本地优先与外网依赖 | Open Duet 桌面要求应用账号，engine 可用云；SayAll 本地 MCP 可被云模型客户端读取。 | 逐路径核身份服务、内容出口、凭据与停止 / 撤销，而不是只看数据文件位置。 |
| 发行标签与实际验收 | Open Duet 有新 mobile 发行，但文档对真机状态不一致；SayAll 主线部分功能仍标候选。 | 记录准确包 / commit、平台和功能，不能从 tag 或源码存在推出完整产品验收。 |

## 验证范围与接续

- **已核**：九个官方 daily 页；五个唯一仓库 ID、固定 SHA、完整树、发行列表与引用文档 / 抽样实现；Kimi 模型元数据；四个新目录、Auto Ontology 原位更新与首页分类 / 实际总数；两条历史 X 原帖、两条 YouTube 列表 / oEmbed 和 Instagram 访问状态。
- **未运行**：上游安装 / 构建 / 测试、模型下载与推理、SQL / MCP OAuth / 内部服务权限测试、采集账号登录与自动投递、Open Duet 桌面账号 / engine / container / mobile、SayAll 驱动 / 遥控器 / 语音 / MCP，及视频全片与评论。
- **接续**：Kimi 完整参考与 I/O / 内存测量；Auto Ontology 私网和身份转发；Horizon 漏报 / 错并 / 来源保真；Open Duet 账号 / 审批 / 设备 scope 与文档冲突；SayAll 稳定包对应候选能力、真实语音与撤销测试。skills 同名身份问题继续保留。

## 主要来源

- [NVIDIA/auto-ontology](https://github.com/NVIDIA/auto-ontology)、[API](https://api.github.com/repos/NVIDIA/auto-ontology)；固定文档 / 实现见[原位解读](../../projects/auto-ontology/README.md)。
- [FareedKhan-dev/kimi-k3-in-c](https://github.com/FareedKhan-dev/kimi-k3-in-c)、[API](https://api.github.com/repos/FareedKhan-dev/kimi-k3-in-c)；模型元数据与测量来源见[解读](../../projects/kimi-k3-in-c/README.md)。
- [Thysrael/Horizon](https://github.com/Thysrael/Horizon)、[API](https://api.github.com/repos/Thysrael/Horizon)；配置和证据提示见[解读](../../projects/Horizon/README.md)。
- [Anil-matcha/open-duet](https://github.com/Anil-matcha/open-duet)、[API](https://api.github.com/repos/Anil-matcha/open-duet)；认证 / 审批 / 电脑与版本见[解读](../../projects/open-duet/README.md)。
- [HD838A/remote-mic-app](https://github.com/HD838A/remote-mic-app)、[API](https://api.github.com/repos/HD838A/remote-mic-app)；候选状态、隐私 / 授权和许可见[解读](../../projects/remote-mic-app/README.md)。
