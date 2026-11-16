<!-- markdownlint-disable MD013 -->

# AI 热点日报｜2026-11-17

- 采样：2026-11-17（Asia/Shanghai）07 时段；事件日期另列。daily 增星、API 累计量、Views 和视频计数均为抓取快照，不是自然日结算。
- 范围：官方综合、Python、TypeScript、JavaScript、Rust、Go、C++、Jupyter Notebook、Swift 九个 daily 页，有界抽样，不合成跨平台排名。
- 证据：A 为官方榜单 / API / 固定 SHA 文档和代码；B 为平台原帖及原生元数据；C 为聚合或受限入口。上游自述、静态核读、日报判断与运行验收分开。
- 获取：广泛搜索以二手日报为主，首组四条项目定向搜索为空；随后搜索含无关同名与平台摘要，未据此归因项目热度。网页工具对 X 403、YouTube / Instagram 限流，改用直接官方 HTTP、GitHub 连接器、原生列表 / oEmbed；搜索为空不表示没有讨论。
- 接续：最近日报 11-16；按项目目录、owner/repo、仓库 ID 去重，三页首次建档，Stitch Skills 原位刷新；不重写昨天四页，不把今天快照回填成过去的数据。

## 今日重点

- **技能增多，不等于效果已被证实。** Claude-BugHunter 综合 / Python +1,057；当前树有 83 个 skills，而 API 简介仍为 82。历史三题开关技能均 3/3，不能证明泛化增益；代码 MIT 与内容 CC BY 4.0 也要分开。[解读](../../projects/Claude-BugHunter/README.md)
- **论文写作自动化要查执行和证据链。** PaperOrchestra 综合 / Python +306；写作、引用 F1、生成绘图和最终 PDF 是不同验收对象。绘图 worker 直接执行生成的 Python，引用分数不代表论断有依据。[解读](../../projects/paper-orchestra/README.md)
- **成熟 ASR 仍有工程关注度。** Whisper Python +123；补录 2022 年首发项目，当前包 / Release 仍为 20250625。turbo 转写、英语翻译和说话人分离不能混作同一能力。[解读](../../projects/whisper/README.md)
- **设计插件需要真实的验收范围。** Stitch Skills 综合 / TypeScript +540，原页刷新来源与快照 / 上传 / 校验边界；最新 Release 仍是 05-18 的 v1.0，不写成今日更新。[解读](../../projects/stitch-skills/README.md)

## GitHub 热点项目

日增来自本轮官方 daily；API 为 stars / forks / open issues（含 PR），不是今天新增 issue 数。下面“新增”只指本仓库首次建档。

| 项目与动作 | 可核热度与版本 | 沿用分类 | 工程关注 |
| --- | --- | --- | --- |
| [Claude-BugHunter](../../projects/Claude-BugHunter/README.md)，新增 | 综合 / Python +1,057；7,394 / 1,145 / 19；[API](https://api.github.com/repos/elementalsouls/Claude-BugHunter)；插件 2.1.0，[v2.1](https://github.com/elementalsouls/Claude-BugHunter/releases/tag/v2.1)，UTC 06-05。 | Agent 框架与技能生态 | 技能 / engine / 主动测试、范围匹配、安装足迹、历史评测与双许可。 |
| [paper-orchestra](../../projects/paper-orchestra/README.md)，新增 | 综合 / Python +306；1,430 / 236 / 33；[API](https://api.github.com/repos/google-research/paper-orchestra)；本轮 [Releases](https://github.com/google-research/paper-orchestra/releases) 列表为空。 | 办公、商业与行业应用 | 远端数据、输出清理、引用匹配分母、生成代码执行与研究复核。 |
| [whisper](../../projects/whisper/README.md)，新增 | Python +123；112,852 / 13,668 / 185；[API](https://api.github.com/repos/openai/whisper)；[PyPI](https://pypi.org/pypi/openai-whisper/json) / 源码 20250625；[v20250625](https://github.com/openai/whisper/releases/tag/v20250625) 于 UTC 2025-06-26 发布。 | 语音、视频与多模态 | 本地推理与首次下载、turbo 非翻译、幻觉 / 语言差异、CER / WER 和回听。 |
| [stitch-skills](../../projects/stitch-skills/README.md)，刷新 | 综合 / TypeScript +540；9,718 / 1,241 / 19；[API](https://api.github.com/repos/google-labs-code/stitch-skills)；[v1.0](https://github.com/google-labs-code/stitch-skills/releases/tag/v1.0)，UTC 05-18。 | 前端、UI 与 Agent 交互层 | 浏览器采集与静态导出、真实云端写入、凭据 / 日志和有限 validator。 |

- 三个新上游未命中既有目录 / 主上游；Stitch Skills 保持同 ID 原目录。实际项目数 **1,038 → 1,041**，首页同步四个既有分类，不扩分类。
- 已建档观察：Univer +1,878、Modern Web Guidance +1,200、LoopForge +1,016、SkillEvaluator +953、Open Code Review +946、Chrome DevTools MCP +837、AG-UI +790、Plannotator +689、FFmpeg Skill +475。本轮仅记录这些榜单值，不重复建档或宣称重新审查其实现。
- 后续候选：Omnigraph Rust +228、BigMoeOnEdge C++ +83、Agenticos Python +56；保留独立核读。普通框架、邮箱、历史地图与系统工具不会只因上榜就被归作 AI 核心，本轮也不是全榜穷尽。
- 官方 daily 页：[综合](https://github.com/trending?since=daily)、[Python](https://github.com/trending/python?since=daily)、[TypeScript](https://github.com/trending/typescript?since=daily)、[JavaScript](https://github.com/trending/javascript?since=daily)、[Rust](https://github.com/trending/rust?since=daily)、[Go](https://github.com/trending/go?since=daily)、[C++](https://github.com/trending/c++?since=daily)、[Jupyter Notebook](https://github.com/trending/jupyter-notebook?since=daily)、[Swift](https://github.com/trending/swift?since=daily)。

## X 观察

本轮可读的 [OpenAI 账号](https://x.com/OpenAI)由 [Whisper 官方首发页](https://openai.com/index/whisper/)页脚回链确认身份；新项目的搜索入口与它分开，不建立未经证明的项目关联。

- [2026-11-16 科研使用研究原帖](https://x.com/OpenAI/status/2122380010287960095)与 [oEmbed](https://publish.twitter.com/oembed?url=https://x.com/OpenAI/status/2122380010287960095)的作者、日期和核心正文一致。原帖明确标出 **253.8K Views**，作为截至本轮的累计观察；其余裸数字不猜测为赞 / 转发 / 评论，也不算今日新增。
- 原帖称研究覆盖 1,800 多名参与者、科学家自报生产率接近翻倍。[官方研究网页](https://openai.com/index/science-at-the-frontier/)进一步区分：使用分析为 **1,819 人 / 580,186 条科学消息**，2026-08-20 至 09-22；问卷分析为 **251 人**，09-30 至 10-07。生产率问题每项有 249–251 个回答，自报同质工作无 AI 需约 **1.9 倍时间**；不能把 1,819 人都当作这项问卷分母。
- 官网明确：生产率是自报，发现加速是预期，不能建立因果效应。该研究不评估本轮 PaperOrchestra、Whisper 或 Stitch Skills；未阅读全文 PDF，不能称为独立复核该研究。
- 讨论线索是“省时”如何转成可复核成果，以及实验、经费与人员瓶颈。本轮只看到少量可见回复，未系统采样评论；不把选择性回复写成平台舆论比例。
- [PaperOrchestra 实时搜索](https://x.com/search?q=%22PaperOrchestra%22&f=live)与 [Claude-BugHunter 实时搜索](https://x.com/search?q=%22Claude-BugHunter%22&f=live)直接 HTTP 200 后转登录；没有取得两项目可独立核验的当日原帖 / 互动增量，不能声称它们在 X 爆发。

## Instagram 观察

- [aiagents 标签](https://www.instagram.com/explore/tags/aiagents/)直接 HTTP 200 转 popular，标题为 **129K reels**。宽泛话题累计量不能归因本轮项目，也不代表今日新增。
- [paperorchestra 标签候选](https://www.instagram.com/explore/tags/paperorchestra/)HTTP 200 转同名 popular，只能读标题与登录入口，没有可核项目帖子或计数；同名不构成项目身份。
- [OpenAI 官方账号入口](https://www.instagram.com/openai/)由前述官网页脚回链，直接访问转登录 / HTTP 429。身份可追溯与帖子可读是两件事。
- 本轮未取得项目级原帖、日期、互动与评论样本，不制作 Instagram 项目排名；未登录或发布。

## YouTube 观察

原生搜索列表与 oEmbed 交叉核元数据，均为第三方内容；没有完整观看或系统评论审阅。相对年龄不反推精确日期，累计播放不当日增量。

| 视频 | 可核信息 | 讨论与边界 |
| --- | --- | --- |
| [5 AI agents write a research paper: PaperOrchestra explained](https://www.youtube.com/watch?v=VDMk_DF-hgw) | [PaperOrchestra 原生搜索](https://www.youtube.com/results?search_query=PaperOrchestra)列 **46 views / 1d ago / 5:42**，作者 paper2video；[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=VDMk_DF-hgw&format=json)标题 / 作者一致。 | 近期解说观察，不是 Google 官方演示，也不能证明生成论文或引用正确。搜索还有多条数月前视频，不能都计为本日传播。 |
| [OpenAI Whisper Demo: Convert Speech to Text in Python](https://www.youtube.com/watch?v=HbY51mVKrcE) | [OpenAI Whisper 原生搜索](https://www.youtube.com/results?search_query=OpenAI+Whisper)列 **167,916 views / 4y ago / 4:59**，作者 Rob Mulla；[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=HbY51mVKrcE&format=json)匹配。 | 历史教程累计背景，不能证明当前包的 turbo、版本兼容或中文转写质量；没有把 16 万播放写成今日热度。 |

两条 watch 直接 HTTP 200，但静态提取仅站点壳。网页工具对原生搜索限流；HTTP / oEmbed 成功不代表已看视频、核评论或独立重现实验。

## 讨论与争议：事实、判断和待验证

下面是来源导出的工程议题，不包装成已统计的社媒争论；实现链接与详细范围见对应项目页。

| 议题 | 已核事实 | 判断 / 待验证 |
| --- | --- | --- |
| AI 提速的分母 | 官方网页把 1,819 人使用数据与 251 人问卷分开，1.9 倍为自报。 | 测固定任务的时间、质量、审阅成本和失败率；不能写成已证实科研成果翻倍。 |
| 技能数量与能力增益 | BugHunter main 83 skills；历史三题两条件均满分，skills-on 费用更高。 | 先排除天花板与记忆题，再评陌生任务、误报与单位成功成本。 |
| 范围策略与执行权限 | BugHunter 有 host 匹配、deny 优先、默认拒绝；复制安装会改宿主目录和可选配置。 | 核所有工具、重定向、网络和文件路径，不把一段范围代码当系统隔离证据。 |
| 论文生成与科研真实性 | PaperOrchestra 编排写作和 PDF；绘图直接 exec，引用分数按解析出的 ID 集合计算。 | 分别核执行环境、数据、引文支持率与覆盖率，不能以自动评分取代研究复核。 |
| 本地 ASR 与准确记录 | Whisper 可本地推理，但模型卡承认幻觉 / 重复和语言差异；缺权重会下载。 | 固定模型做领域评测并回听，无声与关键数字单列；部署本地不证明输出正确。 |
| 静态导出与采集行为 | Stitch 先以浏览器加载页面 / 可选 auth script，再整理导出；上传另创建 screen。 | 核采集脚本、登录态、页面数据与云端资源，不能仅看最终 HTML 没脚本。 |
| 校验通过与可用交付 | Stitch React validator 只做有限 AST / Props / 颜色检查。 | 继续做编译、业务、可访问性与视觉验收，不把单个脚本扩大为全面 QA。 |

## 验证范围与接续

- 来源：九页 official daily、四个唯一仓库 ID、固定 main SHA、完整目录树与发行列表；只对相关 README / 许可 / 清单 / 安装 / 权限 / 执行 / 评测代码抽样核读，未审计全仓。PyPI、X 原帖 / oEmbed / 官网研究网页、Instagram 访问状态和两条 YouTube 元数据另核。
- 文档：三个新增七节页、Stitch Skills 原页、同日四平台日报、首页四类 / 最新入口 / 实际总数与 TODO。原有 AGENTS.md 修改保留且不纳入本次提交。
- 检查通过：四项目 28 个固定章节、日报七节、四个分类入口、1,041 个实际目录、七文件 346 个本地链接；72 个本轮来源 URL 均有已取得的来源或明确访问证据，其中 34 个固定 SHA 文件。七文件 Markdown lint 零问题，diff 空白检查通过；受限入口不充当原帖已读证据。发布前另核精确暂存范围与远端 master。
- 接续：BugHunter 多宿主安装 / 范围和陌生题 paired eval；PaperOrchestra 引文匹配覆盖、生成代码环境、输出覆盖与日志密钥；Whisper 中文 / 无声 / 数字 / 领域 CER 与实际听评；Stitch 浏览器采集、上传数据 / 云资源及 validator 外的 QA。Omnigraph、BigMoeOnEdge、Agenticos 留待后续来源核读。
- 未执行：上游安装、扫描 / 探测任何目标、运行其测试或 Agent、调用模型 / 学术检索 API、下载权重 / 发行二进制 / 媒体、处理录音、生成论文 / 图、登录、改宿主技能 / MCP / shell 配置、采集或上传页面、部署、评论发布、完整视频观看或系统评论统计。本轮是文档和来源验证。
