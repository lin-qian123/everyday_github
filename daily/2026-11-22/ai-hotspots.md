<!-- markdownlint-disable MD013 -->

# AI 热点日报｜2026-11-22

- 采样：2026-11-22（Asia/Shanghai）07 时段；发行 / 视频日期单列。GitHub `stars today`、API 累计值和视频播放量均为本轮快照，不是自然日结算，也不合成跨平台排名。
- 范围：综合、Python、TypeScript、JavaScript、Go、Rust、C++、Swift、Jupyter Notebook、Shell 十个官方 daily 页的有界抽样。本轮补充三个未独立建档项目，不声称覆盖全部新上榜项目。
- 证据：A 为官方榜单、仓库 API、固定 SHA 文件；B 为平台原帖 / 元数据；C 为搜索、聚合或受限入口。上游声明、本文工程判断和运行验收分开。
- 获取：`search-layer` 日内广搜无结果；Web 搜索取得发布聚合、旧闻和视频线索，但未形成足够项目原帖样本。项目依据官方 Trending HTTP 与 GitHub 连接器；社媒另读原生页面和 oEmbed。检索缺口不代表没有热点。
- 接续：依据 `projects/` 目录、上游 owner/repo、旧 owner 和仓库 ID 去重；Python AgentScope 与已收录 Java 仓库不同。保留此前项目页和已有 `AGENTS.md` 修改，仅同步两个受影响分类与状态。

## 今日重点

- **训练复现要拆开精度、耗时与恢复。** TorchTitan Python +8；batch-invariant 模式有限定精度 / 并行条件，上游样本的计算变慢被检索与调度开销掩盖；最终权重导出也不等于可恢复训练的 checkpoint。[项目解读](../../projects/torchtitan/README.md)
- **协作控制面需要核实际执行权限。** CLI Agent Orchestrator Python +14；复用多个已有 CLI，但 provider 白名单强度不同，Codex 默认 worker 带 `--yolo`，tmux 不提供系统隔离。[项目解读](../../projects/cli-agent-orchestrator/README.md)
- **框架抽象与执行后端分别验收。** AgentScope Python +64；SDK、服务、权限与 workspace 分层，LocalWorkspace 仍使用本机 backend，reply token 预算也不是服务商账单硬上限。[项目解读](../../projects/agentscope/README.md)

## GitHub 热点项目

API 数值依次为 stars / forks / open issues（含 PR）；跨语言上榜不累加。

| 项目与动作 | 本轮热度 / 发行 | 沿用分类 | 工程关注 |
| --- | --- | --- | --- |
| [torchtitan](../../projects/torchtitan/README.md)，新增 | Python +8；5,938 / 1,095 / 509；[API](https://api.github.com/repos/pytorch/torchtitan)；最新非预发行 [v0.4.0](https://github.com/pytorch/torchtitan/releases/tag/v0.4.0)，UTC 10-28。 | 模型、训练与推理基础设施 | Python recipe、并行布局、数值路径、checkpoint 与指标分母。 |
| [cli-agent-orchestrator](../../projects/cli-agent-orchestrator/README.md)，新增 | Python +14；1,618 / 342 / 179；[API](https://api.github.com/repos/awslabs/cli-agent-orchestrator)；最新非预发行 [v2.5.3](https://github.com/awslabs/cli-agent-orchestrator/releases/tag/v2.5.3)，UTC 10-08；main 包写 2.5.4，不能视为已发新版。 | Agent 框架与技能生态 | provider 原生 / 软限制、委派上限、Codex sandbox、控制面认证。 |
| [agentscope](../../projects/agentscope/README.md)，新增 Python 页 | Python +64；36,438 / 3,899 / 843；[API](https://api.github.com/repos/agentscope-ai/agentscope)；最新非预发行 [v2.0.12](https://github.com/agentscope-ai/agentscope/releases/tag/v2.0.12)，UTC 11-16；在线 latest 权限文档转 2.0.13dev。 | Agent 框架与技能生态 | 权限模式、本机 / sandbox 后端、预算、模型数据出口与服务隔离。 |

- 三个唯一仓库 ID 为 `730932260 / 1028432181 / 742244656`；实际目录 **1,053 → 1,056**。建档日期不是项目首发日期，语言榜抽样也不是综合榜前三。
- 头部已建档项目继续观察：综合 daily 的 Claude-BugHunter +1,794、Firecrawl +999、Superpowers +884、CLI-Anything +767、App Store Compliance +724、diagram-design +582、last30days-skill +566、MiniMind +488；语言页还见 FreeVideo Python +410、OpenVINO C++ +202。这里只重新读取热度，没有重新审计这些项目。
- 未因通用 Web 框架、普通下载器或系统工具上榜就纳入 AI 重点。原有同名 `skills` 的 owner-aware key 与 taste-skill 身份待办保留；本轮没有用新 owner 覆盖无法证明同身份的旧页。
- 来源：[综合 daily](https://github.com/trending/?since=daily)、[Python](https://github.com/trending/python?since=daily)、[TypeScript](https://github.com/trending/typescript?since=daily)、[JavaScript](https://github.com/trending/javascript?since=daily)、[Go](https://github.com/trending/go?since=daily)、[Rust](https://github.com/trending/rust?since=daily)、[C++](https://github.com/trending/c++?since=daily)、[Swift](https://github.com/trending/swift?since=daily)、[Jupyter Notebook](https://github.com/trending/jupyter-notebook?since=daily)、[Shell](https://github.com/trending/shell?since=daily)，本轮均 HTTP 200，榜单随时间变化。

## X：搜索受限，文档外链也需核身份

| 来源 | 本轮可核状态 | 结论与边界 |
| --- | --- | --- |
| [AgentScope 定向搜索](https://x.com/search?q=%22AgentScope%22&f=live)、[CAO 定向搜索](https://x.com/search?q=%22cli-agent-orchestrator%22&f=live) | 两者 HTTP 200 后转登录引导，未取得项目原帖或互动数。 | C 级观察入口，不能从 GitHub 增星推断 X 传播量或总结群体争论。 |
| [AgentScope 在线权限文档](https://docs.agentscope.io/latest/en/building-blocks/permission-system/overview)底部 X 外链 → [@agentscope](https://x.com/agentscope) | Web 读取该账号返回 403；原生 HTTP 可读，但显示个人姓名与 2009 年旧帖，本轮未取得与该框架关联的证据。 | 文档存在外链不等于账号身份已证实；该账号排除为项目官方原帖来源，不使用其计数。 |

本轮没有足够的当日原帖、回复或转引样本，不能把下文工程问题写成已统计的 X 争论。账号失配只描述本次可读页面，不推断原因或账号归属变化。

## Instagram：宽泛聚合与项目样本分开

- [aiagents 标签入口](https://www.instagram.com/explore/tags/aiagents/)本轮 HTTP 200，转 popular 页面，标题 **129K reels**。这是宽泛主题的四舍五入累计显示，不是今日新增、独立作者数或三个项目的传播量。
- [agentscope 标签入口](https://www.instagram.com/explore/tags/agentscope/)本轮 HTTP 200，转 popular 页面，只读到标题和登录 / 注册导航，未取得可归属项目的帖文、日期、互动或评论。
- 两者均为 C 级观察入口；没有独立可核的 Instagram 项目热度与争议样本，不用历史快照代替今天访问结果。

## YouTube：近期演讲、历史发布与同名框架分开

以下从原生检索列表读取，标题 / 作者经 oEmbed 交叉核对；播放量为累计快照，相对日期保持列表原文。

| 视频 / 频道 | 本轮可核元数据 | 解释与限制 |
| --- | --- | --- |
| [Torchtitan RL: A Unified and Extensible Training Framework for... — Felipe Mello & Jiani Wang](https://www.youtube.com/watch?v=6d2BbUK9l7A)，PyTorch Foundation | **106 次播放、9d ago、19:34**；[检索](https://www.youtube.com/results?search_query=torchtitan)、[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=6d2BbUK9l7A&format=json)。 | B 级近期演讲元数据；未核视频所用 commit、实验条件或完整内容，不当作本页主干性能证据。 |
| [Lecture 39: Torchtitan](https://www.youtube.com/watch?v=VYWRjcUqW6w)，GPU MODE | **5,390 次播放、1y ago、1:23:38**；[同次检索](https://www.youtube.com/results?search_query=torchtitan)、[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=VYWRjcUqW6w&format=json)。 | 固定上游 README 直接链接的历史讲座，README 新闻标注 2024-12；不代表 v0.4.0 或当前主干演示。 |
| [Introducing AgentScope 2.0](https://www.youtube.com/watch?v=t7Ac080UZSM)，Tongyi Lab | **30,514 次播放、5mo ago、4:55**；[检索](https://www.youtube.com/results?search_query=AgentScope+2.0)、[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=t7Ac080UZSM&format=json)。 | B 级历史发布元数据；Web 搜索索引较早显示 30,127，本日报采用本轮原生列表值。频道名与 oEmbed 不是独立效果验证，不能据此认定最新补丁已演示。 |

三个 watch 页面 HTTP 200，但未从中核到完整可用的视频内容；本轮未完整观看、回听或统计评论。[CAO / AWS 检索](https://www.youtube.com/results?search_query=cli+agent+orchestrator+AWS)前列出现通用 AWS Multi-Agent Orchestrator、Kiro 与其他编排器，未确认对应本轮 CAO 仓库，排除为项目视频样本。

## 讨论与争议：把声明还原成可检验条件

以下是固定上游资料引出的工程判断，**不是已测量的社媒共识或群体争论**；具体来源见项目页。

| 议题 | 已核资料 | 判断 / 待验证 |
| --- | --- | --- |
| 确定性是否没有成本 | TorchTitan 上游限定 Search-R1 样本中，计算指标变慢，而整步时间近似持平。 | 分别报告计算、检索、通信和调度；换 workload 后重测，不外推普适加速或免费确定性。 |
| 最后保存的权重能否继续原训练 | TorchTitan 区分 model-only `exports/` 与完整 `step-N`。 | 验证 optimizer、数据状态与步数恢复，不能只检查文件存在。 |
| reviewer profile 是否形成只读边界 | CAO 的工具限制因 provider 而异，Codex 默认 yolo；supervisor 默认可委派更宽工具。 | 查实际进程参数、原生执行拒绝和子任务权限；tmux / prompt 不等于系统隔离。 |
| 本机控制面是否自动按用户隔离 | CAO 默认认证关闭；local token 是全部 scopes 且会传入 agent pane。 | 分别检查可达范围、token、terminal 写入和日志，不把 loopback 等同多用户授权。 |
| workspace / 预算抽象是否是硬保证 | AgentScope LocalWorkspace 是本机 backend；reply budget 阈值后仍有收尾模型调用。 | 执行后端、权限规则、单次调用超额和团队总费用分别验收。 |
| 官方页面链接是否足以证明社媒身份 | AgentScope 文档的 X 外链本轮未形成账号与项目的关联证据。 | 验证可读账号、内容与回链后再归属；缺证时排除，保留准确入口状态。 |

## 验证范围与接续

- 来源核验：十个官方榜单；三个仓库 API、固定主干 SHA、发行列表及非截断树清单；抽读 README、许可、配置、运行 / 权限文档及少量入口。树清单完整不代表全仓审计，论文与安全政策中的每项外部依赖未逐一复核。
- 交付范围：三份七节指南、本日报、首页两个既有分类 / 最新日期 / 实际目录数和 TODO；21 个项目章节、日报七节、1,056 个目录、六文件 365 个本地链接及 60 个有本轮来源 / 访问证据的 URL 核对通过（含 26 个固定 SHA 文件），Markdown lint 零问题。受限入口通过的是状态核对，不表示原帖内容可读。保留用户已有 `AGENTS.md` 修改，不纳入本次提交；提交前核精确暂存范围与空白，推送后核远端 master。
- 接续：目标 GPU 的数值 / 性能与恢复；CAO 实际 provider 版本、权限拒绝与控制面；AgentScope 执行后端、预算与服务隔离；X / Instagram 当日原帖和 YouTube 具体版本、完整内容与评论样本。
- 本轮未执行上游安装、模型 / 云调用、provider 登录、worker 或服务启动、MCP / hook 授权、主机配置更改、GPU / 集群申请、训练 / 推理 / 隔离实验、权重 / 二进制 / 媒体下载或完整观看；资料核读与运行验收分开。
