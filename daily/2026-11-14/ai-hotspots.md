<!-- markdownlint-disable MD013 -->

# AI 热点日报｜2026-11-14

- 采样：2026-11-14（Asia/Shanghai）01 时段；GitHub daily 日增、累计 stars 与视频播放为分时快照，不是自然日结算。历史发布与教程单列。
- 范围：官方综合、Python、TypeScript、Rust、Go、JavaScript、C++、Swift、Jupyter Notebook 九页，有界抽样，不合成跨平台排名。
- 证据：A 为官方榜单 / API / 固定 SHA 文件；B 为平台原生元数据；C 为聚合或受限入口。静态核读、上游评测和实际运行分别表述。
- 获取：广泛搜索多为汇总，定向四条社媒检索无结果，search-layer 也无有效候选；以官方 HTTP daily 选样，GitHub 连接器核仓库身份、主线 SHA、完整目录树、发行与引用文件，另核 npm、官方权重元数据和 STQ PR。空搜索不代表没有讨论。
- 日期边界：最近已发布日报为 11-12，本轮只记录当前采样，不将今天快照回填成 11-13 的历史数据。

## 今日重点

- **代码审查先看覆盖分母**：OpenCodeReview 综合 / Go +206，v1.13.9 新增 excluded coverage、零 finding warnings 和工具声明修复，原位更新 9 月旧页。[解读](../../projects/open-code-review/README.md)
- **本地剪辑要区分技术 QA 与内容验收**：ffmpeg-skill Python +224，42 个工具与生成式契约有工程价值；默认 MCP 只列 12 个不限制其余调用，音频修复也不代表时轴全闭环。[解读](../../projects/ffmpeg-skill/README.md)
- **翻译量化须核真实后端**：Hy-MT2 Python +49，旧模型首次建档；1.25-bit 内核 PR 仍未合并，权重大小、内存和翻译质量分别验证。[解读](../../projects/Hy-MT2/README.md)
- **记忆可携带，权限仍随客户端变化**：AvenoxBeyin Python +46，v3.13.0 增加可选交接 / Web；本地 Markdown、模型出口、global hook 与 Desktop 自动注入分开看。[解读](../../projects/avenoxbeyin/README.md)

## GitHub 热点项目

日增取指定官方 daily 页；API 数为 stars / forks / open issues（含 PR）。“新增”指本仓库首次建档，非刚发布；语言榜不等于全站排名。

| 项目与动作 | 可核热度与版本 | 沿用分类 | 工程关注 |
| --- | --- | --- | --- |
| [ffmpeg-skill](../../projects/ffmpeg-skill/README.md)，新增 | Python +224；5,408 / 467 / 29；[API](https://api.github.com/repos/kajisho5/ffmpeg-skill)；[v3.8.4](https://github.com/kajisho5/ffmpeg-skill/releases/tag/v3.8.4)，UTC 11-13；[npm 3.8.4](https://registry.npmjs.org/ffmpeg-skill/latest)。 | 语音、视频与多模态 | MCP 列表与权限、3.x 迁移、音轨采样与视频帧、完整视听。 |
| [Hy-MT2](../../projects/Hy-MT2/README.md)，新增 | Python +49；1,749 / 185 / 14；[API](https://api.github.com/repos/Tencent-Hunyuan/Hy-MT2)；release 列表为空；README 模型发布日期 05-21。 | 模型、训练与推理基础设施 | STQ 未合并、模型 / 数据双许可、judge 出口与已评分分母。 |
| [avenoxbeyin](../../projects/avenoxbeyin/README.md)，新增 | Python +46；445 / 75 / 38；[API](https://api.github.com/repos/avenoxai/avenoxbeyin)；[v3.13.0](https://github.com/avenoxai/avenoxbeyin/releases/tag/v3.13.0)，UTC 11-12。 | 记忆层与个人 AI 基础设施 | 词法召回、历史 receipt、Desktop hook 缺口、全局 bridge 与本机 Web。 |
| [open-code-review](../../projects/open-code-review/README.md)，原位刷新 | 综合 / Go +206；50,388 / 3,742 / 338；[API](https://api.github.com/repos/alibaba/open-code-review)；[v1.13.9](https://github.com/alibaba/open-code-review/releases/tag/v1.13.9)，UTC 11-13；[npm 1.13.9](https://registry.npmjs.org/@alibaba-group%2Fopen-code-review/latest)。 | Coding Agents 与终端助手 | selected / failed / waived / excluded、provider / delegate、默认关闭 telemetry 与本地 raw 日志。 |

- 去重：对比目录、完整 owner/repo 与仓库 ID，三新一更，实际目录 1,027 → 1,030；已存在的 Buzz、Qwen Code、OpenBot、Plannotator 不重复建档。
- 已有热度观察：Modern Web Guidance 综合 +1,875、Codex Security +754、Sure +944、OpenBot TypeScript +799、Qwen Code +574。只记录榜单，不据此称本轮复审了这些实现。
- 取舍：Veyra-NRVideo、locally-uncensored 等仍是后续候选；未做同等深度核读，不将描述和 stars 直接转为效果结论。通用监控、网络、侧载工具不因排名高就并入 AI 核心项目。
- 官方页：[综合](https://github.com/trending?since=daily)、[Python](https://github.com/trending/python?since=daily)、[TypeScript](https://github.com/trending/typescript?since=daily)、[Rust](https://github.com/trending/rust?since=daily)、[Go](https://github.com/trending/go?since=daily)、[JavaScript](https://github.com/trending/javascript?since=daily)、[C++](https://github.com/trending/c++?since=daily)、[Swift](https://github.com/trending/swift?since=daily)、[Jupyter Notebook](https://github.com/trending/jupyter-notebook?since=daily)。

## X 观察

项目原帖证据不足：[Hy-MT2 实时搜索](https://x.com/search?q=%22Hy-MT2%22&f=live)返回 403，定向项目检索没有可核原帖，未取得今天互动量或评论分布。

可核的一方背景材料是 X 工程博客 [Rebuilding the global town square from scratch](https://blog.x.com/en/engineering/rebuilding-the-global-town-square-from-scratch)，页面日期 **2026-11-04**，作者 Principal Engineer Yagiz Nizipli。文章介绍少量工程师配合 coding agents、统一 AGENTS.md、仓库 skills、lint / typecheck / review 和浏览器核验来推进 Web 重建。它是历史工程自述，非今日上榜项目背书，也不是平台帖子热度。

- 讨论线索：可复用旧系统行为作为规格，配合确定性规则和人工验收，与今天 OCR 的“流程覆盖不等于语义正确”有工程关联；这是本日报的分析。
- 证据边界：团队效率和性能来自作者特定迁移与测量条件，不能推出所有团队都可复制。博客回链的[作者账号](https://x.com/yagiznizipli)同样返回 403，不能声称已读原帖或评论、获得 Views。

## Instagram 观察

- [aiagents 标签](https://www.instagram.com/explore/tags/aiagents/)跳转 popular 聚合，标题约 129K reels；这是宽泛话题数量，不能归给今日三个新项目或推算当日增长。
- [machinetranslation 标签](https://www.instagram.com/explore/tags/machinetranslation/)网页工具限流；定向 AvenoxBeyin 检索无结果，没有核实项目账号身份、具体原帖、日期或互动量。
- 因此本轮仅保留观察入口，不给 Instagram 项目排名、传播规模或评论共识；未登录、采集账号资料或发布。

## YouTube 观察

两条相关第三方视频的原生搜索卡片与 oEmbed 标题 / 作者相符。仅核元数据，没有完整观看或统计评论。

| 视频 | 可核元数据 | 讨论与边界 |
| --- | --- | --- |
| [Hy-MT2 Simplified](https://www.youtube.com/watch?v=aoiKkXtkMBM) | Omar Kamal；[Hy-MT2 原生搜索](https://www.youtube.com/results?search_query=Hy-MT2)为 775 views、5mo ago、13:32；[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=aoiKkXtkMBM&format=json)标题 / 作者一致。 | 历史第三方讲解；不能替代模型、低比特后端或翻译评测复现。 |
| [ffmpeg-skill Explained: Is It Right for You?](https://www.youtube.com/watch?v=mdQnvzfd2Zg) | Tech On Cue；[ffmpeg-skill 原生搜索](https://www.youtube.com/results?search_query=ffmpeg-skill)为 212 views、8d ago、3:25；[oEmbed](https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=mdQnvzfd2Zg&format=json)标题 / 作者一致。 | 选型解读，不是本轮执行证据；当前 42 工具与 3.8.4 边界须回源码。 |

watch 页经网页工具读取均限流，原生搜索与 oEmbed 经直接 HTTP 成功；各自证据分开记录。播放为累计值，相对年龄不反推精确发布日期，不与 GitHub 日增合并排名。搜索也有通用 FFmpeg 和旧 HY-MT1.5 内容，未计入项目热度。

## 讨论与争议：事实、判断和待验证

下表以文档与源码提出工程问题，不包装成已统计的社媒争论。

| 议题 | 已核事实 | 判断 / 接续 |
| --- | --- | --- |
| 审查覆盖与低噪声 | OCR 新发行记录 excluded、warnings；manifest 单列 failed / waived；README 承认较低 recall。 | 无评论与无漏洞分开；同报覆盖、误报、漏报及总费用。 |
| 本地剪辑与权限 | MCP 默认列 12 个但全 42 个仍可调用；verified 有未测属性边界。 | 精简 schema 不能充当授权；完整观看 / 听评和素材权利独立验收。 |
| 量化体积与可运行性 | Hy-MT2 文档指向仍 open 的 STQ PR；440 MB 是作者权重体积主张。 | 固定实际实现测 RAM、KV、时延与质量，避免按参数或文件大小选机器。 |
| 评测平均数与失败分母 | IFMTBench 对缺失输出不计平均，多约束略过缺失维度，judge 可走远端。 | 同报 total / scored 与逐维缺失；规则调试分不冒充完整评测。 |
| 本地记忆与客户端交付 | Avenox 文档区分显式检索、CLI hook 和未闭环的 Desktop 自动注入；Web 承认同机跨端口 cookie 信任面。 | 来源正确、权限过滤、注入交付和 Agent 工作声明分别验收。 |
| 遥测与调试正文 | OCR telemetry 默认关闭且不导出 prompt；本地会话和可选 raw body 日志另存。 | 网络出口、路径元数据与本机正文日志各自治理，不靠一个 content flag 统称隐私。 |

## 验证范围与接续

- 本轮来源：九页官方 daily；四个唯一仓库 ID、固定主线 SHA、完整目录树与发行；27 个固定 SHA 引用文件；两个 npm latest、两个官方权重元数据及 STQ PR 状态。未对整仓每个文件作审计。
- 文档检查：四页 28 个固定章节、四个唯一 ID、首页四类入口、1,030 个实际目录和 330 个本地链接通过；67 个范围内外部链接均对应已读来源或上述明确访问边界，其中 27 个固定 SHA 文件已获取并核读相关段落。7 个变更 Markdown 文件 lint 为零问题，diff 空白检查通过；未将受限入口算作完整原帖核验。
- 接续优先：翻译后端 / 完整评分分母；FFmpeg 采样与帧、MCP 权限 / 真实视听；记忆 Desktop hook / bridge / Web；OCR coverage / tools / 原始日志。
- 未执行：安装上游、模型或付费 API 调用、下载权重、处理媒体、修改用户 hooks、启动 Web / MCP、发布评论、权限 / 性能 / 验签实验、完整视频或评论审阅。保留用户既有 AGENTS.md 修改。
