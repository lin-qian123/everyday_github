<!-- markdownlint-disable MD013 -->

# AI 热点日报｜2026-11-26

- 采样：2026-11-26（Asia/Shanghai）约 07:00–07:04；`stars today` 是滚动 daily 榜单快照，API stars / forks / open issues 与视频播放量是累计值，不是本地自然日增量，不合成跨平台排名。
- 范围：综合、Python、TypeScript、JavaScript、Rust、Go、C++、C、Shell、Jupyter Notebook 十个官方 daily 页有界抽样。三项是本仓库今日新建档案，不声称今天首次上榜或发布。
- 证据：A 为官方榜单 / API、固定 SHA 文档与局部源码 / 发行；B 为视频标题、作者与原生计数；C 为搜索、标签聚合与受限入口。作者声明、静态判断和本轮运行验证分开。
- 获取：Web 工具直开 Trending 受限，原生 HTTP 十页均 200 并读到项目行；广搜主要返回目录、新闻与旧内容，定向搜索未获得可读的当日项目社媒原帖。仓库事实采用 GitHub 连接器 API、README、非截断 tree 与固定文件局部核读；没有执行上游。搜索缺口不代表当天没有讨论。
- 去重：对照 `projects/` 目录、owner/repo 文内映射和 repository ID；三项未见既有档案。既有高热项目只记本次榜单信号，保留 `AGENTS.md` 原修改及历史身份 / 同名项目键待办。

## 今日重点

- **代理选型先看确切版本和凭据路径。** `Antigravity-Manager` Rust +134：稳定 v5.0.4 / 默认 main 与 beta.2 是不同 SHA；鉴权修复列在预发行中。README 的“加密 SQLite”声明不能覆盖所查 JSON token 写入路径。[七节解读](../../projects/Antigravity-Manager/README.md)
- **RAG 教程把最新介绍与旧示例分开。** `llm-universe` Notebook +9：C1 刚更新代表型号，C4 / C5 仍示范 GPT-4o 和旧 Chroma 路径；v1 是 2024 PDF。教学 M/N 是在答案在库前提下的查询级命中率。[七节解读](../../projects/llm-universe/README.md)
- **图文匹配分数需要任务校准。** `CLIP` Notebook +8：旧模型再次进入观察范围，默认分支三月提交是 CI 引用更新；softmax 受候选类别影响，模型卡用途建议和 MIT 许可须分开理解。[七节解读](../../projects/CLIP/README.md)

## GitHub：三项新增档案与已有热点

| 项目 | 官方 daily 增星 | API 累计 stars / forks / open issues | 版本与证据 |
| --- | --- | --- | --- |
| [lbjlaq/Antigravity-Manager](https://github.com/lbjlaq/Antigravity-Manager) | Rust +134 | 34,039 / 3,604 / 1,711 | 稳定 v5.0.4（11-20），预发行 v5.0.5-beta.2（11-25）；API NOASSERTION，实际 CC BY-NC-SA 4.0；ID `1104535633`。 |
| [datawhalechina/llm-universe](https://github.com/datawhalechina/llm-universe) | Jupyter Notebook +9 | 14,346 / 1,455 / 18 | 11-25 主线更新 C1；v1（2024-04-14）仅 PDF 发行；API license null，非截断 tree 无许可文件；ID `711550638`。 |
| [openai/CLIP](https://github.com/openai/CLIP) | Jupyter Notebook +8 | 34,659 / 4,068 / 274 | 默认提交 2026-03-25；Releases 空、setup.py 1.0，不是新模型；MIT，ID `321960447`。 |

open issues 含 PR；榜单与 API 有采样差。Antigravity-Manager API pushed_at 为 11-25 14:16 UTC，但默认分支仍是稳定 tag 对应 SHA，不能据此推定 beta 已合入 main。固定版本、源码和实际许可见三份项目页。

综合榜头部 AI 项目已有目录，本轮不重复建档；以下只更新本日报观察，不构成重新验收其既有说明。

| 已收录项目 | 综合 daily 增星 | 观察边界 |
| --- | --- | --- |
| [Claude-BugHunter](https://github.com/elementalsouls/Claude-BugHunter) / [解读](../../projects/Claude-BugHunter/README.md) | +1,644 | 技能增长或增星不能证明实际漏洞有效率。 |
| [superpowers](https://github.com/obra/superpowers) / [解读](../../projects/superpowers/README.md) | +902 | 流程和技能的采用热度与结果质量分开。 |
| [CLI-Anything](https://github.com/HKUDS/CLI-Anything) / [解读](../../projects/CLI-Anything/README.md) | +1,094 | 软件工具化仍需按具体应用验收。 |
| [minimind](https://github.com/jingyaogong/minimind) / [解读](../../projects/minimind/README.md) | +828 | 训练时间 / 成本受设备、模型与训练范围约束。 |
| [firecrawl](https://github.com/firecrawl/firecrawl) / [解读](../../projects/firecrawl/README.md) | +1,131 | 内容可获取与内容权利、真实性分别核对。 |

[NGINX](https://github.com/nginx/nginx) +174 和 [Ghost-Downloader-3](https://github.com/XiaoYouChR/Ghost-Downloader-3) +950 未按热度机械归为 AI 项目。综合榜并非按增星严格排序，本表顺序不代表跨平台或全领域排名。

来源：[综合](https://github.com/trending?since=daily)、[Python](https://github.com/trending/python?since=daily)、[TypeScript](https://github.com/trending/typescript?since=daily)、[JavaScript](https://github.com/trending/javascript?since=daily)、[Rust](https://github.com/trending/rust?since=daily)、[Go](https://github.com/trending/go?since=daily)、[C++](https://github.com/trending/c++?since=daily)、[C](https://github.com/trending/c?since=daily)、[Shell](https://github.com/trending/shell?since=daily)、[Jupyter Notebook](https://github.com/trending/jupyter-notebook?since=daily)。

## X：当日原帖与回复样本缺口

| 来源入口 | 本轮可复核状态 | 可支持的结论 |
| --- | --- | --- |
| [Antigravity-Manager live 搜索](https://x.com/search?q=%22Antigravity-Manager%22&f=live) | HTTP 200 后转 login onboarding，没有帖文列表。 | C 级访问状态；没有日期、互动或回复样本，不能评价今日传播。 |
| [llm-universe live 搜索](https://x.com/search?q=%22llm-universe%22&f=live) | 同样转登录。 | 搜索入口可追溯，但未取得项目讨论证据。 |

Web 定向检索也没有补到可独立读取的当日原帖。不把 README 宣传、发行说明或下述工程疑问当成 X 用户共识；不沿用前日互动量。

## Instagram：宽泛累计量与项目访问限制

- [aiagents 标签](https://www.instagram.com/explore/tags/aiagents/)本轮转 popular，HTTP 200，标题为 **129K reels**。这是宽泛主题累计约数，不是今日新增、独立作者数或三项目热度。
- [openaiclip 标签](https://www.instagram.com/explore/tags/openaiclip/)转 accounts/login，HTTP 429；未取得帖子、发布时间、互动或评论。
- 两项只记 C 级入口与访问状态。未获得三个仓库的项目级 Instagram 传播或争议证据。

## YouTube：两条历史元数据与同名排除

原生搜索数据提供下列累计播放、相对年龄与时长，oEmbed 交叉核标题 / 作者；两条 watch 页均 HTTP 200。页面可达与元数据核对不等于完整观看、听评或技术复现。

| 视频 | 本轮元数据 | 关联与限制 |
| --- | --- | --- |
| [OpenAI CLIP: ConnectingText and Images (Paper Explained)](https://www.youtube.com/watch?v=T9XSU0pKX2E) | Yannic Kilcher；**183,575 views / 5y ago / 48:07**；[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=T9XSU0pKX2E&format=json)。 | 第三方历史论文讲解。Web 索引旧值 181,945 不当作当前量；视频不能证明本轮设备性能或新的模型能力。 |
| [GitHub - datawhalechina/llm-universe…](https://www.youtube.com/watch?v=hs5qdoQhQlA) | GitHub Daily Trend AI Podcast；**420 views / 1y ago / 4:08**；[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=hs5qdoQhQlA&format=json)。 | 第三方历史仓库介绍，标题直接关联 owner/repo；不认作 Datawhale 官方课程或当前依赖已跑通的证据。 |

[Antigravity-Manager 搜索](https://www.youtube.com/results?search_query=Antigravity-Manager)首批结果主要谈 Google Antigravity 的 Agent Manager / 工作流，未取得对应 `lbjlaq` 仓库的确证，未挪用其播放量。[课程搜索](https://www.youtube.com/results?search_query=llm-universe+Datawhale)、[CLIP 搜索](https://www.youtube.com/results?search_query=OpenAI+CLIP+Yannic+Kilcher)亦含无关候选。没有采评论或据此统计赞同 / 争议规模。

## 讨论与争议：将文档差异转成可检验问题

以下是固定来源引出的**工程判断和待验项**，不是社媒观点统计；具体出处见项目页。

| 议题 | 已核事实 | 接下来应核 |
| --- | --- | --- |
| 最新发行是否等于稳定 / main | Manager beta.2 声明移除静态后缀鉴权豁免，稳定 / main 仍含该判断。 | 目标 tag、已安装制品、实际路由拒绝路径与修复覆盖；本轮未利用或安全复测。 |
| 原子写入是否等于加密 | Manager 将包含 token 的账户对象序列化 JSON 并原子落盘，与 README 的加密 SQLite 宣传不一致。 | 目标版本真实文件、权限、备份 / 同步和密钥撤销；不读取用户现有凭据来推定结果。 |
| 本地知识库是否等于离线 | 课程界面本地运行，embedding 与回答仍使用配置的云 API。 | 文档 / 对话数据出口、预算、索引模型一致性与多用户边界。 |
| 教程准确率是否等于片段精度 | C5 M/N 以每题答案在库、前 K 片段至少命中一次为成功。 | 明确 Hit@K、知识缺失、多证据覆盖、拒答与冻结测试集；模型自评需独立抽检。 |
| 高匹配分是否等于可信概率 | CLIP 归一化特征乘可学习尺度，候选类上 softmax。 | 类别与提示变化、校准、开放集拒识及领域 / 语言测试。 |
| 公开可读是否等于同一种复用许可 | Manager CC BY-NC-SA、课程无所见许可、CLIP MIT 与模型卡用途建议并存。 | 逐项目核授权、具体用途与输入资料权利，不以 stars 或开源标签推断。 |

## 验证范围与接续

- 三个上游 ID、默认 SHA、非截断 tree、README 与发行集合已核；tree 完整不等于全仓审计。新增三份七节页及日报，复用 Coding Agents、AI 学习、语音视频多模态三个既有分类，实际目录 `1064 → 1067`；首页日期 / 导航和 TODO 同步。
- 已通过 21 个项目章节、日报七节 / 四平台、1,067 个实际目录及分类 / 去重 / 日期、381 个本地链接检查。62 个来源 / 访问状态 URL 中 61 个 HTTP 200，Instagram 项目标签 429 已列明；24 个 GitHub blob 展示页返回 503，已改用同 SHA 的可达 raw 文件，不作为源码缺失。六文件 Markdown lint 与 diff 空白检查通过；仅提交本轮六文件，发布后核对远端 master。
- 接续：Manager 目标版本修复 / 凭据格式 / 日志与恢复；课程独立环境 / API / 索引 / 冻结测试集与许可；CLIP 可信权重 / 目标领域与语言 / 候选和拒识；当日社媒原帖、回复及视频具体版本。
- 本轮未安装运行上游、读取用户凭据、登录授权、切换账户、启动服务 / 代理、改宿主配置、上传文档、迁移数据库、调用模型、下载权重 / 制品 / PDF / 媒体、做安全 / 性能实验或完整观看。静态核读与运行验收分别记录。
