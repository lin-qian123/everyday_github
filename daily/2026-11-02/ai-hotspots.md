<!-- markdownlint-disable MD013 -->

# AI 热点日报｜2026-11-02

- 采样：2026-11-02，Asia/Shanghai，约 06:57 起；读取时快照，不是自然日结算。原帖 / 发行日期单列，历史内容不写成今日发布。
- 范围：GitHub 综合及 Python、TypeScript、JavaScript、Go、Rust、C++、Jupyter Notebook、Swift daily 榜；X、Instagram、YouTube 做有界跟踪，不合成跨平台排行榜。
- 证据等级：A 为官方榜单、仓库 API、固定 SHA 文件；B 为有上游回链的账号、原帖 / 平台元数据；C 为第三方观察或受限入口。作者宣传、源码静态核读与本轮实测分开。
- 获取状态：网页工具直开 Trending 受限，直接 HTTP 成功读取九个官方页面；已连接 GitHub 核七个仓库身份、默认分支 SHA、完整递归树、发行列表及参考文件。广泛搜索只提供榜单 / 聚合线索，定向项目社媒搜索为空，后续通过官网回链、X oEmbed 和 YouTube 原生列表 / oEmbed 补证。检索缺口不表示没有热点；不同读取时刻的累计 stars 可相差少量。

## 今日重点

- **大模型落到本地仍要算完整硬件账**：FreeToken 综合榜 +232，主路线是 Linux / NVIDIA，专家缓存、RAM 与带宽共同决定效果；LiteRT-LM 语言榜 +9，是另一种适配模型与多平台 SDK 路线。两者都不能从“本地”二字推出设备通吃或完整应用离线。[FreeToken](../../projects/FreeToken/README.md)、[LiteRT-LM](../../projects/LiteRT-LM/README.md)
- **视觉库的价值转向约定和数值证据**：Kornia 综合榜 +88，0.9.0 与路线图强调几何、坐标约定、数值与 conformance；半精度 CPU 测试不能代替 CUDA / MPS 验证。[Kornia](../../projects/kornia/README.md)
- **编码工具接口有助于操作精确，权限另核**：Serena Python 榜 +57，v2 提供 REPL 与不同语义后端；排除 API 或 read_only 配置并不约束 REPL 的进程能力。应用 GPL、SolidLSP MIT 需区分。[Serena](../../projects/serena/README.md)
- **纠正金融模型的输入定义**：Kronos 综合榜 +611；旧页将其误述为文本融合，本轮改为 K 线量化 token 与自回归预测，并补默认切分区间交叠的待核项。[Kronos](../../projects/Kronos/README.md)
- **语音与教学都按具体链路验收**：Moonshine C++ 榜 +27，STT / TTS、中文 CER / 英文 WER、历史非商用模型分开；AI Engineering Hub 综合榜 +573，教程“production-ready”不代表整库生产验收。[Moonshine](../../projects/moonshine/README.md)、[AI Engineering Hub](../../projects/ai-engineering-hub/README.md)

## GitHub 热点项目

日增为指定官方 daily 页的 stars today；累计按 stars / forks / open issues（含 PR）排列，来自 API。以下是按主题选择的项目，含语言榜低增量补充，不代表全站前七；stars 不是用户数、质量或安全证明。

| 项目与动作 | 可核热度与发行 | 分类 | 本轮工程观察 |
| --- | --- | --- | --- |
| [FreeToken](../../projects/FreeToken/README.md)，新增 | 综合 +232；累计 15,362 / 1,548 / 470。发行首项 [nightly](https://github.com/FlashML-org/FreeToken/releases/tag/nightly)，UTC 2026-09-09，预发行滚动标签；PyPI 0.2.1。 | 模型、训练与推理基础设施 | CPU–GPU 协同与专家 / KV 缓存；主路线驱动 / CUDA 约束、推理 / daemon 双控制面和客户端配置写入。 |
| [kornia](../../projects/kornia/README.md)，新增 | 综合 +88；累计 11,759 / 1,465 / 133。[v0.9.0](https://github.com/kornia/kornia/releases/tag/v0.9.0)，UTC 2026-10-23。 | 模型、训练与推理基础设施 | 几何核心、坐标约定、已知半精度失败与按设备验证。 |
| [ai-engineering-hub](../../projects/ai-engineering-hub/README.md)，新增 | 综合 +573；累计 40,181 / 6,480 / 133。发行列表为空。 | AI 学习与教育资源 | 抽查 Simple RAG 的 top-k=2 / 全局 Settings、README 模型名称漂移及独立云评估数据流。 |
| [serena](../../projects/serena/README.md)，新增 | Python +57；累计 30,990 / 2,119 / 139。[v2.1.0](https://github.com/oraios/serena/releases/tag/v2.1.0)，UTC 2026-10-19；主线 2.1.1.dev0。 | Coding Agents 与终端助手 | LSP / 付费 JetBrains、tool / REPL 接口、trusted project 与实际隔离、分组件许可。 |
| [moonshine](../../projects/moonshine/README.md)，新增 | C++ +27；累计 11,370 / 641 / 18。[v0.1.5](https://github.com/moonshine-ai/moonshine/releases/tag/v0.1.5)，UTC 2026-08-24。 | 语音、视频与多模态 | 流式与历史 non-streaming、STT / TTS 许可与首次下载分开；中文 CER 不能和英文 WER 混比。 |
| [LiteRT-LM](../../projects/LiteRT-LM/README.md)，新增 | C++ +9；累计 6,797 / 776 / 748。[v0.19.0](https://github.com/google-ai-edge/LiteRT-LM/releases/tag/v0.19.0)，UTC 2026-10-30。 | 模型、训练与推理基础设施 | C API 破坏性变更、多语言接口状态、模型 / 后端适配与 localhost 服务入口。 |
| [Kronos](../../projects/Kronos/README.md)，原位修订 | 综合 +611；累计 45,323 / 7,495 / 294。发行列表为空。 | 办公、商业与行业应用 | 修正为 K 线输入；tokenizer / 上下文匹配、默认切分区间与简化回测边界。 |

- **去重与收录**：以 `projects/` 实际目录及 owner/repo 映射双重去重，七个唯一仓库 ID；新增六个目录，原位刷新 Kronos，实际目录 `977 → 983`。复用五类，补齐原来首页缺失的 Kronos 解读入口。
- **已有头部信号**：综合榜 T3 Code +3,100、Claude-mem +1,527、HEX +1,329、Claude-Code-Game-Studios +970、OpenMausBot +919、Lightpanda +827、Handy +383、AiSOC +436。多数已有近期说明，本轮记录榜单信号而未逐个重审实现。
- **同名与迁移候选**：scenario-labs/skills（Python）、Leonxlnx/taste-skill（JavaScript）与 herdrdev/herdr（Rust）有现有同名目录，未仅凭 owner 变化覆盖旧页。LibreChat owner 沿革、其他广泛 ML 教材候选留待后续核身份与选题，不为了增加数量重复建档。
- **取舍**：普通 API 清单、占卜、窗口管理、游戏引擎或媒体下载工具没有因上榜被自动归为 AI 新项目；Moonshine、LiteRT-LM、Serena 来自语言榜，明确不是全站头部。
- 官方榜单：[综合](https://github.com/trending?since=daily)、[Python](https://github.com/trending/python?since=daily)、[TypeScript](https://github.com/trending/typescript?since=daily)、[JavaScript](https://github.com/trending/javascript?since=daily)、[Go](https://github.com/trending/go?since=daily)、[Rust](https://github.com/trending/rust?since=daily)、[C++](https://github.com/trending/c++?since=daily)、[Jupyter Notebook](https://github.com/trending/jupyter-notebook?since=daily)、[Swift](https://github.com/trending/swift?since=daily)。

## X 观察

[Kornia 官网](https://www.kornia.org/) 回链 [@kornia_foss](https://x.com/kornia_foss)，账号页面标题匹配。以下固定帖由官方 oEmbed 核作者、正文与完整日期；均为历史原帖，没有取得可可靠归属各字段的点赞 / 转发 / 评论 / 浏览快照，不记录互动量。

| 固定来源 | 可复核状态 | 讨论与限制 |
| --- | --- | --- |
| [0.9.0 的约定说明](https://x.com/kornia_foss/status/2113900399811871228) | B 级，Kornia 官方账号，**2026-10-24**；说明图像、通道、数组、坐标与角度约定。 | 与本轮几何数值审查直接相关，但不是 11 月 2 日新发布，也不证明已消除所有约定问题。 |
| [AI 开发分工讨论](https://x.com/kornia_foss/status/2112981761764560992) | B 级，Kornia 官方账号，**2026-10-21**；讨论从“AI 怎样帮助”转向辨认哪些工作由人完成。 | 这是作者观点与工作流叙事；未读取完整关联 PR / 评论，不能当作 AI 贡献比例、代码质量提升或社区共识的量化证据。 |

未把账号 follower、页面未标明语义的计数或历史帖推成当日热度，也不把 GitHub 增星归因于这两条帖子。

## Instagram 观察

| 来源 | 可复核状态 | 讨论与限制 |
| --- | --- | --- |
| [edgeai 主题](https://www.instagram.com/explore/tags/edgeai/) | C 级，HTTP 返回后落到 accounts/login。 | 未读到项目原帖、作者、日期或互动字段；不能据此判断 FreeToken / LiteRT-LM 的平台传播。 |
| [aiagents 主题](https://www.instagram.com/explore/tags/aiagents/) | C 级，落到 popular/aiagents 聚合。 | 页面主题 reels 总量不是任一入选项目互动量。未取得独立可读项目原帖，保留观察入口，不推断平台无热点或热度下降。 |

## YouTube 观察

原生搜索列表给出固定视频、作者、相对时间和累计播放，官方 oEmbed 交叉核标题 / 作者。以下都是**历史视频**，没有观看全片或分析评论；相对时间不换算精确发布日期，累计播放不当作今日增量。

| 固定视频 | 可核元数据与来源关系 | 讨论与限制 |
| --- | --- | --- |
| [How They Fixed AI's Biggest Local Hardware Problem (with FreeToken)](https://www.youtube.com/watch?v=8n4Uo47CadY) | Better Stack / @betterstack；列表累计 **331,831 views**、**2mo ago**；oEmbed 一致。B 级元数据，**第三方视频**。 | 可以观察到持续累积的历史内容入口；标题不能替代模型 / RAM / GPU / 量化 / 上下文条件下的性能复现。 |
| [Introduction to Serena – The IDE for Your Coding Agent](https://www.youtube.com/watch?v=5QN7gN1KYLA) | Oraios AI / @OraiosAI；列表累计 **38,171 views**、**6mo ago**；oEmbed 一致。固定 README 直接回链。 | 早于当前 v2 发行；介绍中的接口、许可与能力需对照本轮固定源码，不以旧演示代替当前验收。 |
| [Getting started with Moonshine Voice](https://www.youtube.com/watch?v=WH-AGvHmtoM) | Pete Warden / @PeteWarden；列表累计 **1,107 views**、**8mo ago**；oEmbed 一致。固定 quickstart 回链。 | 可作为教程入口，旧 API 与模型许可要重新核对；没有把视频当作中文识别准确率或实时延迟证据。 |

## 讨论与争议

以下是从一手资料提炼的工程讨论点，**不是评论统计得到的争议强度或社群共识**。

- **“能加载”与“值得运行”分别测**：FreeToken 依靠分层内存与带宽，LiteRT-LM 依赖模型适配与后端。参数量、VRAM、首 token、decode、任务成功率和耗电应分别报告。[FreeToken](../../projects/FreeToken/README.md)、[LiteRT-LM](../../projects/LiteRT-LM/README.md)
- **配置约束何时变成权限约束**：Serena 明确 REPL read_only 不是进程隔离，trusted-project 也不是 containment；本地服务监听、CORS 与认证同样是不同控制点。[Serena](../../projects/serena/README.md)、[FreeToken](../../projects/FreeToken/README.md)
- **精度证据不能跨任务迁移**：Kornia CPU 半精度结果不覆盖 GPU；Moonshine 中文 CER、英文 WER、float / quantized 与不同数据集分开。[Kornia](../../projects/kornia/README.md)、[Moonshine](../../projects/moonshine/README.md)
- **许可随组件和版本核对**：Serena 当前应用 GPL / SolidLSP MIT、历史 MIT；Moonshine 默认 STT MIT / 指定旧非英语模型非商用 / TTS 独立条款；代码开放不统一授权模型与数据。[Serena](../../projects/serena/README.md)、[Moonshine](../../projects/moonshine/README.md)
- **研究示例不等于生产或盈利证据**：Kronos 默认时间区间交叠需要追到样本构造后才可判断泄漏；AI Engineering Hub 的教程标签不能替代独立评估、权限和恢复验证。[Kronos](../../projects/Kronos/README.md)、[AI Engineering Hub](../../projects/ai-engineering-hub/README.md)

## 已核实、未验证与接续

- **已核实**：九个官方榜单、七个唯一仓库身份 / SHA / 完整树 / 发行列表与固定参考文件；六新页去重、Kronos 原位纠错与五类索引；PyPI Kornia 0.9.0、FreeToken 0.2.1、Serena 2.1.0、Moonshine Voice 0.1.5、LiteRT-LM 0.19.0 的版本 / Python 字段；两个 X 原帖日期与正文、Instagram 两个受限落点、三条 YouTube 的作者 / 标题及原生列表累计播放 / 相对时间。
- **未验证**：上游安装、构建或示例执行；模型 / 权重下载和调用；CPU / GPU / NPU 性能、数值与梯度；录音、语音准确率、设备能耗；MCP 接入、真实写文件 / shell 权限实验；Kronos 数据重建 / 训练 / 回测与泄漏定性；视频全片、评论、社媒当日互动增量与传播因果。
- **接续**：FreeToken wheel / 模型 / RAM / 带宽基准和双控制面；Kornia 实际算子 / dtype / device 与坐标一致性；Serena 两后端 / tool-REPL 接口及许可；Moonshine 模型身份 / CER-WER / 离线与资产条款；LiteRT-LM C API / SDK / 后端 / 模型匹配；教程单目录锁依赖 / 数据出口与检索验证；Kronos 切分 / 窗口 / 复权 / purge 与纯时间外对照。

## 主要来源

- [FlashML-org/FreeToken](https://github.com/FlashML-org/FreeToken)、[API](https://api.github.com/repos/FlashML-org/FreeToken)、[固定文件与解读](../../projects/FreeToken/README.md)。
- [kornia/kornia](https://github.com/kornia/kornia)、[API](https://api.github.com/repos/kornia/kornia)、[固定文件与解读](../../projects/kornia/README.md)。
- [patchy631/ai-engineering-hub](https://github.com/patchy631/ai-engineering-hub)、[API](https://api.github.com/repos/patchy631/ai-engineering-hub)、[固定文件与解读](../../projects/ai-engineering-hub/README.md)。
- [oraios/serena](https://github.com/oraios/serena)、[API](https://api.github.com/repos/oraios/serena)、[固定文件与解读](../../projects/serena/README.md)。
- [moonshine-ai/moonshine](https://github.com/moonshine-ai/moonshine)、[API](https://api.github.com/repos/moonshine-ai/moonshine)、[固定文件与解读](../../projects/moonshine/README.md)。
- [google-ai-edge/LiteRT-LM](https://github.com/google-ai-edge/LiteRT-LM)、[API](https://api.github.com/repos/google-ai-edge/LiteRT-LM)、[固定文件与解读](../../projects/LiteRT-LM/README.md)。
- [shiyu-coder/Kronos](https://github.com/shiyu-coder/Kronos)、[API](https://api.github.com/repos/shiyu-coder/Kronos)、[固定文件与解读](../../projects/Kronos/README.md)。
