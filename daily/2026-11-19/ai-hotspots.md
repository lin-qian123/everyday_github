<!-- markdownlint-disable MD013 -->

# AI 热点日报｜2026-11-19

- 采样：2026-11-19（Asia/Shanghai）07 时段；事件日期另列。daily 增星、API 累计数和视频播放量均为本轮快照，不是自然日结算。
- 范围：GitHub 综合、Python、TypeScript、JavaScript、Rust、Go、C++、Jupyter Notebook、Shell、Swift 十个官方 daily 页的有界抽样；重点补三项档案，不合成跨平台排行榜，也不声称覆盖所有新上榜仓库。
- 证据：A 为官方榜单 / API / 固定 SHA 文件，B 为平台原生列表 / 元数据，C 为搜索、聚合或受限入口。上游声明、静态核读、本文判断与运行验收分开。
- 获取：广泛搜索主要给出聚合及二手材料，四条候选 / 社媒定向搜索为空；网页工具读取 Trending 受限，改用官方 HTTP、GitHub 连接器和平台原生 HTTP / oEmbed。搜索为空不等于没有讨论。
- 接续：沿用 11-18 的项目档案与首页分类。新增前查 `projects/`、上游链接和唯一仓库 ID；Sellbird 旧名 Harvey 的 API 迁移到同一 ID，本库没有旧档案，不重复建档。

## 今日重点

- **发布检查必须把未知结果留下来。** App Store Compliance Shell +596；静态 guard 在部分 `NOT CHECKED` hook 路径仍放行，Fleet Sweep 则把覆盖不全单列。许可为 ORA-2.3，不能按 MIT 技能包复用。[项目解读](../../projects/app-store-compliance/README.md)
- **销售 Agent 的价值在可核流程，外发仍要逐封负责。** Sellbird Python +358；默认审批和确定性发送关卡值得观察，但主机保存数据、模型调用、邮箱验证与实际发送是不同权限和数据流。[项目解读](../../projects/sellbird/README.md)
- **成熟推理工具也要看补丁、设备与性能分母。** OpenVINO 综合 / C++ +18；2026.4.1 是 10 月既有发行，本轮新建档。LLM 首 token 后速率不等于端到端延迟。[项目解读](../../projects/openvino/README.md)

## GitHub 热点项目

API 顺序为 stars / forks / open issues（含 PR），不是本日新增 issue 数。首次建档不代表项目今天首发；同一仓库出现在多个语言榜不累加。

| 项目与动作 | 可核热度 / 版本 | 沿用分类 | 工程关注 |
| --- | --- | --- | --- |
| [app-store-compliance](../../projects/app-store-compliance/README.md)，新增 | Shell +596；1,364 / 105 / 27；[API](https://api.github.com/repos/mjmirza/app-store-compliance)；[v2.4.0](https://github.com/mjmirza/app-store-compliance/releases/tag/v2.4.0)，UTC 11-15，非预发行。 | Agent 框架与技能生态 | 未检查放行、人工证据、宿主安装、规则数量漂移与 ORA 许可。 |
| [sellbird](../../projects/sellbird/README.md)，新增 | Python +358；6,486 / 1,337 / 60；[API](https://api.github.com/repos/ethanplusai/sellbird)；[v0.4.0](https://github.com/ethanplusai/sellbird/releases/tag/v0.4.0)，UTC 11-06，非预发行。 | 办公、商业与行业应用 | 默认审批 / autopilot、CLI 契约、数据出口、邮箱授权及 AGPL。 |
| [openvino](../../projects/openvino/README.md)，新增 | 综合 / C++ +18；11,308 / 3,601 / 1,159；[API](https://api.github.com/repos/openvinotoolkit/openvino)；[2026.4.1](https://github.com/openvinotoolkit/openvino/releases/tag/2026.4.1)，UTC 10-01，非预发行。 | 模型、训练与推理基础设施 | 设备 / 驱动、动态 shape 数值回归、遥测和 LLM 性能口径。 |

- 唯一仓库 ID 依次为 `1261204838 / 1179388779 / 153097643`；实际项目目录 **1,044 → 1,047**，复用三个既有分类。
- 已建档项目的本轮综合 daily 观察：Claude-BugHunter +2,322、PaperOrchestra +1,529、ECC +1,109、last30days-skill +1,062、Superpowers +823、CLI-Anything +384、Stitch Skills +369、SkillEvaluator +323。这里只记录热度，不表示重审了实现或新发行。
- **保留身份缺口：** JavaScript 榜的 `Leonxlnx/taste-skill` +822，API ID `1162099055`；旧 `projects/taste-skill` 声明的 `KOHbDS/taste-skill` 本轮 API 404。尚无同一 ID 或迁移证据，不能据目录同名覆盖旧档案，也不能把旧页的泛化文风分析归到当前前端技能。[当前候选](https://github.com/Leonxlnx/taste-skill)、[旧地址核查](https://api.github.com/repos/KOHbDS/taste-skill)
- [综合 daily](https://github.com/trending?since=daily)、[Python](https://github.com/trending/python?since=daily)、[TypeScript](https://github.com/trending/typescript?since=daily)、[JavaScript](https://github.com/trending/javascript?since=daily)、[Rust](https://github.com/trending/rust?since=daily)、[Go](https://github.com/trending/go?since=daily)、[C++](https://github.com/trending/c++?since=daily)、[Jupyter Notebook](https://github.com/trending/jupyter-notebook?since=daily)、[Shell](https://github.com/trending/shell?since=daily)、[Swift](https://github.com/trending/swift?since=daily)本轮均 HTTP 200；动态榜单未来会变化。通用包管理、前端框架或系统工具不只因上榜便归为 AI 核心。

## X：账号可读，原帖缺口保留

| 入口与关联 | 可读事实 / 热度 | 证据边界 |
| --- | --- | --- |
| [@sellbirdagent](https://x.com/sellbirdagent)，由上游 README / 发行说明回链。 | 直接 HTTP 200，账号标题与 sellbird.ai 回链可读；网页工具 403。未取到可验证的原帖互动快照。 | C 级观察入口。页面同时有帖子计数与未发帖占位提示，不据此判断是否有帖，不从账号概况推导项目传播。 |
| [@MirzaJhanzaib](https://x.com/MirzaJhanzaib)，由 app-store-compliance README 回链。 | 直接 HTTP 200，可读账号简介；帖子区登录提示，网页工具 403。 | 本轮无可统计的项目帖、Views、转发或评论样本。个人简介是自述，不等于机构背书。 |

本轮没有将 GitHub 增星换算成 X 热度，也没有复用历史热门帖充当今日项目讨论。

## Instagram：聚合量与项目原帖分开

- [aiagents 标签入口](https://www.instagram.com/explore/tags/aiagents/)本轮 HTTP 200，跳到 popular 聚合页，标题显示 **129K reels**；网页工具限流。该数仅是宽泛主题聚合快照，不是当日新增、独立作者数或三个项目的传播量。
- [sellbird 标签入口](https://www.instagram.com/explore/tags/sellbird/)本轮 HTTP 200 后转登录，未取得项目原帖、账号归属和互动量；不把同名标签视为官方活动。
- 均作为 C 级观察；没有可据以总结评论争议的帖子样本。今日读到的聚合数字与昨日读取缺口分开记录，不能据两次访问状态推断增长。

## YouTube：历史演示与累计元数据

| 原生入口 / 条目 | 本轮可核事实 | 解释与限制 |
| --- | --- | --- |
| [Sellbird / Harvey 检索](https://www.youtube.com/results?search_query=sellbird+harvey+AI)中的 [Sellbird GitHub Overview: Local vs Hosted AI Sales Agent Architecture](https://www.youtube.com/watch?v=aUZrA1O_GFs)，频道 Alex Hitt。 | 原生列表 **404 次累计播放、9d ago、9:09**；[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=aUZrA1O_GFs&format=json)标题 / 作者一致。 | B 级第三方历史解读。未读完整内容与代码链接，不把其架构标题当作隔离测试或转化效果证据；同检索混入法律 AI Harvey，未计入本项目。 |
| [OpenVINO 检索](https://www.youtube.com/results?search_query=OpenVINO+2026)中的 [OpenVino Model Server Demo](https://www.youtube.com/watch?v=He1TOoslxdg)，频道 Intel Devs。 | 原生列表 **11,897 次累计播放、5mo ago、5:07**；[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=He1TOoslxdg&format=json)完整标题 / 作者一致。 | B 级历史元数据；主题是 Model Server，与本轮 runtime 主仓及 2026.4.1 的版本对应未核，不用于证明今日上榜原因或性能。 |
| [app-store-compliance 定向检索](https://www.youtube.com/results?search_query=app-store-compliance+mjmirza) | 返回若干通用商店提交 / 拒审教程。 | 未核到可明确对应本仓库的视频条目；检索缺口不表示不存在相关视频。 |

两条 watch 本轮 HTTP 200，页面覆盖层标题可读；没有据此宣称已观看、运行演示、核实全部描述或采集评论。相对发布时间是列表原文，播放量为累计值，不是当日增量。

## 讨论与争议：可证伪的工程问题

以下是依据上游材料提出的判断，不包装成已统计的社媒争论；固定 SHA 来源见项目页。

| 议题 | 已核事实 | 判断 / 下一步 |
| --- | --- | --- |
| hook 放行能否视为发布通过 | App Store guard 的部分未知路径返回 0，且允许显式覆盖 critical；Fleet Sweep 另核覆盖与未知结果。 | CI 应核结论、Coverage 与真实提交通道；手册不能替代商店审核及当期法规确认。 |
| 条目数能否代表自动化覆盖 | API 描述 117 / 95；固定 JSON 实际 123 个模式、107 个期限。 | 数据版本、规则新鲜度与可自动检测数量分开统计，不用一个数字宣称全覆盖。 |
| 没有模型 API 账单是否代表零成本 | Sellbird 使用订阅 CLI，仍有配额、邮箱和可选付费来源。 | 记录真实配额 / 费用、事实错误、退信与人审时间，不能先下销售收益结论。 |
| 无工具模型是否足以控制外发 | Sellbird 模型主要产文本，但程序本身能用邮箱，审批可转 autopilot。 | 分别验证模型契约、发送状态、暂停 / 退订和异常对账；本机部署不代表无云数据流。 |
| 性能数字是否可跨任务比较 | OpenVINO 官方页的 GenAI tok/s 计算首 token 后速率；发行补丁涉及数值与驱动问题。 | 同权重、精度、输入输出与设备条件测 TTFT、全程耗时和任务质量。 |
| 公开仓库是否可任意复用 | 三项目当前许可分别为 ORA-2.3、AGPL-3.0-only、Apache-2.0。 | 按版本、组件、使用与再分发方式核权利；不从 GitHub 可访问推导宽松许可。 |

## 验证范围与接续

- 本轮读取十个官方 daily 页、三个新项目的元数据 / 固定分支 SHA / 发行列表，以及相关 README、许可、文档和代码。两个较小仓库目录树完整；OpenVINO 递归树读取未成功，改用根树与固定路径抽样，不称全仓审计。
- 交付范围：三份七节项目说明、本日报、首页三个分类 / 最新日期 / 实际项目总数和 TODO。已有 `AGENTS.md` 修改保持原样并排除提交。
- 检查通过：三项目 21 个固定章节、日报七节、三个分类入口、1,047 个实际目录及六文件 352 个本地链接；65 个本轮来源 URL 均有已读内容或明确访问证据，其中 25 个为固定 SHA 文件。六文件 Markdown lint 零问题、空白检查通过；旧身份 API 404 和社媒受限入口按缺口保留。发布前另核精确六文件暂存范围，推送后核远端 master；资料检查不等于运行测试。
- 接续：App Store 未检查 / 豁免与宿主真实 hook；Sellbird 审批 / CLI 兼容 / 发送异常；OpenVINO 固定模型的数值、驱动与性能；taste-skill 旧址身份；社媒原帖及评论补证。vllm-ascend、Dodaios、splash 等其他候选留待后续按来源筛选。
- 未执行：上游安装或测试、用户项目扫描、商店提交、联系人采集、邮箱 / 模型 / 云调用、登录材料读取、发送 / 回复邮件、修改宿主配置、迁移数据库、部署、权重 / 二进制 / 媒体下载、设备性能 / 隔离实验、完整观看或评论统计。
