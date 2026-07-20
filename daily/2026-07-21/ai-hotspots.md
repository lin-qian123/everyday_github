<!-- markdownlint-disable MD013 -->

# 2026-07-21 AI 热点日报

> 抓取时间：2026-07-21（Asia/Shanghai）。本日报使用 GitHub API、项目 README、官方站点、公开搜索结果和可访问的 X / Instagram / YouTube 索引。X、Instagram、YouTube 的互动数受登录、地区和抓取窗口影响；未能直接复核时只写“公开索引可见”或“聚合摘录”，不编造精确指标。

## 今日判断

- GitHub 新项目从单纯 coding agent 继续外扩到 provenance、模型路由、本地推理、agent sandbox、agentic security 和视频 production skill，说明“agent 周边工程系统”仍是主线。
- `machine-genome`、`open-kritt`、`fabrica` 同日上榜，体现安全、身份、隔离和审计正在成为 agent 工程基础层，而不是后置补丁。
- 社媒侧 GPT-Red 仍是最强 AI 安全叙事；YouTube 侧继续围绕 Codex / Claude Code 真实任务比较、agent loop 纪律和 AI 视频制作工具发酵。

## GitHub 热点项目

| 项目 | 今日信号 | 分类 | 评价 |
| --- | --- | --- | --- |
| [`machine-genome`](../../projects/machine-genome/README.md) | 2026-07-20 创建；GitHub API 抓取时约 269 stars、7 forks。 | Agent 框架与技能生态 | 把模型、agent、harness、数据集和产物身份做成签名 provenance 协议，适合长期跟踪 AI 供应链。 |
| [`nativ`](../../projects/nativ/README.md) | 2026-07-20 创建；约 146 stars、9 forks；Swift / MLX macOS app。 | 模型、训练与推理基础设施 | Apple Silicon 本地模型从 runner 走向桌面工作台和 coding-tool 后端，和 `Rapid-MLX` / `ollama` 形成对照。 |
| [`codex-router`](../../projects/codex-router/README.md) | 2026-07-19 创建；约 107 stars、9 forks；围绕 Kimi / DeepSeek / Codex picker。 | Coding Agents 与终端助手 | 模型路由和成本控制进入 Codex 周边生态，但要重点审查本地配置与凭据边界。 |
| [`software-periodic-table`](../../projects/software-periodic-table/README.md) | 2026-07-19 创建；约 68 stars、4 forks；115 个软件元素 ontology。 | Agent 框架与技能生态 | 把业务应用生成从 prompt 经验转向可检索元素组合，是值得观察的 agent composition 方法。 |
| [`video-shotcraft`](../../projects/video-shotcraft/README.md) | 2026-07-19 创建；约 41 stars、4 forks；Remotion + Codex / Claude skill。 | 语音、视频与多模态 | 代表 agent-native 视频生产链路，把镜头语言和动效参数做成 skill / recipe 库。 |
| [`open-kritt`](../../projects/open-kritt/README.md) | 2026-07-20 创建；约 36 stars、11 forks；AGPL security scanner。 | Agent 框架与技能生态 | AI 安全扫描从报告生成走向容器执行、PoC 验证和 workflow 编排；双重用途风险高。 |
| [`fabrica`](../../projects/fabrica/README.md) | 2026-07-19 创建；约 35 stars、7 forks；Kata / Cloud Hypervisor agent sandbox。 | Agent 框架与技能生态 | agent execution sandbox 继续升温，microVM 隔离比普通容器更适合不可信代码任务。 |
| [`graphkit`](../../projects/graphkit/README.md) | 2026-07-19 创建；约 23 stars、1 fork；Claude Code graph engineering skill。 | Agent 框架与技能生态 | 用 executor / supervisor / ledger 文件把长任务拆成小图，补足单 loop 漂移问题。 |

## X 热点

### GPT-Red 与 AI 安全自动红队继续扩散

- 出处：OpenAI X 帖 <https://x.com/OpenAI/status/2077446719990796505>，官方文章 <https://openai.com/index/unlocking-self-improvement-gpt-red/>。
- 热度信号：公开搜索在 7 月 16-21 日持续返回 OpenAI、AI 新闻账号、安全从业者和短视频二创围绕 GPT-Red 的讨论。
- 讨论点：自动红队、自博弈强化学习、prompt injection、agent 数据外泄和现实系统漏洞测试。
- 评价：与 GitHub 上 `open-kritt`、`conversation-steganography`、`machine-genome` 的同日热度相互呼应，说明 agent 安全从模型对齐扩展到运行环境和供应链。
- 争议：官方评测之外的第三方复现有限；自动红队能力也可能降低攻击门槛。

### Codex 周边模型路由与本地后端升温

- 出处：GitHub `codex-router` <https://github.com/duolahypercho/codex-router>、`nativ` <https://github.com/Blaizzy/nativ>，以及 X / YouTube 上围绕 Codex、Claude Code、Kimi、DeepSeek 的工具流讨论。
- 热度信号：近两天新仓库直接把 Codex、Kimi、DeepSeek、MLX、本地 server、model picker 写入项目定位。
- 讨论点：用户希望保留 Codex workflow，同时更灵活地选择模型、降低成本或使用本地推理。
- 评价：这不是单个模型胜负，而是“agent host + router + local backend”的组合式工作流。
- 争议：路由器和本地服务会触碰凭据、配置和模型调用日志，安全边界必须优先于便利性。

## Instagram 热点

### GPT-Red 被二次传播为“AI 黑客 / AI 防御”故事

- 出处：OpenAI Instagram reel <https://www.instagram.com/reel/Da2_pMcpu21/>；公开索引显示其 2026-07-16 发布，约 2265 likes、57 comments。另有聚合账号贴文如 <https://www.instagram.com/reel/DbA771WxAgz/>、<https://www.instagram.com/reel/Da8HsWmkvXz/>。
- 热度信号：公开搜索继续出现“OpenAI GPT-Red”“AI super-hacker”“prompt injection”短视频标题。
- 讨论点：大众传播更关注“AI 自动攻击 AI 找漏洞”，技术细节如 held-out scenarios、自博弈训练和 agent tool boundary 往往被压缩。
- 评价：能把 AI 安全带给更广泛受众，但也容易把复杂红队流程简化成单一超级模型故事。
- 争议：二创内容经常缺少实验设置、模型版本和失败案例，证据等级低于官方文章与论文/报告。

### AI 视频制作工作流继续吸引创作者

- 出处：`video-shotcraft` Gallery <https://vincentwei1021.github.io/video-shotcraft/>，YouTube 示例 <https://youtu.be/gcVvRM_P3SM>，公开 Instagram AI video trends 聚合页 <https://www.instagram.com/popular/ai-video-trends-2026/>。
- 热度信号：社媒仍持续出现 AI video generator、product promo、motion design、Sora / Veo / Runway / Kling 对比内容。
- 讨论点：创作者关心可控镜头、真实产品截图、字幕、音效、品牌一致性和可商用交付，而不是只看端到端生成模型。
- 评价：`video-shotcraft` 这类 skill 说明“AI 视频”正在拆分成模型生成、代码化动效、剪辑工具和 agent QA 多层。
- 争议：榜单和短视频容易混入广告、联盟导流和不可复核样例。

## YouTube 热点

### Codex vs Claude Code 的真实任务比较继续延伸

- 出处：YouTube “Codex vs Claude Code: Live AI SDR Build” <https://www.youtube.com/watch?v=4asYu8HDaTs>，“Claude Code vs Codex : A realistic comparison” <https://www.youtube.com/watch?v=sj-QxjZjcV0>。
- 热度信号：公开搜索显示近一个月仍有围绕 Codex、Claude Code、Definition of Done、项目管理 demo、SDR 自动化的实测视频。
- 讨论点：创作者开始比较端到端任务完成、后端选择、自动化安全评估、代码质量、成本和时间，而不是只做“谁会写函数”的短 demo。
- 评价：和 `graphkit`、`software-periodic-table`、`fabrica` 的 GitHub 热点一致，agent 工程正在转向任务定义、执行隔离、验收和可复用结构。
- 争议：单个视频任务样本小，结论容易受作者熟悉度、prompt、模型版本和工具配置影响。

### AI 视频工具从模型榜单走向 production stack

- 出处：`video-shotcraft` YouTube 示例 <https://youtu.be/gcVvRM_P3SM>，公开搜索中的 2026 AI video generator 横评和工作流视频。
- 热度信号：AI video ranking、product demo、cinematic promo、Remotion / agent skill 相关内容继续出现。
- 讨论点：视频创作者不仅需要“生成一段画面”，还需要镜头库、动效模板、音效、字幕、可编辑工程和最终渲染。
- 评价：agent-native 视频生产会更像软件工程 pipeline，而不是单一模型调用。
- 争议：开源工具的可复现性强于闭源模型榜单，但最终视觉质量和版权风险仍要人工把关。

## 今日新增项目归档

- `projects/machine-genome/README.md`
- `projects/nativ/README.md`
- `projects/codex-router/README.md`
- `projects/software-periodic-table/README.md`
- `projects/open-kritt/README.md`
- `projects/video-shotcraft/README.md`
- `projects/fabrica/README.md`
- `projects/graphkit/README.md`

## 后续跟踪

- 跟踪 `machine-genome` 是否出现真实 registry 使用和第三方 attestations。
- 观察 `nativ` 是否稳定发布 macOS app，并验证 OpenAI / Anthropic-compatible endpoint 对 Codex / Claude Code 的兼容性。
- 审查 `codex-router` 的配置迁移、rollback、凭据文件权限和 provider 生命周期。
- 跟踪 `open-kritt` 的 threat model、误报率、PoC 验证质量和隔离建议是否完善。
- 横向比较 `fabrica`、`clawk`、`tupper`、`OpenSandbox` 的隔离模型、部署成本和凭据边界。
- 观察 `graphkit` 是否从 Claude Code skill 扩展到 Codex / OpenCode 等多 runtime。
