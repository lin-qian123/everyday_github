<!-- markdownlint-disable MD013 -->

# 2026-07-25 AI 热点日报

> 抓取时间：2026-07-25（Asia/Shanghai）。GitHub 数据来自 GitHub REST API：下列项目均创建于 2026-07-24，star/fork 为抓取时快照，并结合各项目 README 核对。它们是新项目中的早期开发者信号，不等同于 GitHub 全站 Trending 或成熟推荐。无法独立复核的社媒互动量不编造。

## 今日判断

- 今日样本的共同点不是更大规模的模型，而是把 agent 生成或协作拉回可交付界面：依赖任务板、trace debugger、可编辑科研图和演示文稿 skill 都在处理“怎么知道工作真的完成”。
- 另一条支线是把 AI 放进具体个人工作流：求职资料管理和手势驱动的人像风格化都展示了本地/远程混合运行的便利，同时也带来履历、人像、GPU 服务暴露等隐私边界。
- 这些仓库最多只上线一天；star 只能说明初始发现度，不能证明安全、模型质量、许可证适配、团队可维护性或跨平台稳定性。

## GitHub 热点项目

| 项目 | 可核验信号 | 分类 | 评价 |
| --- | --- | --- | --- |
| [`mission-control-board`](../../projects/mission-control-board/README.md) | 07-24 创建；52 stars；10 forks；MIT。 | 前端、UI 与 Agent 交互层 | 单文件任务依赖图将人/agent 责任分列；ready 是推导值，但不能替代 CI 验收。 |
| [`slide-meme-inserter`](../../projects/slide-meme-inserter/README.md) | 07-24 创建；37 stars；0 forks；MIT。 | 办公、商业与行业应用 | 为 Codex/Claude 的 HTML deck 引入受控梗图设计与审计；版权和受众判断不可自动化。 |
| [`job-search-workflow`](../../projects/job-search-workflow/README.md) | 07-24 创建；24 stars；3 forks；PolyForm Noncommercial，alpha。 | 办公、商业与行业应用 | 用本地 ledger 和提示契约组织求职；不得让 AI 虚构经历或代投。 |
| [`blinkface`](../../projects/blinkface/README.md) | 07-24 创建；21 stars；2 forks；代码 MIT。 | 语音、视频与多模态 | 手势取景 + FLUX 实时风格化有明确的同意与端口安全边界。 |
| [`capybara`](../../projects/capybara/README.md) | 07-24 创建；8 stars；0 forks；MIT。 | Agent 框架与技能生态 | 以 OTLP/会话 trace 追溯 agent 失败和成本；收集内容前必须先做脱敏。 |
| [`scientific-illustrator`](../../projects/scientific-illustrator/README.md) | 07-24 创建；8 stars；1 fork；MIT。 | 语音、视频与多模态 | 将科研图的原生对象、渲染与审查分开验证；Windows PowerPoint 是硬限制。 |

## X、Instagram 与 YouTube 观察

- X：[`blinkface` 作者的演示帖](https://x.com/Lumosous/status/2080430080371941882) 是项目 README 直接链接的手势实时预览证据。它支持“存在可演示交互”的判断，但本轮无法可靠读取实时互动量，也不据此推断受众规模或产品成熟度。
- GitHub：上述六个项目的创建时间、stars/forks、许可证和项目描述均以各自 [仓库主页](https://github.com/rockthemike712/mission-control-board) 的 REST API 返回为准；其中 `mission-control-board` 和 `slide-meme-inserter` 是本轮同日新项目中 star 较高的可读工程样本。
- Instagram：从 [OpenAI 官方账号](https://www.instagram.com/openai/) 可追踪生成式 AI 的产品与创作内容，但登录/地区限制使本轮无法独立核验 07-25 单帖的点赞、播放或发布时间，因此不将账号动态伪作日榜。
- YouTube：从 [OpenAI 官方频道](https://www.youtube.com/@OpenAI) 可进入 agent 与多模态产品演示；本轮没有找到能独立核验为当日发布且与上表直接相关的单条热门视频，故仅记录该官方入口而不列热度数字。

## 后续跟踪

- 对 `capybara` 验证多种 OTEL schema、敏感内容关闭与 replay 的离线边界，观察能否从 TUI 工具沉淀为团队回归流程。
- 对 `mission-control-board` 试验把任务完成关联到构建、测试、PR 和人工审批，而不是仅靠点选状态。
- 观察 `scientific-illustrator` 是否给出 macOS/Linux draw.io 的可重复验证，以及复杂科研图的编辑性样例。
- 对 `blinkface` 优先复核 token、反代、访问日志和同意记录；对 `job-search-workflow` 复核其 alpha 质量、许可证与敏感资料最小化策略。
