<!-- markdownlint-disable MD013 -->

# AI 热点日报｜2026-11-16

- 采样：2026-11-16（Asia/Shanghai）07 时段。daily 增星、API 累计量、Views 和视频计数是抓取快照，不是自然日结算；事件日期另列。
- 范围：官方综合、Python、TypeScript、JavaScript、Rust、Go、C++、Jupyter Notebook、Swift 九个 daily 页；有界抽样，不合成跨平台排名。
- 证据：A 为官方榜单 / API / 固定 SHA 文档和代码；B 为平台原帖及原生元数据；C 为聚合或受限入口。上游自述、静态核读、日报判断与运行验收分开。
- 获取：广泛搜索多为二手汇总，四条项目定向 X / Instagram / YouTube 搜索为空；网页工具对 Trending 受限、X 403、YouTube / Instagram 限流。改用直接官方 HTTP、GitHub 连接器及原生列表 / oEmbed；空搜索不等于没有讨论。
- 接续：最近日报为 11-15。按目录、owner/repo 和仓库 ID 去重，三个项目首次建档，Univer 原位刷新；不重建昨天三页，不把当前快照回填到过去。

## 今日重点

- **GGML 1.0 的看点是执行与迁移。** 综合 / C++ +53；11-13 稳定发行删旧 API、更新 RPC 协议，并记录多后端改动。发行性能描述需目标机器复测。[解读](../../projects/ggml/README.md)
- **AI Infra 学习开始重视可复算与缺项。** Python +151；十二章初稿附静态计算与实跑记录，逻辑载荷、资源下界和实测要分开。最新构建仍为 10-01。[解读](../../projects/ai-infra-book/README.md)
- **聊天组件带来的不只是界面。** assistant-ui TypeScript +92；需要一起核在线安装引导、工具执行位置和 Cloud 会话边界。[解读](../../projects/assistant-ui/README.md)
- **Univer 的老版本说明需要升级。** 综合 / TypeScript +1,041；原页从 09-23 的 0.25.2 / 1.0 RC 观察更新到稳定 1.5.0，补 Worker 迁移、导出水印、原生组件与保存草稿边界。[解读](../../projects/univer/README.md)

## GitHub 热点项目

日增取本轮官方 daily；API 为 stars / forks / open issues（含 PR），不是本轮新增问题数。“新增”仅指本仓库首次建档。

| 项目与动作 | 可核热度与版本 | 沿用分类 | 工程关注 |
| --- | --- | --- | --- |
| [ggml](../../projects/ggml/README.md)，新增 | 综合 / C++ +53；15,891 / 2,018 / 386；[API](https://api.github.com/repos/ggml-org/ggml)；[v1.0.0](https://github.com/ggml-org/ggml/releases/tag/v1.0.0)，UTC 11-13。 | 模型、训练与推理基础设施 | 库 / GGUF / 应用区别；构图、缓冲与后端；API / RPC 组合迁移。 |
| [ai-infra-book](../../projects/ai-infra-book/README.md)，新增 | Python +151；7,819 / 629 / 9；[API](https://api.github.com/repos/bojieli/ai-infra-book)；[build-20261001-161920](https://github.com/bojieli/ai-infra-book/releases/tag/build-20261001-161920)，UTC 10-01。 | AI 学习与教育资源 | 原创 / 第三方许可，静态 / 实跑口径、历史实验状态与 LFS 指针。 |
| [assistant-ui](../../projects/assistant-ui/README.md)，新增 | TypeScript +92；13,236 / 1,342 / 81；[API](https://api.github.com/repos/assistant-ui/assistant-ui)；[React npm 0.15.36](https://registry.npmjs.org/@assistant-ui%2Freact/latest)；[setup-agent@0.2.0](https://github.com/assistant-ui/assistant-ui/releases/tag/setup-agent%400.2.0)，UTC 11-13，为独立辅助包。 | 前端、UI 与 Agent 交互层 | 在线 guide / 项目写入、toolkit 客户端与服务端、人工结果、Cloud workspace / retention。 |
| [univer](../../projects/univer/README.md)，刷新 | 综合 / TypeScript +1,041；25,567 / 2,333 / 175；[API](https://api.github.com/repos/dream-num/univer)；[v1.5.0](https://github.com/dream-num/univer/releases/tag/v1.5.0)，UTC 11-14；[core npm](https://registry.npmjs.org/@univerjs%2Fcore/latest) 同为 1.5.0。 | 办公、商业与行业应用 | 开源 / 商业层、Worker 导出迁移、chart 数据读写、原生绑定及免费额度水印。 |

- 三个新上游身份未命中既有项目；Univer 保留同 ID 原目录。实际目录 **1,035 → 1,038**，首页同步四个既有分类，不扩分类。
- 已建档观察：Modern Web Guidance +1,220、Plannotator +860、Chrome DevTools MCP +718、Claude Trading Skills +707、Open Code Review +688、LoopForge +484、AG-UI +393、SkillEvaluator +205。只记录本轮榜单；没有把它们再建成新项目或宣称已复审实现。
- 其他候选：Claude-BugHunter 综合 / Python +221、COG-second-brain Python +37、WrenAI Python +52 等保留后续核读。普通网络、动画、模拟器与系统工具不因上榜就归作 AI 核心；本轮并非全榜穷尽。
- 官方页：[综合](https://github.com/trending?since=daily)、[Python](https://github.com/trending/python?since=daily)、[TypeScript](https://github.com/trending/typescript?since=daily)、[JavaScript](https://github.com/trending/javascript?since=daily)、[Rust](https://github.com/trending/rust?since=daily)、[Go](https://github.com/trending/go?since=daily)、[C++](https://github.com/trending/c++?since=daily)、[Jupyter Notebook](https://github.com/trending/jupyter-notebook?since=daily)、[Swift](https://github.com/trending/swift?since=daily)。

## X 观察

Univer 固定 README 回链 [univerHQ](https://x.com/univerHQ)，直接 HTTP 可读账号与部分原帖；网页工具读账号为 403。账号自述的 30k+ GitHub stars 没有明确单仓口径，本日报采用上表 API，不把账号宣传数字当 Univer 单仓当前量。

- [11-09 宣布 Univer 1.4 与 Space 的原帖](https://x.com/univerHQ/status/2119777905815519641)与 [oEmbed](https://publish.twitter.com/oembed?url=https://x.com/univerHQ/status/2119777905815519641)的作者、日期和正文一致。直接原帖明确标出 **204K Views**；其余裸数字不猜测为赞 / 转发 / 评论。
- 已核内容：介绍用 Univer SDK 构建文件管理、表格、文档、演示文稿与 Agent 工作区。这是 **2026-11-09 历史累计背景**，不是今天新增 204K，也不是 1.5.0 的发布时间或功能清单。
- 讨论线索：编辑草稿如何提交、谁能合并、最终 Office 文件如何回读，是本日报结合当前发行提出的工程问题；未系统读取评论，不能称为平台共识或用户投诉分布。
- [assistant-ui 实时搜索](https://x.com/search?q=%22assistant-ui%22&f=live)直接 HTTP 200 后落到登录引导。书稿定向搜索为空；两者未取得可独立核验的当日原帖与互动增量，不作传播判断。

## Instagram 观察

- [aiagents 标签](https://www.instagram.com/explore/tags/aiagents/)直接 HTTP 200，转 popular 聚合，标题为 **129K reels**。它是宽泛话题累计量，不能归因于本轮项目或推出本日增长。
- [assistantui 标签候选](https://www.instagram.com/explore/tags/assistantui/)转登录并返回 429；同名标签不建立项目身份。定向搜索也未取得可核项目帖子。
- 本轮没有项目级原帖、日期、互动或评论样本；只保留受限观察入口，不制作 Instagram 项目热榜。未登录或发布。

## YouTube 观察

仅核元数据；没有完整观看或评论审阅。相对年龄不反推精确日期，累计计数不写成今日播放增量。

| 视频 | 可核信息 | 讨论与边界 |
| --- | --- | --- |
| [We Built a Git-Style Spreadsheet Runtime for AI Agents · Univer CLI](https://www.youtube.com/watch?v=p75pV2qNQj4) | 上游 README 回链的 [Univer 频道列表](https://www.youtube.com/@dreamNum/videos)列 **370**、**5mo ago**、3:32；[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=p75pV2qNQj4&format=json)标题与作者 Univer 匹配。列表计数只作累计快照。 | 历史官方演示；不能证明当前 1.5.0 的布局、服务、许可或迁移正确，也不能把 Git-style 当进程隔离。 |
| [assistant-ui · Short Demo](https://www.youtube.com/watch?v=ZW56UHlqTCQ) | 固定 README 直接回链；[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=ZW56UHlqTCQ&format=json)确认标题和作者 Simon Farshid。未取得该条可靠日期 / 播放量，不补数字。 | 项目引用的演示入口，不能作为当前组件、在线 setup 或 Cloud 保留策略的行为证明。 |

两条 watch 直接 HTTP 200 但静态提取仅站点壳；网页工具对短演示限流。[assistant-ui 原生搜索](https://www.youtube.com/results?search_query=assistant-ui)另有第三方旧教程和无关同名内容，未纳入项目热度；HTTP 成功不等于已看视频。

## 讨论与争议：事实、判断和待验证

以下是官方材料导出的工程议题，不包装成已统计的社媒争论。

| 议题 | 已核事实 | 判断 / 待验证 |
| --- | --- | --- |
| 资源估算与真实性能 | 书稿计算文档分开逻辑载荷、硬件峰值和实跑；共享设备和历史编号限制有记录。 | 固定模型 / 输入 / 精度与机器，独立核 trace；不把 Roofline 下界写成实测延迟。 |
| GGML 1.0 的稳定性 | 稳定 Release 明列旧 API 删除和 RPC v9，后端优化来自维护方发行记录。 | 同步上层构图及 peers，数值、吞吐和内存分别测；版本号不是无迁移保证。 |
| 安装版本与远端文本 | assistant-ui setup guide 从服务器获取，256 KiB / 无重定向 / 有限步骤检查存在。 | 固定 CLI 也不冻结远端文案；检查编码 Agent 最终安装和改动，不把格式约束称作权限沙箱。 |
| 人工界面与执行授权 | toolkit 区分浏览器、后端、人类结果和只渲染工具。 | UI 批准须与真实身份、目标和操作绑定，服务端另做授权和幂等。 |
| 删除对话与删除所有记录 | Cloud retention 保留 runs、scores、汇总等，缩短窗口另有 24h 等待和分批处理。 | 按记录类型确认数据生命周期，不能声称立即全删。 |
| Office 开源与免费 | Univer 核心开源，商业模块另发；1.5.0 原生导出有月度无水印额度与后续水印路径。 | 分别核包、native adapters、服务和商业条件；免费功能不自动成为 Apache-2.0。 |
| semver 与实际迁移 | Univer 稳定政策承诺同 major 的 stable API 兼容，1.5.0 同时列 Worker / 导出迁移。 | 判定接口是否 stable / internal，再以实际锁文件和回归验证，不仅看 minor 标签。 |

## 验证范围与接续

- 来源：九页 official daily、四个唯一仓库 ID、固定主线 SHA 与最近发行；GGML / assistant-ui / Univer 完整目录树。书稿递归树 Transport closed，改查根树及固定 README / 计算 / 实验 / LFS / 许可文件，明确为抽样，未审计整书或整仓。两个 npm latest 与来源清单另核。
- 文档：三个新增七节页、Univer 原页、同日四平台日报、首页四类 / 最新入口 / 实际总数与 TODO；AGENTS.md 原修改不纳入提交。
- 检查通过：四项目共 28 个固定章节、日报七节、四个分类入口、1,038 个实际目录、七文件 341 个本地链接；63 个本轮来源链接均匹配已取得的来源或明确访问证据，其中 25 个固定 SHA 文件。七文件 Markdown lint 零问题，diff 空白检查通过；受限入口不充当原帖已读证据。发布前另核暂存范围与远端 master。
- 接续：GGML 1.0 上层迁移与后端数值 / 性能；书稿选定算例手算与独立实测、历史状态映射；assistant-ui toolkit / setup / Cloud workspace / 删除边界；Univer Worker、chart schema、native bindings、保存草稿和 Office 回读。
- 未执行：安装运行上游、编码 Agent 安装引导、编译 / 测试、模型或 Cloud API、下载权重 / LFS / 媒体 / 原生发行包、登录、迁移用户文档、部署、评论发布、完整视频观看或系统评论统计。本轮验证是文档和来源核验。
