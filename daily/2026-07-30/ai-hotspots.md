<!-- markdownlint-disable MD013 -->

# 2026-07-30 AI 热点日报

> 抓取时间：2026-07-30（Asia/Shanghai）。项目创建时间、stars、forks 和许可证来自 GitHub REST API 快照及项目原始 README；数值会持续变化。下表项目均创建于 07-29，属于“早期开发者信号”，并不代表 GitHub 全站 Trending 或生产成熟度。社媒页面可访问性与帖文排序受登录、地区和时间线影响；未独立复核的互动量一律不填写。

## 今日判断

- 07-29 的新项目呈现“把 AI 接进具体工作入口”的分化：设计规则、个人反思、文献核验、品牌可见性和科研配图，分别把 agent 能力压进不同的工作流边界。
- 最需要避免的共同误读是把“模型参与”当作可靠性背书：节律可造成敏感推断，文献工具不能替代原文判读，GEO 采样不能证明增长，科研图也不能替代数据与版权审查。

## GitHub 热点项目

| 项目 | 可核验信号 | 分类 | 评价 |
| --- | --- | --- | --- |
| [`ai-design-skills`](../../projects/ai-design-skills/README.md) | 07-29 创建；约 154 stars、9 forks；MIT。 | Agent 框架与技能生态 | 用 Markdown 设计规则约束 coding agent；应与组件库和视觉/无障碍测试配套。 |
| [`fingertips`](../../projects/fingertips/README.md) | 07-29 创建；约 47 stars、6 forks；MIT。 | 前端、UI 与 Agent 交互层 | 仅收输入节律而非内容的 companion 信号层；仍需严肃对待行为隐私与误触发。 |
| [`zhixin-companion`](../../projects/zhixin-companion/README.md) | 07-29 创建；约 39 stars、5 forks；CC BY-NC-SA 4.0（source-available）。 | 记忆层与个人 AI 基础设施 | 为个人复盘提供事实/感受/解释的分层框架；不能替代心理健康或其他专业服务。 |
| [`lit-review-skill`](../../projects/lit-review-skill/README.md) | 07-29 创建；约 15 stars；MIT。 | Agent 框架与技能生态 | 用多源 API 与证据等级做引文审计；关键主张仍要人工查全文和出版方记录。 |
| [`geolook`](../../projects/geolook/README.md) | 07-29 创建；约 14 stars、8 forks；MIT。 | 办公、商业与行业应用 | 把 GEO 拆成采样、诊断、工单和验收；不能从短期样本推断品牌长期收益。 |
| [`dreampaper`](../../projects/dreampaper/README.md) | 07-29 创建；约 8 stars、1 fork；API 未声明 SPDX 许可证。 | 办公、商业与行业应用 | 本地模板驱动的科研图/幻灯片生成；数据正确性、素材授权和最终审稿不可省略。 |

GitHub 的当天 [Trending 页面](https://github.com/trending) 可复核到 `airi`、`aisuite`、`ECC`、`speech-to-speech`、`claude-video` 等已有收录方向；本轮新建页改以 [07-29 创建的 AI/agent/LLM 仓库 API 搜索](https://api.github.com/search/repositories?q=%28agent%20OR%20llm%20OR%20ai%29%20created%3A2026-07-29&sort=stars&order=desc&per_page=100) 及逐仓库元数据为准，因此不把它们误写为 Trending 固定名次。

## X、Instagram 与 YouTube 观察

| 平台 | 可追溯入口与状态 | 本轮可得信号 | 讨论与边界 |
| --- | --- | --- | --- |
| X | [OpenAI 官方账号](https://x.com/OpenAI)；页面可打开，完整时间线读取受登录与动态加载影响。 | 适合作为模型、开发者产品和 agent 发布的官方原帖入口。 | 本轮未独立确认与上表六个 07-29 新仓库直接相关的作者/官方单帖；不将通用账号活跃度转写为项目热度。 |
| Instagram | [OpenAI 官方账号](https://www.instagram.com/openai/)；页面入口可打开，排序和完整贴文通常受登录影响。 | 适合观察面向公众的多模态产品展示与创作叙事。 | 未能独立复核日榜或与这六个项目的传播链，不填写互动数，也不做“Instagram 热传”结论。 |
| YouTube | [OpenAI 官方频道](https://www.youtube.com/@OpenAI)；频道入口可打开。 | 适合追踪产品演示、开发者讲解和长视频材料。 | 未检索到可直接归因于六个新仓库的当天官方视频；频道内容不能替代项目维护者证据。 |
| GitHub | [Trending](https://github.com/trending)；直接可打开。 | 页面当日仍集中于 agent、语音与视频工具，含已有条目 `airi`、`ECC`、`claude-video`。 | Trending 是随时变化的社区探索页，不能反推出新仓库固定名次或长期采用。 |

## 后续跟踪

- 将 `ai-design-skills` 与设计 token、组件库和视觉回归测试配对，检验生成页面的无障碍与移动端质量。
- 为 `fingertips` 设计 opt-in、最小保留、删除与关闭机制，再评估节律摘要的误触发和用户感受。
- 对 `zhixin-companion` 测试私密记录的本地忽略、备份、导出和危机转介文案，不把反思工具包装成诊断系统。
- 用一组已知正确/错误/撤稿/付费墙引用回归 `lit-review-skill`，分别记录书目、主张支持和全文可得性的错误率。
- 对 `geolook` 预注册问题、模型版本、地区和采样窗口，并保留原始回答；严禁用自动生成内容绕过事实核验。
- 为 `dreampaper` 建立可编辑草图到人工终稿的审稿链，逐项核验原始数据、比例尺、引用、模板和图源许可。
