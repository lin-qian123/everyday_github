<!-- markdownlint-disable MD013 -->

# AI 热点日报｜2026-11-12

- 采样：2026-11-12（Asia/Shanghai）07 时段；GitHub daily 日增、累计 stars、X Views 和视频播放均为分时快照，不是自然日结算。发布日期和历史教程单列。
- 范围：官方综合、Python、TypeScript、Rust、Go、JavaScript、C++、Swift、Jupyter Notebook 九页；社媒有界观察，不合成跨平台排名。
- 证据：A 为官方榜单 / API / 固定 SHA 文件；B 为平台原生元数据；C 为聚合、受限观察入口。静态核读、作者评测与本轮实际运行分别表述。
- 获取：广泛搜索多为汇总或历史线索，search-layer 无有效候选；以九页官方 HTTP 榜单选样，连接器核五个仓库 ID、主线 SHA、目录树、发行和引用文件。连接器 `/readme` 端点返回 400 后改读固定 SHA raw 文件；不是仓库无 README。X 搜索 403 / 登录，但官网回链账号与指定原帖可直接核读。

## 今日重点

- **给 Agent 的 Web 指南也要核数据出口**：Modern Web Guidance 源仓库综合 / TypeScript +133；1.0 发布带来了可核 X / YouTube 活动。本地检索与默认开启的遥测须分开说明。[解读](../../projects/modern-web-guidance-src/README.md)
- **代码顾问和实施者分工**：improve 综合 +333；先调查与写计划，`execute` 才另调执行者。低价模型执行是否省总成本仍待同条件对照。[解读](../../projects/improve/README.md)
- **交付流程与平台权限一起看**：LoopForge Go +76；v0.3.6 新发行。脚本 / 人工关卡有价值，默认公网监听、开放注册与受信任团队可见性也必须部署前处理。[解读](../../projects/LoopForge/README.md)
- **高热沙箱原位纠正旧页**：OpenSandbox Python +88；按同 ID 确认组织迁移，更新 3 月旧说明。稳定 1.2.0、RC 镜像、包版本及签名缺口不能混写。[解读](../../projects/OpenSandbox/README.md)
- **经典 RAG 课重新上榜**：RAG From Scratch Notebook +164；是历史课程首次建档，旧依赖、模型名、tracing 与缺少根许可须先检查。[解读](../../projects/rag-from-scratch/README.md)

## GitHub 热点项目

日增取指定官方 daily 页。API 数为 stars / forks / open issues（含 PR）；“新增”指本仓库首次建档，语言榜位置不等于全站排名。

| 项目与动作 | 可核热度与版本 | 沿用分类 | 工程关注 |
| --- | --- | --- | --- |
| [improve](../../projects/improve/README.md)，新增 | 综合 +333；10,810 / 441 / 18；[API](https://api.github.com/repos/shadcn/improve)；发行列表为空，技能元数据 1.0.0，主线最后提交 UTC 09-12。 | Agent 框架与技能生态 | 顾问只写计划、执行者 worktree、漂移门控和总费用实测。 |
| [modern-web-guidance-src](../../projects/modern-web-guidance-src/README.md)，新增 | 综合 / TypeScript +133；1,704 / 138 / 366；[API](https://api.github.com/repos/GoogleChrome/modern-web-guidance-src)；[npm CLI 1.0.0](https://registry.npmjs.org/modern-web-guidance/latest)，源仓库 audit-data 为审计预发行。 | 前端、UI 与 Agent 交互层 | 源 / 分发仓库、Baseline、扫描覆盖、默认遥测、代码 / 指南双许可。 |
| [LoopForge](../../projects/LoopForge/README.md)，新增 | Go +76；313 / 60 / 57；[API](https://api.github.com/repos/Tencent/LoopForge)；[v0.3.6](https://github.com/Tencent/LoopForge/releases/tag/v0.3.6)，UTC 11-11；[Local npm 0.2.2](https://registry.npmjs.org/loopforge-cli/latest)。 | Coding Agents 与终端助手 | 初始管理员、默认注册、全员列表可见、Docker socket、Local 版本与迁移。 |
| [rag-from-scratch](../../projects/rag-from-scratch/README.md)，新增 | Notebook +164；9,845 / 2,268 / 46；[API](https://api.github.com/repos/langchain-ai/rag-from-scratch)；发行列表为空，主线最后提交 UTC 2025-06-26。 | AI 学习与教育资源 | 历史依赖 / prompt / 模型、外部 tracing、检索与引用评估、许可缺口。 |
| [OpenSandbox](../../projects/OpenSandbox/README.md)，原位刷新 | Python +88；17,201 / 1,630 / 210；[API](https://api.github.com/repos/opensandbox-group/OpenSandbox)；[1.2.0](https://github.com/opensandbox-group/OpenSandbox/releases/tag/release-1.2.0) 稳定，[rc.2](https://github.com/opensandbox-group/OpenSandbox/releases/tag/release-1.2.1-rc.2) 于 UTC 11-11 预发行；[server PyPI](https://pypi.org/pypi/opensandbox-server/json) 为 1.2.0。 | 前端、UI 与 Agent 交互层 | 迁移同 ID、server / SDK / 镜像、签名缺口、网络 / Vault 和 warm 成功分母。 |

- 去重：比对 `projects/` 目录、完整 owner/repo 和仓库 ID；四个新目录、一个原位刷新，实际目录 1,023 → 1,027。旧 `alibaba/OpenSandbox` API 明确迁移到 ID 1118085970，与 `opensandbox-group/OpenSandbox` 一致。
- 已有高热只记录，不据此重审实现：Astryx 综合 +2,842、Sure +1,079、agent-skills +788、agent-browser +712、HA-MCP +640。Sure 昨日已建档，未再新增。
- 选择是有限抽样：Sherlock、Topcoat、通用算法和侧载工具不因增长高就并入 AI 核心项目；`ed-donner/agents` 等同名目录冲突不覆盖旧页。未选中不表示质量差或没有活动。
- 官方页：[综合](https://github.com/trending?since=daily)、[Python](https://github.com/trending/python?since=daily)、[TypeScript](https://github.com/trending/typescript?since=daily)、[Rust](https://github.com/trending/rust?since=daily)、[Go](https://github.com/trending/go?since=daily)、[JavaScript](https://github.com/trending/javascript?since=daily)、[C++](https://github.com/trending/c++?since=daily)、[Swift](https://github.com/trending/swift?since=daily)、[Jupyter Notebook](https://github.com/trending/jupyter-notebook?since=daily)。

## X 观察

[Chrome 官方文档](https://developer.chrome.com/docs/modern-web-guidance)回链 [@ChromiumDev](https://x.com/ChromiumDev)，据此确认账号关系，再读取原帖与 oEmbed。下列为原帖日期和明确标注的 Views；无每日增长序列，不推断 GitHub 增长原因。

| 原帖 | 可核快照 | 讨论与证据边界 |
| --- | --- | --- |
| [Modern Web Guidance 1.0 发布](https://x.com/ChromiumDev/status/2120201406820884794)，11-10 | 原帖 136.5K Views；[oEmbed](https://publish.twitter.com/oembed?url=https://twitter.com/ChromiumDev/status/2120201406820884794) 作者 / 日期相符。 | 宣布与 Firefox、MDN、Edge 合作和 200+ 指南。可见少量 MDN / Edge 回复支持跨浏览器合作；有限展示不构成观点分布或全体开发者共识。 |
| [模型边缘情况与指南评测](https://x.com/ChromiumDev/status/2120519875932123327)，11-11 | 原帖 9,229 Views；[oEmbed](https://publish.twitter.com/oembed?url=https://twitter.com/ChromiumDev/status/2120519875932123327) 作者 / 日期相符。 | “超过 40% 边缘情况失败”是作者评测宣传，需回到指定任务与 grader；不能外推全部模型、线上缺陷率或用户体验。 |

[improve 搜索](https://x.com/search?q=shadcn%20improve&f=live)及 [Modern Web Guidance 搜索](https://x.com/search?q=%22modern%20web%20guidance%22&f=live)在网页工具返回 403；[LoopForge 搜索](https://x.com/search?q=LoopForge&f=live)直接 HTTP 转登录。没有可核其他项目当天原帖 / 评论样本，未据此判断无人讨论。原帖时间采用页面日期，不把未声明的显示时区换算成北京时间。

## Instagram 观察

- [aiagents 标签](https://www.instagram.com/explore/tags/aiagents/)跳转 popular 聚合，标题约 129K reels，仅代表宽泛主题；不能归给 improve、LoopForge 或今日新增项目。
- [retrievalaugmentedgeneration 标签](https://www.instagram.com/explore/tags/retrievalaugmentedgeneration/)直接 HTTP 转登录后 429；[rag 标签](https://www.instagram.com/explore/tags/rag/)网页工具限流，且名称本身有歧义。
- 本轮没有能绑定项目、作者、日期与互动量的 Instagram 原帖；无项目排名、当日增量或评论共识结论。没有登录或发布。

## YouTube 观察

使用官网 / README 回链、原生搜索或播放列表，再用 oEmbed 绑定标题和作者。这里只核元数据，没有完整观看或统计全部评论。

| 视频 | 可核元数据 | 使用边界 |
| --- | --- | --- |
| [Modern Web Guidance 官方概览](https://www.youtube.com/watch?v=PsrHq5F_BAc) | Chrome for Developers；[原生搜索](https://www.youtube.com/results?search_query=Modern+Web+Guidance)显示 14,139 views、1d ago；[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=PsrHq5F_BAc&format=json)标题 / 作者一致，官网回链同一视频。 | 能确认官方发布材料存在，不能据此验收性能、无障碍或隐私。相对年龄不反推精确日期。 |
| [RAG From Scratch Part 1](https://www.youtube.com/watch?v=wd7TZ4w1mSw) | LangChain；README 回链的[原始播放列表](https://www.youtube.com/playlist?list=PLfaIDFEXuae2LXbO1_PKyVJiQ23ZztA0x)原生卡片为约 270K、2y ago；[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=wd7TZ4w1mSw&format=json)标题 / 作者一致。 | 是历史课，不是今日新视频。搜索工具缓存另报 248,675，采用原生列表的近似值，不把快照差当播放增长。 |

网页工具读取 RAG watch 页返回 429；列表和 oEmbed 经直接 HTTP 成功，分别记录证据，未称 watch 页或完整内容已验收。播放量是累计值，不与日增 stars 合并排名。

## 讨论与争议：事实、判断和待验证

下表主要是源码和文档暴露的工程议题，不能包装成已统计的社媒争论。

| 议题 | 已核事实 | 判断 / 接续 |
| --- | --- | --- |
| 本地 Web 指南与数据出口 | Chrome README 说明本地检索；logger 普通环境默认遥测，含 query / guide 等，提供关闭变量。 | 区分取包、安装、检索和遥测；敏感查询先治理，再做实际网络验证。 |
| 模型评测与业务收益 | 指南 README 有指定任务 / assertions 的 guided 对照；扫描只覆盖约 20% 的指南库。 | 不能把分数当所有浏览器或全站质量；独立验键盘、fallback、真实性能和业务行为。 |
| 计划分工与成本 | improve 顾问写计划、执行者独立 worktree；没有本轮费用实验。 | 合计调查、执行、返修成本，同时看成功率；计划质量与廉价执行能力都可能成为瓶颈。 |
| 流程关卡与信任边界 | LoopForge 默认开放注册，登录用户可列全部项目；控制面有 Docker socket。 | 人工审批和容器不能代替账号准入、团队边界和宿主权限治理。 |
| 沙箱性能与供应链 | OpenSandbox warm 并发 20 仅 51/100 成功；umbrella 签名 / provenance 有明确缺口。 | 同时报分母与尾延迟；digest 对应不等于来源证明，RC 标记和包组合逐项核验。 |
| RAG 教学与可复现性 | 入门含远端 API、Hub prompt、tracing 和未锁依赖，目录无根 LICENSE。 | 先固定资料 / prompt / 包，确认许可与出口，再做检索、引用和拒答评估。 |

细节与固定 SHA 来源见五份项目页；没有安装、推理、性能、权限或安全实测结论。

## 验证范围与接续

- 已核：九页 daily、五个唯一仓库 ID、完整主线目录树和 SHA、发行状态、指定文件；OpenSandbox 旧 API 迁移目标与新 ID 相同。X 两原帖 / oEmbed 与两个官方 YouTube 视频元数据按上述边界记录。
- 文档验证：五页 35 个固定章节、五个唯一仓库 ID、四类首页入口、1,027 个实际目录与 327 个本地链接通过；77 个范围内外部 URL 对应已读来源或明确的访问边界，其中 29 个固定 SHA 文件已读取。X 搜索、Instagram 原帖与 RAG watch 的受限情况如上。8 个 Markdown 文件 lint 零问题；本轮仅纳入 8 个任务文件，AGENTS.md 原修改保留在提交外。
- 未做：上游安装 / 构建 / 测试、模型或付费 API 调用、容器 / 微虚机创建、资料上传、技能安装、账号登录、GitHub issue / SOP 写入、人工全片观看、完整评论抓取、遥测抓包、隔离 / 性能 / 验签实验。
- 接续：improve 漂移与总费用；Chrome 分发版本 / 遥测 / 兼容；LoopForge 初始账号 / 可信团队 / 执行面 / 迁移；OpenSandbox 稳定与 RC / 逐语言 Vault / 来源证据 / 成功率；RAG 历史依赖 / tracing / 许可 / 引用评估。skills / agents 同名目录的 owner-aware 键仍待设计。
