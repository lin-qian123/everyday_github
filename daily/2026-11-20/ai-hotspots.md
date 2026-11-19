<!-- markdownlint-disable MD013 -->

# AI 热点日报｜2026-11-20

- 采样：2026-11-20（Asia/Shanghai）07 时段；事件 / 发行日期单列。GitHub `stars today`、API 累计数与视频播放量均为本轮快照，不是自然日结算。
- 范围：GitHub 综合、Python、TypeScript、JavaScript、Go、Rust、C++、Swift、Jupyter Notebook、Shell 十个官方 daily 页的有界抽样；重点新增三份项目档案，不合成跨平台榜单，不声称覆盖全部新上榜项目。
- 证据：A 为官方榜单 / API / 固定 SHA 文件，B 为平台原生列表及元数据，C 为搜索 / 聚合 / 受限入口。上游声明、静态核读、本文判断和运行验收分别标识。
- 获取：广泛搜索混入聚合材料、旧闻及同名条目；四条项目 / 社媒定向搜索为空。项目筛选采用官方 Trending HTTP 与 GitHub 连接器，社媒采用原生 HTTP / oEmbed；搜索缺口不证明没有讨论。
- 接续：查 `projects/` 目录、上游 owner/repo 和仓库 ID 后建档，复用首页三个既有分类。沿用前次文档组织，所有热度与版本均在本轮重新读取。

## 今日重点

- **本地视频先分清许可、内存与速度。** FreeVideo Python +99，v0.6.5 北京时间今天凌晨发布。8GB 显存是上游最低适配声明，Mac 路径仍标实验性；48 / 60 fps 导出使用插帧，不能等同原生生成帧率。[项目解读](../../projects/FreeVideo/README.md)
- **知识库的同步、AI 和升级是不同边界。** edgeever TypeScript +57；MCP 有只读 / 完全访问 Token，AI 默认直连所选服务，Web 还有实例中转兜底；一键安装器默认每日更新，数据库回退另需备份。[项目解读](../../projects/edgeever/README.md)
- **解码提速要同时保留慢样本。** splash C++ +61；1.7.0 的作者回放有 1.46× 解码 / 1.23× 请求中位速度改善，也披露部分 decode 回退和四会话首 token 总耗时增加。[项目解读](../../projects/splash/README.md)

## GitHub 热点项目

API 依次为 stars / forks / open issues（含 PR）；不是本日新增 issue 数。首次建档不代表今日首发，同仓库跨语言上榜不累加。

| 项目与动作 | 本轮热度 / 发行 | 沿用分类 | 工程关注 |
| --- | --- | --- | --- |
| [FreeVideo](../../projects/FreeVideo/README.md)，新增 | Python +99；3,421 / 453 / 731；[API](https://api.github.com/repos/FlashML-org/FreeVideo)；[v0.6.5](https://github.com/FlashML-org/FreeVideo/releases/tag/v0.6.5)，UTC 11-19 20:54，北京时间 11-20 04:54，非预发行。 | 语音、视频与多模态 | 低显存调度 / 实际耗时、插帧、模型许可及浏览器草稿范围。 |
| [edgeever](../../projects/edgeever/README.md)，新增 | TypeScript +57；3,437 / 1,788 / 67；[API](https://api.github.com/repos/tianma-if/edgeever)；[v2.30.0](https://github.com/tianma-if/edgeever/releases/tag/v2.30.0)，UTC 11-18，非预发行。 | 记忆层与个人 AI 基础设施 | 离线同步、附件完整性、Token、模型数据出口和自动升级。 |
| [splash](../../projects/splash/README.md)，新增 | C++ +61；2,476 / 243 / 167；[API](https://api.github.com/repos/incoai/splash)；[1.7.0](https://github.com/incoai/splash/releases/tag/1.7.0)，UTC 11-17，非预发行。 | 模型、训练与推理基础设施 | M3+ / macOS 26.4+、首 token、并发、默认近似缓存与认证。 |

- 三个唯一仓库 ID 为 `1368913638 / 1281033762 / 1376380844`；实际项目目录 **1,047 → 1,050**。
- 已建档项目的综合 daily 快照：Superpowers +2,029、Claude-BugHunter +1,353、last30days-skill +952、CLI-Anything +899、Firecrawl +795、App Store Compliance +542、Stitch Skills +303、OpenVINO +246。这里只观察热度，没有重审这些项目的实现、版本或效果。
- 新候选来自语言页，因此三项并非综合榜前三。通用 Web 框架、下载器和系统工具不只因上榜就归入 AI 核心；同名或迁移候选仍需身份核验。
- 来源：[综合 daily](https://github.com/trending/?since=daily)、[Python](https://github.com/trending/python?since=daily)、[TypeScript](https://github.com/trending/typescript?since=daily)、[JavaScript](https://github.com/trending/javascript?since=daily)、[Go](https://github.com/trending/go?since=daily)、[Rust](https://github.com/trending/rust?since=daily)、[C++](https://github.com/trending/c++?since=daily)、[Swift](https://github.com/trending/swift?since=daily)、[Jupyter Notebook](https://github.com/trending/jupyter-notebook?since=daily)、[Shell](https://github.com/trending/shell?since=daily)，本轮均 HTTP 200；动态页面后续会变化。

## X：官方身份可核，项目原帖缺口保留

| 入口与关联 | 本轮可读事实 | 热度 / 讨论边界 |
| --- | --- | --- |
| [@inco_ai](https://x.com/inco_ai)，由 [Splash 官网首发博客](https://inco.ai/blog/splash/)回链，账号也回链 inco.ai。 | HTTP 200，账号名称与简介可读，帖子区需登录；官网文章日期 2026-09-17。 | C 级观察入口，没有取得可验证的项目原帖 / 回复及互动量；不把官网首发文章当作今天的 X 传播。 |
| [FreeVideo / MiniMax 定向搜索](https://x.com/search?q=%22FreeVideo%22%20%22MiniMax%22&f=live) | HTTP 200 后进入登录引导。 | 未取得原帖，不把模型名称相同视为同一项目，也不推断转发规模。 |
| [splash / incoai 定向搜索](https://x.com/search?q=%22splash%22%20%22incoai%22&f=live) | HTTP 200 后进入登录引导。 | 没有本轮可统计的 Views、点赞、转发或评论样本。 |

GitHub 增星不换算成 X 热度；本节没有足够帖子样本总结群体立场。

## Instagram：宽泛聚合与受限项目入口

- [aiagents 标签入口](https://www.instagram.com/explore/tags/aiagents/)本轮 HTTP 200，转 popular 页面，标题可读 **129K reels**。这是宽泛主题累计聚合快照，不是今天新增、独立作者数或三个项目的传播量，四舍五入值也不能用于推断日增。
- [edgeever 标签入口](https://www.instagram.com/explore/tags/edgeever/)转登录并返回 HTTP 429；未取得项目原帖、官方账号归属、互动或评论。
- 两项均为 C 级观察入口。本轮没有可用于确认项目热点或统计争议的 Instagram 样本，不沿用历史访问结果充当当日证据。

## YouTube：近期视频与历史条目分别记录

下表来自原生检索列表，标题 / 作者再用 oEmbed 交叉核对；播放量均为累计值，相对发布时间保留列表原文。

| 条目与作者 | 本轮可核元数据 | 解释与限制 |
| --- | --- | --- |
| [FreeVideo: Run MiniMax H3 Locally with Just 8GB VRAM｜ComfyUI](https://www.youtube.com/watch?v=SET6nWjBNNE)，ABV — AI · Books · Validation | **661 次播放、3w ago、0:59**；[检索](https://www.youtube.com/results?search_query=FreeVideo+MiniMax+H3)、[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=SET6nWjBNNE&format=json)。 | B 级第三方历史元数据；标题提及本项目，未核视频内容及 v0.6.5 对应，不作为 8GB / 画质实测证据。同检索的 H3 V2 / Singularity V2 条目未自动归入本项目。 |
| [Splash 1.6.1 is INSANELY FAST! Local AI on M6 Mac Mini](https://www.youtube.com/watch?v=8dhcnt-G19M)，Execute Automation | **4,610 次播放、10h ago、16:27**；[检索](https://www.youtube.com/results?search_query=Splash+inco+inference)、[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=8dhcnt-G19M&format=json)。 | B 级近期第三方条目；标题版本为 1.6.1，不能视为 1.7.0 的独立基准。标题形容词不是本文验收结论；同名 SPLASH 学术会议视频排除。 |
| [EdgeEver Tutorial: Install and Use It Step by Step (Docker, Self-Hosted Notes)](https://www.youtube.com/watch?v=ZFQvQUDJLJI)，Tech On Cue | **12 次播放、2d ago、6:35**；[检索](https://www.youtube.com/results?search_query=edgeever)、[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=ZFQvQUDJLJI&format=json)。 | B 级第三方近期教程元数据；具体版本、部署安全与恢复步骤未核，不用少量播放量推断质量或全平台传播。 |

三个 watch 页面均 HTTP 200，但仅取得页面壳；没有完整观看、读取全部描述或采集评论。上述条目说明可观察的视频入口，不能解释今天 GitHub 上榜的因果。

## 讨论与争议：把宣传转成可检验的问题

下列是依据上游资料提出的工程判断，**不是已统计的社媒争论**；固定 SHA 证据见项目页。

| 议题 | 已核资料 | 判断 / 可验证方向 |
| --- | --- | --- |
| 低显存是否意味着快速、本地是否意味着可任意商用 | FreeVideo 有分层卸载；Mac 作者例中 10 秒 1344×768 轻量视频约需 42 分钟；模型许可不同于代码 Apache-2.0。 | 同时记录完整耗时、峰值资源、画质与对应模型条款；不把能运行扩写成低成本高质量。 |
| 60 fps 导出是否证明原生生成能力 | v0.6.5 发行说明称 48 / 60 fps 使用 GPU 生成中间帧。 | 保存原生帧数及导出路径，检查运动伪影，不混淆补帧与模型采样。 |
| 自托管笔记是否没有第三方数据流 | edgeever 文档列客户端模型直连、Web 实例中转及可选图床；隐私政策有具体适用范围。 | 对所选配置逐条画出数据出口，只读 Token 也可能允许读取敏感全文。 |
| 一键更新是否等于可回滚升级 | edgeever 一键安装默认每日更新，migration 不随镜像回退撤销。 | 固定正式版，先备份并在独立实例恢复；健康检查不能代替内容完整性验收。 |
| decode 加速是否等于用户更早看到答案 | splash 1.7.0 有解码中位改善，也披露部分回退和并发首 token 总耗时增加。 | 分开报告 TTFT、队列等待、decode、请求全程和任务正确率，保留慢样本。 |
| 固定 seed 是否足够复现 | splash 默认 int8 cached state 和自动验证行数均可影响输出。 | 同时固定权重、缓存精度、验证模式、前缀、并发及版本，再比较 token / 任务差异。 |

## 验证范围与接续

- 本轮读取十个官方 daily 页，三个项目的 API / main SHA / 发行列表与完整目录树，并抽读固定 README、许可、配置、运行文档及少量实现；完整树清单不等于全仓代码审计。FreeVideo 附带模型许可与其 README 指向的当前来源文本一致，不代表全面法律适用性评估。
- 交付：三个七节项目说明、本日报、首页三个既有分类 / 最新日期 / 实际项目总数和 TODO；已有 `AGENTS.md` 修改保持原样并排除提交。检查通过：21 个项目章节、日报七节、三个分类、1,050 个目录、六文件 356 个本地链接及 60 个有当轮来源 / 访问证据的 URL（含 22 个固定 SHA 文件）；Markdown lint 零问题、空白检查通过。提交前另核精确暂存范围，推送后核远端 master。
- 接续：FreeVideo 目标硬件 / 原生帧率与画质；edgeever 附件、冲突同步、只读权限和恢复；splash 同权重的数值、缓存与并发性能。X / Instagram 原帖、视频版本对应与评论样本仍待补证；vllm-ascend 等其他候选留待按来源筛选。
- 未执行：上游安装或运行、个人知识库连接 / 导入、MCP 授权、迁移、云开通、模型或 Agent 调用、宿主配置修改、部署、权重 / 二进制 / 媒体下载、设备 / 数值 / 性能 / 隔离实验、完整观看和评论统计。资料核验与这些运行验收分开。
