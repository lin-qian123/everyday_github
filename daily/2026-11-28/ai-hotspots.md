<!-- markdownlint-disable MD013 -->

# AI 热点日报｜2026-11-28

- 采样：2026-11-28（Asia/Shanghai）06:59 起分批获取。官方 `stars today` 是滚动 daily 快照；API stars / forks / open issues、帖文互动与视频播放为累计值，不是本地自然日增量，不合成跨平台排名。
- 范围：综合、Python、TypeScript、JavaScript、Rust、Go、C++、C、Shell、Jupyter Notebook 十个官方 daily 页有界抽样，选三项未建档项目；不声称三项今天首次发布 / 上榜，也不声称穷尽全部 AI 项目。
- 证据：A 为官方榜单、GitHub API / 固定文件及官网；B 为可读原帖 / 原生视频元数据与 oEmbed；C 为搜索、标签、受限入口。作者描述、本轮静态观察与工程判断分别表述。
- 获取：Web 直开 Trending 受限，原生 HTTP 十页均 200；广搜主要得到第三方目录、旧结果和另需核验的新闻，未直接作为技术结论。连接器核项目身份、提交、发行与 tag；较大固定文件经原生 HTTP 获取，未运行上游。
- 去重：按 `projects/` 目录、owner/repo 与三个 repository ID 检查未见既有档案；综合榜已有项目只记录信号。保留已有 `AGENTS.md` 修改及历史身份 / owner-aware 项目键待办。

## 今日重点

- **Agent 后端的关键是实际授权与版本。** Appwrite 在 TypeScript daily +50，当前 Cloud MCP 的 OAuth / 写原因与自托管 stdio / API key 不同；README 镜像 2.7.2、最新所见 2.7.4 和 Cloud 新功能需分别看。[七节解读](../../projects/appwrite/README.md)
- **机器人本地运行栈需要完整主机与硬件验收。** Intrinsic Core 在 C++ daily +7；详细入门比 README 的平台要求更严格，设置脚本会改主机，主线感知模型与旧发行范围不能合并。[七节解读](../../projects/intrinsic-core/README.md)
- **课程完整功能取决于所选阶段。** UnderCover 在 Notebook daily +3，作为低增星教学样本；main 仍是骨架，课末分支才有完整理赔参考实现，公开仓库未见许可。[七节解读](../../projects/undercover/README.md)

## GitHub：三项新增档案与已有热点

| 项目 | 官方 daily 增星 | API 累计 stars / forks / open issues | 版本、许可与身份 |
| --- | --- | --- | --- |
| [appwrite/appwrite](https://github.com/appwrite/appwrite) | TypeScript +50 | 58,696 / 5,918 / 628 | main 11-27；2.7.4 11-19，README 示例仍 2.7.2；BSD-3-Clause；ID `180190854`。 |
| [intrinsic-ai/intrinsic-core](https://github.com/intrinsic-ai/intrinsic-core) | C++ +7 | 811 / 103 / 13 | main 11-27；20261022.0 10-22；根 Apache-2.0，模型 / 第三方另核；ID `1360910719`。 |
| [ed-donner/undercover](https://github.com/ed-donner/undercover) | Jupyter Notebook +3 | 133 / 323 / 10 | main / week3day5-end 各自固定 11-26 SHA；所见 Releases 空、API license 空、两 tree 未见 LICENSE / COPYING；ID `1377599321`。 |

open issues 含 PR；榜单与 API 有采样差。默认 SHA、tag / 阶段 SHA 及固定来源见项目页。低增星项目是补充工程阅读样本，不称跨平台热门或本日新发布。

综合榜已有项目不重复建档；下表只表示本轮榜单信号，没有重新验收旧指南。

| 已收录项目 | 综合 daily 增星 | 观察边界 |
| --- | --- | --- |
| [Claude-BugHunter](https://github.com/elementalsouls/Claude-BugHunter) / [解读](../../projects/Claude-BugHunter/README.md) | +1,615 | 采用量与漏洞有效率、授权测试分开。 |
| [superpowers](https://github.com/obra/superpowers) / [解读](../../projects/superpowers/README.md) | +916 | 流程流行不证明所有任务都需要重流程。 |
| [CLI-Anything](https://github.com/HKUDS/CLI-Anything) / [解读](../../projects/CLI-Anything/README.md) | +668 | 具体软件的命令契约与副作用仍需验收。 |
| [minimind](https://github.com/jingyaogong/minimind) / [解读](../../projects/minimind/README.md) | +667 | 训练时间须匹配设备、配置和任务。 |
| [firecrawl](https://github.com/firecrawl/firecrawl) / [解读](../../projects/firecrawl/README.md) | +833 | 获取能力、来源真实性和使用权分开核。 |

没有仅按增星将 NGINX +148、Ghost-Downloader-3（Python +843）归为 AI 项目；各语言榜也不是共同分母的 AI 排名。

来源：[综合](https://github.com/trending?since=daily)、[Python](https://github.com/trending/python?since=daily)、[TypeScript](https://github.com/trending/typescript?since=daily)、[JavaScript](https://github.com/trending/javascript?since=daily)、[Rust](https://github.com/trending/rust?since=daily)、[Go](https://github.com/trending/go?since=daily)、[C++](https://github.com/trending/c++?since=daily)、[C](https://github.com/trending/c?since=daily)、[Shell](https://github.com/trending/shell?since=daily)、[Jupyter Notebook](https://github.com/trending/jupyter-notebook?since=daily)。

## X：两条可读官方近期原帖，评论样本仍缺

Appwrite 固定 README 直链[官方账号](https://x.com/appwrite)，主页与下列原帖原生 HTTP 均 200，读到正文、显示日期及带标签的互动信息。日期保留页面写法，不擅自将页面时区换成本地自然日。

| 原帖 | 本轮可核元数据 | 讨论内容与边界 |
| --- | --- | --- |
| [PostgreSQL 19 on Appwrite Cloud](https://x.com/appwrite/status/2126383357554806837) | 页面 2026-11-27；1,100 Views、14 likes、2 reposts、0 replies（累计）。 | 作者宣布 Cloud 新数据库默认 PG19，可从 17 / 18 在线升级。[官方公告](https://appwrite.io/blog/post/announcing-postgresql-19)说明切换关闭连接、需重连，升级不可逆；不能简写成零停机 / 可降级。 |
| [project environments beta](https://x.com/appwrite/status/2126043820353827322) | 页面 2026-11-26；1,340 Views、18 likes、2 replies、0 reposts（累计）。 | 作者宣布 Cloud Pro / Enterprise 的 dev / staging / QA environments beta；不是自托管 2.7.4 或所有计划的能力证据。 |

主页置顶的 11-09 MCP1 是另一项产品宣传，未把其“10x”说法归给主仓库或当作本轮性能结论。[UnderCover live 搜索](https://x.com/search?q=%22undercover%22%20%22ed-donner%22&f=live)转登录，没有可读帖文列表；定向广搜也未补得对应当日项目原帖。

上表是官方发布内容与累计互动，不是用户意见抽样。未读取回复正文、统计赞反比例或证明原帖带来了 GitHub 增星。

## Instagram：关联账号受限，标签只能作为入口

- 固定 Appwrite README 关联的[官方 Instagram](https://www.instagram.com/appwrite.io/)本轮原生 HTTP **429**，未得到可复核的当前帖子正文、日期与互动。
- [appwrite 标签](https://www.instagram.com/explore/tags/appwrite/)HTTP 200 后转 popular，标题 **550+ reels**；没有逐帖身份和日期，不能认定均对应本仓库、当前功能或本日发布。
- [aiagents 标签](https://www.instagram.com/explore/tags/aiagents/)HTTP 200，标题 **129K reels**，是宽泛主题累计约数，不能外推三项目热度、独立作者数或今日新增。
- 三者仅作 C 级访问 / 观察记录；未取得当日可独立核实的项目帖子或评论。受限不表示平台没有相关讨论。

## YouTube：两条关联作者的历史视频

固定 README 各自关联 Appwrite / Edward Donner 频道；原生搜索取得下列元数据，oEmbed 再核对标题 / 作者。两 watch 页均 HTTP 200；未完整观看、听评或读取评论。

| 视频 | 本轮原生元数据 | 关联与边界 |
| --- | --- | --- |
| [Appwrite MCP server setup with Cursor](https://www.youtube.com/watch?v=Qzikjm5H7wM) | Appwrite；**2,869 views / 1y ago / 4:33**；[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=Qzikjm5H7wM&format=json)。 | 历史设置视频；不把旧流程当当前 OAuth / 动态工具 / Events 的验证，也未采用同频道 MCP1 视频替代主仓库证据。 |
| [Why Do So Many FDE Jobs Need LangGraph?](https://www.youtube.com/watch?v=9gK0ZMtEsWs) | Edward Donner；**17,136 views / 1mo ago / 12:53**；[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=9gK0ZMtEsWs&format=json)。 | 上游关联作者的 FDE / LangGraph 主题内容；标题与元数据不足以证明讲解了 UnderCover 的指定分支，更不是课程就业效果证据。 |

原生[Appwrite 搜索](https://www.youtube.com/results?search_query=Appwrite+MCP+server+official)与 [FDE 搜索](https://www.youtube.com/results?search_query=Edward+Donner+AI+FDE+UnderCover)还包含其他作者 / 产品；未合并播放量或推定本日传播。未取得可确证的 Intrinsic Core 本轮视频样本。

## 讨论与争议：可检验的工程问题

以下来自固定文档和局部源码，是**工程判断 / 待验项**，不是已采得的社媒争论或用户共识。

| 议题 | 已核事实 | 应核问题 |
| --- | --- | --- |
| 写调用带确认字段就代表人工批准吗 | Appwrite 远程写工具由模型提交 confirm_write 与原因，客户端处理 annotations。 | 实际客户端是否请求审批、用户批准对象与最终写入是否一致。 |
| 同一后端品牌是否意味功能一致 | Cloud OAuth / Events 与本地 stdio / key 不同；README、发行、Cloud 公告各有范围。 | 目标部署的工具集、版本、scope、资源 ACL 和实际数据出口。 |
| online 升级是否可无条件恢复 | Cloud PG19 公告说明切换关闭连接、升级单向。 | 应用重连、兼容、备份与恢复方案；本轮未执行迁移。 |
| 仿真与 local runtime 是否证明实机可用 | Intrinsic 入门有平台 / GPU 要求，脚本改主机；main 新感知与旧发行分开。 | 完整版本组合、标定、控制时延、异常恢复和现场验收。 |
| debug 关闭是否等于无图像发布 | 主线感知磁盘 dump 缺省未设置，visualization 发布默认 true；SAM 3 另有许可。 | 真实订阅者、图像流、权重授权、plans 与冷启动行为。 |
| 课程完成与 checkpoint 是否证明业务正确 | UnderCover main 为骨架；课末有 checkpoint、筛查和 Gateway 代码，阶段签核 / 付款流程有变化。 | 选定阶段的权限、重复效果、失败恢复、隐藏评估与模型筛查漏检。 |
| 公开代码能否直接复用 | Appwrite BSD、Core Apache / 模型另核，UnderCover 未见通用许可证。 | 明确具体组件与用途的许可；不把公开可读当商业授权。 |

## 验证范围与接续

- 核对三 repository ID / 默认提交 / 发行；Intrinsic annotated tag 解引用到 commit，Appwrite 发行 tag 与 main 分开，UnderCover main / 课末 tree 均不截断。Appwrite 大 tree 获取失败，只核根目录和固定文件，不称全仓审计。
- 三份七节项目页归入既有 Agent 框架、AI 学习、办公行业分类，实际目录 `1070 → 1073`；首页日期 / 分类 / 项目数与 TODO 同步。
- 已通过 21 个项目章节、日报七节 / 四平台、分类与 1,073 个目录检查，389 个本地链接存在；68 个来源 / 访问状态 URL 中 67 个 HTTP 200、1 个为上文披露的 Instagram 429。HTTP 200 的登录页 / 标签页限制仍保留；六文件 Markdown lint 和 diff 空白检查通过。只提交本轮六文件，推送后核远端 master。
- 接续：Appwrite 目标客户端授权 / 事件对账 / 副本恢复；Intrinsic 固定环境 / 模型许可 / 仿真和实机验收；UnderCover 目标阶段 / 幂等恢复 / 独立评估 / 许可；社媒当日原帖与回复、指定版本视频内容。
- 本轮仅为内容维护和静态核读；未安装运行上游、读取用户凭据、登录授权、部署、修改主机 / 云资源、连接机器人、迁移上传数据、调用模型 / 云计算、下载权重 / 制品 / 媒体或完整观看。未将作者宣称和静态源码当产品验收。
