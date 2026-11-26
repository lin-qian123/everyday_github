<!-- markdownlint-disable MD013 -->

# AI 热点日报｜2026-11-27

- 采样：2026-11-27（Asia/Shanghai）约 06:58–07:03。`stars today` 是官方滚动 daily 榜单快照；API stars / forks / open issues 与视频播放量为累计值，不是本地自然日增量，不合成跨平台排名。
- 范围：综合、Python、TypeScript、JavaScript、Rust、Go、C++、C、Shell、Jupyter Notebook 十个官方 daily 页有界抽样，选取三项新建档案，不声称今天首次上榜或发布，也不是全榜全部 AI 项目的穷尽清单。
- 证据：A 为官方榜单 / GitHub API、固定 SHA 文档与局部源码 / 发行；B 为原生视频元数据和 oEmbed；C 为搜索、标签与受限入口。作者实验、静态判断、本轮运行验证分别记录。
- 获取：Web 直开 Trending 受限，原生 HTTP 十页均 200 并读到项目行；广搜主要为聚合目录、旧内容及另需核验的新闻，未直接用作技术结论。GitHub 连接器核 metadata、提交、完整 tree、README、发行与 tag；较大源码经固定 SHA HTTP 获取后局部核读，没有执行上游。
- 去重：按 `projects/` 目录、owner/repo 和 repository ID 核对三项未见既有档案；综合榜已有项目仅记信号。保留原有 `AGENTS.md` 修改和历史身份 / 同名项目键待办。

## 今日重点

- **客户端增强要核实际权限与数据路径。** WorkDaddy 在 JavaScript daily +49，通过 CDP 接入登录中的客户端；免打扰会改宿主策略或自动点允许，诊断默认开，导出加密与原样备份是不同路径。[七节解读](../../projects/WorkDaddy/README.md)
- **成熟课程仍需明确环境和评估口径。** pytorch-deep-learning 在 Notebook daily +12；旧 SETUP、等 batch 平均、每 epoch 看 test 与仅保存参数，分别影响环境、指标、独立测试和恢复。[七节解读](../../projects/pytorch-deep-learning/README.md)
- **配方可追踪不等于当前资源已跑通。** Nemotron 在 Notebook daily +2，作为补充工程样本；主线晚于 v0.2.0，Python / 许可元数据有差异，Parse 的 80 GB 是待完整验证建议，tiny 不自动降低 batch。[七节解读](../../projects/Nemotron/README.md)

## GitHub：三项新增档案与已有热点

| 项目 | 官方 daily 增星 | API 累计 stars / forks / open issues | 版本、许可与身份 |
| --- | --- | --- | --- |
| [babygoton/WorkDaddy](https://github.com/babygoton/WorkDaddy) | JavaScript +49 | 3,510 / 385 / 185 | 1.2.23（11-22）；tag / main 提交不同、compare 文件差异为空；API NOASSERTION，实际 AGPL-3.0-or-later；ID `1338532566`。 |
| [mrdbourke/pytorch-deep-learning](https://github.com/mrdbourke/pytorch-deep-learning) | Jupyter Notebook +12 | 19,486 / 5,244 / 151 | 默认提交 09-27 修 widget metadata，Releases 空；MIT；ID `418718534`。 |
| [NVIDIA-NeMo/Nemotron](https://github.com/NVIDIA-NeMo/Nemotron) | Jupyter Notebook +2 | 2,392 / 504 / 98 | main 11-23 更新 Parse；v0.2.0 10-15；根许可 Apache-2.0、Python 元数据 MIT；ID `1069235905`。 |

open issues 含 PR；榜单与 API 存在采样差。三个项目的默认 SHA、固定文件与发行身份见项目页；没有把更新时间、main 的 package version 或“作者已验证版本”当成当前设备验收。

综合榜已有项目不重复建档，下表只保留本次榜单信号，不构成重新验收旧指南。

| 已收录项目 | 综合 daily 增星 | 观察边界 |
| --- | --- | --- |
| [Claude-BugHunter](https://github.com/elementalsouls/Claude-BugHunter) / [解读](../../projects/Claude-BugHunter/README.md) | +1,600 | 技能增星不等于有效漏洞发现率。 |
| [superpowers](https://github.com/obra/superpowers) / [解读](../../projects/superpowers/README.md) | +853 | 流程采用量与实际交付质量分开。 |
| [CLI-Anything](https://github.com/HKUDS/CLI-Anything) / [解读](../../projects/CLI-Anything/README.md) | +744 | 软件工具化需对具体应用与版本验收。 |
| [minimind](https://github.com/jingyaogong/minimind) / [解读](../../projects/minimind/README.md) | +701 | 训练成本需匹配设备、数据和目标。 |
| [firecrawl](https://github.com/firecrawl/firecrawl) / [解读](../../projects/firecrawl/README.md) | +1,042 | 获取内容能力与内容真实性、权利分开核对。 |

未将 [NGINX](https://github.com/nginx/nginx) +150 或 [Ghost-Downloader-3](https://github.com/XiaoYouChR/Ghost-Downloader-3) +887 按增星机械归为 AI 项目。各语言榜也不是跨领域排行榜。

来源：[综合](https://github.com/trending?since=daily)、[Python](https://github.com/trending/python?since=daily)、[TypeScript](https://github.com/trending/typescript?since=daily)、[JavaScript](https://github.com/trending/javascript?since=daily)、[Rust](https://github.com/trending/rust?since=daily)、[Go](https://github.com/trending/go?since=daily)、[C++](https://github.com/trending/c++?since=daily)、[C](https://github.com/trending/c?since=daily)、[Shell](https://github.com/trending/shell?since=daily)、[Jupyter Notebook](https://github.com/trending/jupyter-notebook?since=daily)。

## X：登录限制下的当日讨论缺口

| 来源入口 | 本轮可复核状态 | 能支持的结论 |
| --- | --- | --- |
| [WorkDaddy live 搜索](https://x.com/search?q=%22WorkDaddy%22&f=live) | Web 403；原生 HTTP 200 后转 login onboarding，无帖文列表。 | C 级访问记录；无当日帖子、互动或回复样本。 |
| [Nemotron live 搜索](https://x.com/search?q=%22Nemotron%22&f=live) | 原生 HTTP 同样转登录页。 | 搜索入口可追溯，不能据此判断传播量或用户共识。 |

定向 Web 检索未补得可独立读取的当日项目原帖。此缺口不表示当天没有讨论；不将 README 宣传、工程疑问或前日互动量改写为本日 X 争议。

## Instagram：主题入口可达，项目互动未核实

- [aiagents 标签](https://www.instagram.com/explore/tags/aiagents/)原生 HTTP 200，转 popular，标题 **129K reels**；这是宽泛主题累计约数，不是三项目热度、独立作者数或今日新增。
- [nemotron 标签](https://www.instagram.com/explore/tags/nemotron/)原生 HTTP 200，转 popular，标题仅为 Nemotron；未取得可独立复核的项目帖子日期、互动量和评论样本。Web 工具直开受节流限制。
- 两项仅记 C 级入口 / 访问状态；不把标签名一致认定为具体仓库、型号或版本的传播证据。

## YouTube：两条上游关联的历史视频元数据

下列视频均由所查 README 关联；原生搜索提供累计播放、相对年龄与时长，oEmbed 交叉核对标题 / 作者。两条 watch 页均 HTTP 200，但只是页面与元数据证据，未完整观看、听评或读取评论。

| 视频 | 本轮原生元数据 | 关联与边界 |
| --- | --- | --- |
| [Learn PyTorch for deep learning in a day. Literally.](https://www.youtube.com/watch?v=Z_ikDlimN6A) | Daniel Bourke；**2,207,484 views / 4y ago / 25:36:58**；[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=Z_ikDlimN6A&format=json)。 | 作者历史课程，README 说明覆盖 00–04，不等于完整 00–09；标题中的一天不是学习效果或当前安装耗时保证。Web 索引旧播放量未沿用。 |
| [Why NVIDIA Built Nemotron—Open Models, Datasets, and Techniques for the Future of AI](https://www.youtube.com/watch?v=_y9SEtn1lU8) | NVIDIA；**3,144,302 views / 1y ago / 3:41**；[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=_y9SEtn1lU8&format=json)。 | 官方历史家族概览，不当作 11-23 Parse 主线、指定模型质量或今日仓库传播的证据。 |

原生[课程搜索](https://www.youtube.com/results?search_query=Daniel+Bourke+Learn+PyTorch+in+a+day)与 [Nemotron 搜索](https://www.youtube.com/results?search_query=NVIDIA+Nemotron+overview)另有不同作者、型号与年代的候选，未合并播放量。WorkDaddy 定向视频搜索未取得确证样本；不以相近名称视频代替。没有据此统计赞同、反对或争议规模。

## 讨论与争议：把文档差异转成可检验问题

以下是固定来源引出的**工程判断 / 待验项**，不是社媒观点调查；出处见各项目参考资料。

| 议题 | 已核事实 | 接下来应核 |
| --- | --- | --- |
| 免打扰是否只是界面优化 | WorkDaddy 会改宿主 sandbox 字段或自动点允许；无保存状态时五项 false。 | 当前客户端实际策略、已有开关、允许目录 / 命令和关闭后的恢复。 |
| 账号留本机是否等于无出口 / 全部加密 | 原样备份保留原认证格式；导出另有加密；诊断默认开启，部分功能访问官方 / 模型服务。 | 目标版本凭据、诊断脱敏、备份权限、模型测试及同步数据流。 |
| 教学指标是否就是最终泛化指标 | PyTorch 示例等 batch 平均且每 epoch 看 test，保存器只写模型 state_dict。 | 逐样本统计、独立盲测、完整训练状态和重开恢复。 |
| 目录元数据可查是否等于任务能跑 | Nemotron Steps 查询不需要 GPU，Parse 训练另有硬件与分阶段依赖。 | root Python 实际限制、控制器 / 阶段环境、真实显存与磁盘。 |
| tiny / lock 是否保证低成本和完整复现 | Parse tiny 不降低默认 SFT batch；继承容器只对额外包解析，80 GB 建议待完整验证。 | 目标输入 / batch、镜像包栈、模型 lineage、恢复和 matched held-out 评估。 |
| 公开仓库是否只有一种许可 | WorkDaddy 实际 AGPL；课程 MIT；Nemotron 根 Apache 与 Python MIT 元数据冲突，数据 / 模型另有条件。 | 具体组件、制品、用途与输入材料的授权，先解决元数据歧义。 |

## 验证范围与接续

- 三个 repository ID、默认提交、非截断 tree、README、发行集合与两个发行 tag 已核；WorkDaddy tag / main compare 文件差异为空。完整 tree 不等于全仓审计，较大文件只围绕所述路径局部核读。
- 本轮新增三份七节页和四平台日报，复用 Coding Agents、AI 学习、模型训练三个既有分类；实际目录 `1067 → 1070`，首页导航 / 日期 / 项目数与 TODO 同步。
- 已通过 21 个项目章节、日报七节 / 四平台、1,070 个目录及分类 / 日期检查，385 个本地链接存在；60 个来源 / 访问状态 URL 均 HTTP 200（本轮获取记录复用与缺项定向核对），社媒 200 的登录页 / 标题页限制仍按上文保留。六文件 Markdown lint 与 diff 空白检查通过；仅提交本轮六文件，发布后核对远端 master。
- 接续：WorkDaddy 目标客户端权限 / 凭据 / 诊断 / 会话恢复；课程独立环境 / 指标 / 盲测 / 训练恢复；Nemotron 许可元数据 / 阶段依赖 / 资源与完整验证；当日社媒原帖、回复及视频具体版本。
- 未安装运行上游、读取用户凭据、登录授权、切号、启动 daemon / CDP / 服务、修改宿主配置、调用模型 / 云计算、上传或迁移数据、下载权重 / 制品 / 媒体、做性能 / 安全实验或完整观看。静态说明不代表产品验收。
