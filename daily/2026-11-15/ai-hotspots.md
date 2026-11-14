<!-- markdownlint-disable MD013 -->

# AI 热点日报｜2026-11-15

- 采样：2026-11-15（Asia/Shanghai）07 时段；GitHub daily、累计 stars 与视频播放均为抓取时快照，不是自然日结算。社媒事件日期另列。
- 范围：官方综合、Python、TypeScript、JavaScript、Rust、Go、C++、Jupyter Notebook、Swift 九个 daily 页，有界抽样，不合成跨平台热度排名。
- 证据：A 为官方榜单 / API / 固定 SHA 文档或代码；B 为平台原生元数据与原帖；C 为聚合或受限入口。上游自述、静态核读、本日报判断与实际运行分开。
- 获取：广泛检索主要命中汇总；四条项目定向 X / Instagram / YouTube 搜索无结果，改用官方 Trending HTTP、GitHub 连接器及平台直接 HTTP。空搜索不证明没有讨论。没有采用二手汇总中的性能或安全结论。
- 接续：最近已发布日报为 11-14；本轮按目录、完整 owner/repo 和仓库 ID 去重，三个项目首次建档。历史项目与来源不重建、不把当前快照回填到过去。

## 今日重点

- **技能评测要检查缺失分母与真实门控。** NVIDIA SkillEvaluator Python +168；0.9.0 新增预算与 baseline 管理，主线三层 CI 仅 Tier 1 阻断，Tier 2 / Tier 3 为 advisory。[解读](../../projects/SkillEvaluator/README.md)
- **交易工作流的人工关卡不等于账户权限。** Claude Trading Skills 综合 / Python +556；将研究、风险与复盘制品串起来，但 release 列表仍为空，流程不构成收益证据。[解读](../../projects/claude-trading-skills/README.md)
- **Agent 接上 UI 后仍需服务端授权。** AG-UI 综合 / TypeScript +9；旧项目首次收录，以 1.0 冻结规范和独立包版本理解中断 / 恢复、状态与兼容。[解读](../../projects/ag-ui/README.md)

## GitHub 热点项目

日增取本轮官方 daily；API 数为 stars / forks / open issues（含 PR），与榜单可能因采样时刻不同略有差异。“新增”指本仓库首次建档，非项目今天才发布。

| 项目与动作 | 可核热度与版本 | 沿用分类 | 工程关注 |
| --- | --- | --- | --- |
| [claude-trading-skills](../../projects/claude-trading-skills/README.md)，新增 | 综合 / Python +556；4,762 / 988 / 62；[API](https://api.github.com/repos/tradermonty/claude-trading-skills)；release 列表为空，根清单 0.1.0 为开发快照。 | 办公、商业与行业应用 | YAML 权威流程、数据来源、宿主权限、无 key / 离线区别、维护自动化副作用。 |
| [SkillEvaluator](../../projects/SkillEvaluator/README.md)，新增 | Python +168；1,248 / 145 / 33；[API](https://api.github.com/repos/NVIDIA/SkillEvaluator)；[v0.9.0](https://github.com/NVIDIA/SkillEvaluator/releases/tag/v0.9.0)，UTC 11-13；[PyPI](https://pypi.org/pypi/skillevaluator/json) 同为 0.9.0。 | Agent 框架与技能生态 | 静态质量 / 扫描 / 激活 / 对照增益；CI advisory、失败臂与预算、模型出口。 |
| [ag-ui](../../projects/ag-ui/README.md)，新增 | 综合 / TypeScript +9；17,334 / 1,665 / 592；[API](https://api.github.com/repos/ag-ui-protocol/ag-ui)；[11-13 发行](https://github.com/ag-ui-protocol/ag-ui/releases/tag/release%2F2026-11-13) 更新 LangGraph 包；[core npm 1.0.4](https://registry.npmjs.org/@ag-ui%2Fcore/latest) / [LangGraph npm 0.0.46](https://registry.npmjs.org/@ag-ui%2Flanggraph/latest)。 | 前端、UI 与 Agent 交互层 | 协议 1.0 与各包 semver、consumer 中断覆盖、state 信任边界、重放与业务幂等。 |

- 三个唯一 ID 均未命中既有项目身份，目录 1,032 → 1,035，首页同步三个既有分类；没有扩展分类。
- 已建档观察：Modern Web Guidance 综合 +1,225、Chrome DevTools MCP +673、Codex Security TypeScript +599、Sure 综合 +659、Plannotator 综合 +412。只记录榜单，没有复审这些实现；最近已深读的项目保留原页，优先补充本轮三个未建档项目。
- 其他候选：VieNeu-TTS、PyRIT 等仍值得后续按模型 / 数据 / 执行权限核读；通用监控、WiFi、网络与备份工具不因排名高就列作 AI 核心项目。此处不是全榜穷尽收录。
- 官方页：[综合](https://github.com/trending?since=daily)、[Python](https://github.com/trending/python?since=daily)、[TypeScript](https://github.com/trending/typescript?since=daily)、[JavaScript](https://github.com/trending/javascript?since=daily)、[Rust](https://github.com/trending/rust?since=daily)、[Go](https://github.com/trending/go?since=daily)、[C++](https://github.com/trending/c++?since=daily)、[Jupyter Notebook](https://github.com/trending/jupyter-notebook?since=daily)、[Swift](https://github.com/trending/swift?since=daily)。

## X 观察

AG-UI 固定 README 回链 [CopilotKit 账号](https://x.com/CopilotKit)。网页工具读取该账号 403，但直接 HTTP 可读资料与部分原帖；下面两条原帖的作者 / 日期 / 正文均与各自 oEmbed 一致。仅列有明确标签的 Views，不把裸数字猜成点赞、转发或评论数。

| 原帖 | 已核事实与热度快照 | 讨论 / 边界 |
| --- | --- | --- |
| [AG-UI 首发](https://x.com/CopilotKit/status/1921940427944702001)；[oEmbed](https://publish.twitter.com/oembed?url=https://x.com/CopilotKit/status/1921940427944702001) | 页面日期 **2025-05-12**；明确 317.4K Views。介绍 Agent 与前端交互和首批集成。 | 历史累计背景，不能写成今日新协议、当前 1.0 支持列表或本日传播量。 |
| [OpenBot 定时任务宣传](https://x.com/CopilotKit/status/2121665112293642240)；[oEmbed](https://publish.twitter.com/oembed?url=https://x.com/CopilotKit/status/2121665112293642240) | 页面日期 **2026-11-14**；明确 986 Views。CopilotKit 引述 OpenBot 的 Routines，称可让 bot 排程工作并通知结果。 | 同生态近期动态；不是 AG-UI 协议的新能力证明。只确认宣传正文，本轮未复审 OpenBot 的排程实现、可靠性或费用。 |

工程讨论线索：从实时对话扩展到长期工作后，应核对任务身份、授权有效期、失败重试与重复执行；这是本日报提出的验收问题，不是已统计的评论共识。

[SkillEvaluator 实时搜索](https://x.com/search?q=%22SkillEvaluator%22&f=live)直接 HTTP 200 后落在登录引导页；交易技能定向搜索无结果。两者本轮没有可核项目原帖或互动增量，不据此断言无人讨论；未系统审阅评论。

## Instagram 观察

- [aiagents 标签](https://www.instagram.com/explore/tags/aiagents/)直接 HTTP 转 popular 聚合，标题约 **129K reels**；这是宽泛主题累计量，与昨天相同也不能推出新增或下降，更不能归给今天三个项目。网页工具对这一入口限流。
- [copilotkit 同名候选](https://www.instagram.com/copilotkit/)转登录，未取得项目上游回链或帖子证据，不能确认账号身份。定向 AG-UI 检索无结果。
- 本轮没有项目级原帖、发布日期或可靠互动量，因此只保留观察入口，不制作平台项目排名、传播范围或争议分布；未登录、发布或采集账号资料。

## YouTube 观察

原生搜索卡片与 oEmbed 的标题 / 作者一致；仅核元数据，没有完整观看或评论统计。播放量是累计快照，相对年龄不反推精确发布日期。

| 视频 | 可核元数据 | 讨论与边界 |
| --- | --- | --- |
| [Ask the Experts: Evaluating Agent Skills · Nemotron Labs](https://www.youtube.com/watch?v=4rI0zATFxYI) | NVIDIA Developer；[SkillEvaluator 原生搜索](https://www.youtube.com/results?search_query=SkillEvaluator)为 6,918 views、Streamed 1mo ago、55:19；[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=4rI0zATFxYI&format=json)匹配，且项目 README 直接回链。 | 官方历史直播入口；未核全部内容，不能证明当前 0.9.0 或固定主线的评测 / CI 语义。 |
| [AG-UI 1.0 is here · Connect Any Agent to Any App](https://www.youtube.com/watch?v=46rhS_FayNE) | CopilotKit；[AG-UI 原生搜索](https://www.youtube.com/results?search_query=AG-UI)为 5,057 views、1mo ago、1:13；[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=46rhS_FayNE&format=json)标题 / 作者匹配。 | 同名维护方频道的历史发布视频；仅元数据核验，不替代 1.0 规范和具体适配器互操作测试。 |

两条 watch 直接 HTTP 均为 200，但静态文本只有站点壳；网页工具读取 AG-UI watch 限流，不能将 HTTP 成功当作已看视频。搜索还出现五年前同名 SkillEvaluator 内容和第三方旧教程，未计入当前项目热度。无可靠当日播放增量。

## 讨论与争议：事实、判断和待验证

以下为一方规范 / 文档与源码导出的工程问题，不包装成已统计的社媒争论。

| 议题 | 已核事实 | 判断 / 接续 |
| --- | --- | --- |
| 质量分与 Agent 增益 | SkillEvaluator 的无密钥 quality-check 不跑安全扫描器，发布证据可仍是 INCOMPLETE；Tier 3 配对才测增益。 | 分开静态质量、激活、任务成功、失败覆盖与对照差，避免拿总分替代效果。 |
| CI 绿灯 | 主线三层 CI 仅 Tier 1 阻断，tier3-required 已弃用并忽略；Tier 2 / 3 保留 advisory 结果。 | CI 通过不能声称全部层已完成或有效；需阅读原生报告和实际团队合并策略。 |
| 无 API 与本地 | 交易技能的无行情 key 路径仍需 CSV / 截图；SkillEvaluator embeddings、chat、judge 与 Agent 可走不同服务。 | 输入来源、模型出口、凭据和日志分别核，不靠一个“本地”标签推断隐私。 |
| 交易纪律与账户边界 | YAML 给出人工关卡，仓位脚本向下取整并写报告；维护者自动化另有提交 / 推送和会话派生数据出口。 | 宿主权限、行情时效、真实成交与教育示例分开；没有收益或最大损失保证。 |
| 发行与开发快照 | 交易库 release 列表为空，兼容表仅 Unreleased；AG-UI 协议 1.0 与 core / LangGraph 包版本不同。 | 固定同一来源身份与组合，不把安装说明当发行收据、不混合包版本。 |
| 人工中断与授权 | AG-UI 1.0 要求 consumer 完整回答 / 放弃所有 interrupt；producer 可以无状态。state 是远端输入。 | UI 回答应绑定可信用户和动作，服务端另做授权、期限与幂等；规范符合性不是安全实测。 |
| 长期任务宣传 | 11-14 原帖介绍 OpenBot Routines，可核正文与 986 累计 Views。 | 尚待独立核排程、重试、取消及成本，不能外推为本轮已验证能力。 |

## 验证范围与接续

- 来源核对：九页官方 daily；三个唯一仓库 ID、主线 SHA、完整目录树与最近发行；24 个固定 SHA 文件已取得，核读相关段落（含三个 README、文档 / 清单 / 许可、交易仓位脚本与 CI 说明），未审计整仓；PyPI 与两个 npm latest 另核。
- 文档范围：三个七节页、同日四平台日报、首页三个既有分类 / 最新入口 / 实际总数与 TODO；原有 AGENTS.md 修改保留在本次提交之外。
- 文档检查通过：三个项目页 21 个固定章节、日报七节、三个分类入口、1,035 个实际目录与六文件中的 334 个本地链接；59 个范围内外链均对应取得的来源或明确访问证据，其中 24 个固定 SHA 文件。六文件 Markdown lint 零问题，diff 空白检查通过。受限入口单列，不充当原帖已读证据。
- 接续优先：SkillEvaluator 发布包与主线 / CI 语义、配对失败分母和独立评测；交易技能数据 / 账户 / 包身份与维护自动化；AG-UI 1.0 中断覆盖、状态校验、版本降级和真实适配器恢复；OpenBot Routines 仍只是原帖观察。
- 未执行：安装上游或技能、运行扫描 / 评测 / 上游测试、模型 / 行情 API、账户连接、交易、下载模型 / 发行二进制、启动应用、配置排程、部署、发布评论、完整观看或系统评论审阅。
