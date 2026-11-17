<!-- markdownlint-disable MD013 -->

# AI 热点日报｜2026-11-18

- 采样：2026-11-18（Asia/Shanghai）07 时段，事件日期另列；daily 增星、API 累计数与视频播放量均为抓取快照，不是自然日结算。
- 范围：GitHub 综合、Python、TypeScript、JavaScript、Rust、Go、C++、Jupyter Notebook、Shell、Swift 十个官方 daily 页的有界抽样；不合成跨平台榜单。
- 证据：A 为官方榜单 / API / 固定 SHA 文档和代码；B 为平台原生列表 / 元数据；C 为搜索、聚合或受限入口。上游自述、静态核读、本文判断与运行验收分开。
- 获取：广泛搜索以二手材料和无关结果为主，随后四条项目 / 社媒定向搜索为空；改用官方 Trending HTTP、GitHub 连接器和平台原生 HTTP / oEmbed。搜索为空不代表没有讨论。
- 接续：最近日报为 11-17；按 `projects/`、已有上游链接与仓库 ID 核对，三个新上游未命中已有档案。只新增三页并同步三类导航，不重复昨天的四项目说明。

## 今日重点

- **团队 Agent 的运营边界比功能数量更值得核。** AgenticOS Python +42，最新非预发行 v1.82.1；文档明确随附 runtime 有网络、共享 Agent 会借出绑定能力、并发预算存在超额窗口。[项目解读](../../projects/agenticos/README.md)
- **超内存推理需要分开看加载、prefill 和 decode。** BigMoeOnEdge C++ +46；v0.44.0 为预发行版，历史吞吐排除加载和 prefill，不能只拿 tok/s 判断可用性；发行说明和 API 文档还有采样参数漂移。[项目解读](../../projects/BigMoeOnEdge/README.md)
- **企业 Agent 手册补进了可执行的工程教学。** AI Agent Handbook JavaScript +71；从 Harness、行为仿真到黄金集形成学习路径。1,906 份沙龙问卷是特定样本自报，不能外推成全行业普查。[项目解读](../../projects/ai-agent-handbook/README.md)

## GitHub 热点项目

增星来自本轮官方 daily；API 顺序为 stars / forks / open issues（含 PR），不是当日新增 issue 数。“新增”指本仓库首次建档，不等于项目今天首发。

| 项目与动作 | 可核热度与版本 | 沿用分类 | 工程关注 |
| --- | --- | --- | --- |
| [agenticos](../../projects/agenticos/README.md)，新增 | Python +42；406 / 72 / 58；[API](https://api.github.com/repos/vstorm-co/agenticos)；[v1.82.1](https://github.com/vstorm-co/agenticos/releases/tag/v1.82.1)，UTC 11-17 22:29，非预发行。 | 办公、商业与行业应用 | 数据出口、沙箱网络、发布时授权、预算并发和 vault 恢复。 |
| [BigMoeOnEdge](../../projects/BigMoeOnEdge/README.md)，新增 | C++ +46；1,010 / 103 / 63；[API](https://api.github.com/repos/Helldez/BigMoeOnEdge)；[v0.44.0](https://github.com/Helldez/BigMoeOnEdge/releases/tag/v0.44.0)，UTC 11-17 08:44，预发行。 | 模型、训练与推理基础设施 | 缓存 / I/O、吞吐分母、数值容差、采样契约和本地 Agent 权限。 |
| [ai-agent-handbook](../../projects/ai-agent-handbook/README.md)，新增 | JavaScript +71；3,442 / 426 / 6；[API](https://api.github.com/repos/aliyun/ai-agent-handbook)；本轮 [Releases](https://github.com/aliyun/ai-agent-handbook/releases) 列表为空。 | AI 学习与教育资源 | 仿真 / 评价分层、教学判分、黄金集冻结、调研样本与厂商语境。 |

- 三个唯一仓库 ID 为 `1318197751` / `1296688895` / `1365520317`。实际项目目录 **1,041 → 1,044**；复用既有分类，不扩分类。
- 已建档榜单观察：Univer +1,776、AG-UI +1,444、FFmpeg Skill +1,376、PaperOrchestra +1,175、Orca +1,052、Claude-BugHunter +1,007、SkillEvaluator +969、Open Code Review +764、LoopForge +590。这些只更新到本日报的热度观察，不代表重新审查实现或已验证新版本。
- [综合 daily](https://github.com/trending?since=daily)、[Python](https://github.com/trending/python?since=daily)、[TypeScript](https://github.com/trending/typescript?since=daily)、[JavaScript](https://github.com/trending/javascript?since=daily)、[Rust](https://github.com/trending/rust?since=daily)、[Go](https://github.com/trending/go?since=daily)、[C++](https://github.com/trending/c++?since=daily)、[Jupyter Notebook](https://github.com/trending/jupyter-notebook?since=daily)、[Shell](https://github.com/trending/shell?since=daily)、[Swift](https://github.com/trending/swift?since=daily)均为本轮 HTTP 200 的动态榜单，未来打开会变化。普通系统工具不只因上榜便列为 AI 核心。

## X：原帖与热度缺口

| 入口与状态 | 可核热度 | 本轮解释 |
| --- | --- | --- |
| [BigMoeOnEdge 最新搜索](https://x.com/search?q=BigMoeOnEdge&src=typed_query&f=live)：网页工具 403；直接 HTTP 200 后转登录。 | 无可独立读取的原帖、Views、点赞或转发快照。 | C 级观察入口，不能据搜索词或 GitHub 上榜推断 X 传播。 |
| [AgenticOS 最新搜索](https://x.com/search?q=agenticos&src=typed_query&f=live)：直接 HTTP 200 后转登录。 | 无可核帖子和互动量。 | 本轮保留覆盖缺口，不把受限读取写成“没有讨论”。 |

未复用昨天 OpenAI 科研帖的累计 Views 充作今天项目热度；本轮没有可统计的 X 评论样本。

## Instagram：登录限制

- [aiagents 主题入口](https://www.instagram.com/explore/tags/aiagents/)：网页工具限流，直接 HTTP 200 后重定向登录。当前没有可独立读取的帖子或主题计数，昨天的聚合量不沿用为今天数据。
- [BigMoeOnEdge 标签入口](https://www.instagram.com/explore/tags/bigmoeonedge/)与 [vstorm.co 同名账号候选](https://www.instagram.com/vstorm.co/)也转登录；后者的归属未由本轮回链确认，不称为官方账号。
- 本轮均为 C 级入口；没有核到项目原帖、评论或互动量，不做项目间热度比较。

## YouTube：端侧话题候选与元数据

| 入口 | 本轮可读事实 | 边界 |
| --- | --- | --- |
| [BigMoeOnEdge 原生搜索](https://www.youtube.com/results?search_query=BigMoeOnEdge)中的 [Qwen Just Ran an 82GB Model on a 12GB Phone](https://www.youtube.com/watch?v=Yf0Aaf94pc8)，频道 Code Unpacked。 | 原生列表显示 **6,970 次累计播放、2mo ago、11:43**；[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=Yf0Aaf94pc8&format=json)的标题 / 作者匹配。列表描述谈 12 GB Android 本地运行约 82 GB 模型。 | B 级元数据，第三方历史话题候选；完整描述、视频内容和代码链接未读，尚未独立确认与本轮仓库及版本的对应关系，不计作项目热度证据。 |
| [agenticos vstorm 原生搜索](https://www.youtube.com/results?search_query=agenticos+vstorm) | HTTP 200，本轮未抽取到可验证的视频条目。 | 检索缺口，不是不存在视频的结论。 |

上述 watch HTTP 200，但 player 数据未提供可用的 videoDetails；网页工具对 watch 限流。没有据页面成功返回宣称已看演示，也没有取得评论争议样本或每日播放增量。

## 讨论与争议：工程判断及待验证

这些议题由上游材料导出，不包装成已经统计的社媒争论；固定 SHA 证据见项目页。

| 议题 | 已核事实 | 判断 / 待验证 |
| --- | --- | --- |
| 自托管是否等于数据不外发 | AgenticOS 的生成、embedding、parser、搜索和工具可各自接外部服务。 | 应按每条数据流验收，不能只核控制台部署位置。 |
| 有沙箱是否足以开放主机 | AgenticOS 随附 runtime 请求网络，常规 runc，sandboxd token 权力很高。 | 独立核 egress、宿主端口、服务 token 和多租户边界。 |
| 月预算是否严格限额 | AgenticOS 文档明确并发费用尚未提交时彼此不可见。 | 严格支出门槛需要供应商额度 / 队列等控制，并核失败和压缩费用。 |
| 大模型能运行是否等于可用 | BigMoeOnEdge 通过闪存与专家缓存运行超 RAM 模型；历史表只计 decode。 | 同时测 TTFT、prefill、长上下文、温控、P95 延迟及任务质量。 |
| 接口兼容是否代表字段生效 | v0.44.0 说明开始读取采样字段；main API 文档仍写忽略。 | 固定实际制品验证请求语义，speculation 的 greedy 条件另核。 |
| 教学与调研能否证明生产收益 | 手册含四类教学任务和 1,906 份特定样本问卷。 | 过关、样本比例和生产效果是不同对象；需脱敏黄金集、逐题失败及现场对照。 |

## 验证范围与接续

- 来源：十个官方 daily 页，三个唯一仓库 ID、main SHA、完整目录树和发行列表；只抽读相关 README、许可、部署、隔离、预算、基准、章节与教学代码，不等于全仓审计或全书审校。
- 文档：三个七节项目页、同日四平台日报、首页三个分类 / 最新日报 / 实际总数和 TODO；原有 `AGENTS.md` 修改保留并排除提交。
- 检查通过：三项目 21 个固定章节、日报七节、三个分类入口、1,044 个实际目录、六文件 348 个本地链接；55 个本轮来源 URL 均有来源内容或明确访问证据，包含 35 个 GitHub 来源、十个 daily 页、九个社媒入口和书站。六文件 Markdown lint 零问题，diff 空白检查通过；受限入口不当作原帖已读证据。发布前另核精确暂存范围，推送后核远端 master。
- 接续：AgenticOS 发布授权 / 并发费用 / vault 恢复；BigMoeOnEdge 发行与文档漂移 / 同机数值性能；手册问卷分母 / 练习与真实任务差异 / 黄金集冻结。社媒原帖和评论仍待可读来源补证。
- 未执行：上游安装或测试、部署、登录、改账户 / 配置、调用模型 / 云服务、上传文档、下载权重 / 二进制 / 媒体、运行 Agent / shell 工具、做容器 / 数值 / 性能实验、完整视频观看或评论统计。本轮是资料与文档维护。
