<!-- markdownlint-disable MD013 -->

# AI 热点日报｜2026-11-21

- 采样：2026-11-21（Asia/Shanghai）07 时段；事件和发行日期单列。GitHub `stars today`、API 累计值、社媒互动与视频播放量均为本轮快照，不是自然日结算。
- 范围：综合、Python、TypeScript、JavaScript、Go、Rust、C++、Swift、Jupyter Notebook、Shell 十个官方 daily 页的有界抽样；新增三份项目指南，不声称覆盖所有新上榜项目，不合成跨平台排名。
- 证据：A 为官方榜单 / GitHub API / 固定 SHA 文件；B 为社媒原帖和平台元数据；C 为搜索、宽泛聚合或受限入口。作者声明、资料核读、本文判断与运行验收分别标识。
- 获取：广泛 Web 检索混入旧闻、聚合与同名内容；项目定向社媒检索也未形成完整样本。项目采用官方 Trending HTTP 与 GitHub 连接器，社媒再用原生页面 / oEmbed 核查。检索缺口不表示没有讨论。
- 接续：按 `projects/` 目录、上游 owner/repo、旧名称及稳定仓库 ID 去重；沿用既有两个分类。此前页面和用户已有 `AGENTS.md` 修改保留，所有本日报计数重新读取。

## 今日重点

- **持续执行需要可审阅的默认值。** Nightshift Shell +35；磁盘清单、hook 和恢复进程帮助接续，但默认 `isolation=none`、工具策略 `auto-add`、证据文件检查 off。能持续工作与结果可验收需要分别建立条件。[项目解读](../../projects/nightshift/README.md)
- **证明应回答“证明了什么”。** Bend TypeScript +95；用 laws 约束 AI 实现，但 `--verdict` 的内核、未证明的翻译过程和执行后端属于不同信任层。当前没有 F64，F32 运算仍有证明边界。[项目解读](../../projects/bend/README.md)
- **新版本要保留失败与回退。** vllm-ascend Python +7；stable v0.30.0、RC v0.32.0rc1、main 不能混写。RC 明列特定 GLM workload 的稳定性问题与最多约 50% 吞吐回退，是限定场景的上游报告。[项目解读](../../projects/vllm-ascend/README.md)

## GitHub 热点项目

API 依次为 stars / forks / open issues（含 PR）；不是当日新增 issues。跨语言上榜的同一仓库不累加。

| 项目与动作 | 本轮热度 / 发行 | 沿用分类 | 工程关注 |
| --- | --- | --- | --- |
| [nightshift](../../projects/nightshift/README.md)，新增 | Shell +35；566 / 24 / 5；[API](https://api.github.com/repos/orwa-mahmoud/nightshift)；[v0.37.2](https://github.com/orwa-mahmoud/nightshift/releases/tag/v0.37.2)，UTC 11-19 19:16 / 北京时间 11-20 03:16，非预发行。 | Coding Agents 与终端助手 | 宿主 hooks、默认权限、恢复成本、逐项检查与证据内容。 |
| [bend](../../projects/bend/README.md)，新增 | TypeScript +95；25,694 / 820 / 161；[API](https://api.github.com/repos/bendlang/bend)；[v2.0.40](https://github.com/bendlang/bend/releases/tag/v2.0.40)，UTC 11-06，非预发行。 | 模型、训练与推理基础设施 | laws 覆盖、checker / kernel / compiler、unsafe、浮点与并行条件。 |
| [vllm-ascend](../../projects/vllm-ascend/README.md)，新增 | Python +7；3,127 / 2,794 / 5,433；[API](https://api.github.com/repos/vllm-project/vllm-ascend)；stable [v0.30.0](https://github.com/vllm-project/vllm-ascend/releases/tag/v0.30.0)，UTC 10-29；更新的 [v0.32.0rc1](https://github.com/vllm-project/vllm-ascend/releases/tag/v0.32.0rc1)，UTC 11-10，预发行。 | 模型、训练与推理基础设施 | 驱动和用户态栈、型号 / 模型 / 功能组合、数值精度与版本回退。 |

- 三个唯一仓库 ID 为 `1300273081 / 684776900 / 924058625`；项目目录 **1,050 → 1,053**。Bend 同时检查旧名称 `HigherOrderCO/Bend`，未找到本仓库已有同身份档案。
- 头部多数已建档，本轮仅更新其热度观察：综合 daily 的 Claude-BugHunter +1,660、Firecrawl +1,226、AutoClip +983、Superpowers +888、App Store Compliance +874、MiniMind +841、CLI-Anything +774；语言页还见 FreeVideo Python +304、Splash C++ +116。未重新审计这些项目，也不由榜位推断质量。
- 新建档不代表今天首发；本轮三项来自语言页，不是综合榜前三。普通下载器、Web 框架和非 AI 系统工具不只因上榜就纳入重点。同名 `skills` 的 owner-aware key 和 taste-skill 的身份缺口仍留待解决。
- 来源：[综合 daily](https://github.com/trending/?since=daily)、[Python](https://github.com/trending/python?since=daily)、[TypeScript](https://github.com/trending/typescript?since=daily)、[JavaScript](https://github.com/trending/javascript?since=daily)、[Go](https://github.com/trending/go?since=daily)、[Rust](https://github.com/trending/rust?since=daily)、[C++](https://github.com/trending/c++?since=daily)、[Swift](https://github.com/trending/swift?since=daily)、[Jupyter Notebook](https://github.com/trending/jupyter-notebook?since=daily)、[Shell](https://github.com/trending/shell?since=daily)，均为本轮 HTTP 200；页面随时间变化。

## X：Bend 历史原帖可核，今日传播仍有缺口

| 来源与身份 | 本轮可核内容 / 热度 | 时间与讨论边界 |
| --- | --- | --- |
| [@bendlang](https://x.com/bendlang)，由固定上游 README 链接，账号回链 bend-lang.com。 | HTTP 200，可读项目简介和转引；沿账号原帖链接取得作者 [Taelin 的原帖](https://x.com/VictorTaelin/status/2104240438127288652)，[oEmbed](https://publish.twitter.com/oembed?url=https://x.com/VictorTaelin/status/2104240438127288652)匹配作者及日期。 | 账号身份与项目关系有上游链路；账号粉丝数不用于项目传播估计。 |
| 同一 Taelin 原帖 | 原生页面显式 aria-label：**148,435 views、767 likes、49 reposts、32 replies**，均为累计快照。作者说明 BendTT 内核、悬赏，并区分证明和仍有 bug 的编译器。 | oEmbed 日期为 **2026-09-27**，针对 Bend 2.0.32；这是历史背景，不能当作今天新发布、v2.0.40 实测或当前悬赏条款已核验。未读取完整回复样本。 |
| [Nightshift / Orwa 定向搜索](https://x.com/search?q=%22nightshift%22%20%22orwa%22&f=live) | HTTP 200 后进入登录引导。 | C 级入口，没有项目原帖、互动统计或今日讨论样本，不从 GitHub 增星换算 X 热度。 |

本节可确认作者公开区分 proof kernel 与 compiler，不能据此宣称社区达成共识，也没有足够样本总结今天的群体争论。

## Instagram：主题聚合可读，项目原帖未核

- [aiagents 标签入口](https://www.instagram.com/explore/tags/aiagents/)本轮 HTTP 200，转 popular 页面，标题 **129K reels**。这是宽泛累计聚合的四舍五入快照，不是今天新增、独立作者数或本轮三个项目的传播量。
- [bendlang 标签入口](https://www.instagram.com/explore/tags/bendlang/)本轮 HTTP 200 后进入登录页，未取得帖文、官方账号归属、评论或互动量。
- 两者均为 C 级入口；没有可以确认项目热度与争议的 Instagram 原帖样本，不复用历史访问状态充当本日数据。

## YouTube：近期 Bend 演讲与历史发布分开

以下取自原生检索列表，标题 / 作者经 oEmbed 交叉核对；播放量为累计值，相对时间保留列表原文。

| 视频与作者 | 本轮可核元数据 | 解释与限制 |
| --- | --- | --- |
| [Bend: A Linear Proof Language That Matches C Performance and Runs on GPUs — Victor Taelin](https://www.youtube.com/watch?v=PqufdZ5skWQ)，SF Lean Meetup | **17,448 次播放、1d ago、1:03:32**；[检索](https://www.youtube.com/results?search_query=Bend+2+language+proof)、[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=PqufdZ5skWQ&format=json)。 | B 级近期演讲元数据；性能措辞属于标题，未完整观看或复现其比较，具体版本未核。 |
| [Bend 2 is here!](https://www.youtube.com/watch?v=J_IPgREVM2E)，频道名称 Bend | **3,796 次播放、2mo ago、4:20**；[同次检索](https://www.youtube.com/results?search_query=Bend+2+language+proof)、[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=J_IPgREVM2E&format=json)。 | B 级历史发布元数据；同名频道不能仅凭名称认定官方，不能用此视频证明最新稳定版效果。 |

两个 watch 页面 HTTP 200，但只取得页面壳，未完整观看或统计评论。另检索 [Nightshift](https://www.youtube.com/results?search_query=nightshift+orwa+coding)主要出现夜班音乐等同名条目，排除；[vLLM Ascend](https://www.youtube.com/results?search_query=vllm+ascend)前列混入通用 vLLM / AMD 视频，不当作 Ascend 插件实测。第三方 Web 检索也找到较早的 Ascend 演讲线索，本轮未升级为今日热点或性能证据。

## 讨论与争议：把完成、证明和支持拆成可核条件

以下为上游资料引出的工程问题，**不是已统计的社媒争论**。具体固定 SHA 来源见三份项目页。

| 议题 | 已核资料 | 判断 / 后续验证 |
| --- | --- | --- |
| 任务全部打勾是否代表验收完成 | Nightshift 默认证据 check / review 均 off；block 只验证命名文件存在。 | 指定可检验 Verify，再打开截图、图表或录屏；产物存在与内容正确分开验收。 |
| “无人值守”是否自动收敛权限 | Nightshift 默认无 worktree 隔离，auto-add，五类 elevation allow，保护模式为空；文档明确 guards 不是 sandbox。 | 对目标项目设置规则、预算和宿主权限，并测试真正的拒绝 / 恢复路径。 |
| 形式化内核是否证明整个应用无 bug | Bend 的 parser / 翻译未证明，默认 checker 与执行后端另有边界；作者历史原帖也主动区分 compiler。 | 先审 laws，验证故意破坏性质能被拒绝，再比较目标后端输出。 |
| 并行语言是否可直接用于现有科研计算 | Bend 无 F64、F32 运算仍为公理、当前单 GPU / 无多机且需要均衡调用。 | 先选离散不变量做小实验；不能推断可替代双精度数值工具链。 |
| 支持两个功能是否意味着可以叠加 | vllm-ascend feature matrix 有部分、不兼容与未知组合。 | 固定硬件、模型、量化和并行配置，逐项开启并保留正确性和失败样本。 |
| 更新 RC 是否必然更快更稳定 | v0.32.0rc1 披露特定 GLM 场景长压服务故障与最多约 50% 吞吐回退；v0.30.0 也有已知问题和上游安全补丁提示。 | 对所用制品核修复状态，测端到端分布和稳定性，不用更新日期代替验收。 |

## 验证范围与接续

- 来源核验：十个官方榜单；三个仓库 API、main SHA、发行列表和非截断树清单；抽读固定 README、许可、配置、指南及 vllm-ascend 少量注册入口。树完整不代表读完源码，Bend 论文、Lean 形式化及上游性能图未完整复核。
- 交付：三份七节项目指南、本日报、首页两个既有分类 / 最新日期 / 实际目录数和 TODO。已通过 21 个项目章节、日报七节、1,053 个目录、六文件 360 个本地链接及 55 个有当轮来源 / 访问证据的 URL 核对（含 22 个固定 SHA 文件）；Markdown lint 零问题。保留已有 `AGENTS.md` 修改并排除提交，提交前再核精确暂存范围与空白，推送后核远端 master。
- 接续：Nightshift 在目标宿主的 gate / 恢复 / 预算与证据内容；Bend 规格保护和不同后端输出；vllm-ascend 目标硬件的版本组合、精度及已知问题修复。X / Instagram 今日原帖、YouTube 版本关联与评论样本仍待补证。
- 未执行：上游安装、插件或 hook 授权、宿主配置更改、定时任务注册、Agent / 模型调用、NPU 申请、权重 / 二进制 / 媒体下载、推理 / 编译 / 证明重跑、设备 / 数值 / 性能 / 隔离或漏洞实验、完整观看与评论统计。资料核读与运行验收分开。
