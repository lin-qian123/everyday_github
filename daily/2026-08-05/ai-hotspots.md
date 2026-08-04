<!-- markdownlint-disable MD013 -->

# 2026-08-05 AI 热点日报

> 抓取时间：2026-08-05（Asia/Shanghai）。创建时间、stars、forks 与许可证来自 GitHub REST API 快照，之后会变化。下表项目均创建于 2026-08-04，是早期开发者信号，不代表 GitHub 全站 Trending 或生产成熟度。X、Instagram、YouTube 的搜索与时间线受登录、索引和动态加载影响，未独立复核的互动量不填写。

## 今日判断

- 今日新仓库的共同主题是让 agent 从“能生成”走向“可持续运行”：LongHorizon-Harness 的独立审计状态、diri 的持久会话/worktree、ironcode 的证据门槛，以及 IngestReasonCreate 的回读核验，分别在不同环节抑制长任务漂移。
- 工具能力与执行边界仍须分开看。Fuxi 与 diri 都可调度 shell、MCP 或远端环境；强功能并不等于默认安全。`ai-evals` 说明评测需求正在升温，但其公开细节与许可尚不足以产生模型排名结论。

## GitHub 热点项目

| 项目 | 可核验信号 | 分类 | 评价 |
| --- | --- | --- | --- |
| [`LongHorizon-Harness`](../../projects/LongHorizon-Harness/README.md) | 08-04 创建；约 173 stars、12 forks；MIT。 | Agent 框架与技能生态 | 管理、执行、审计角色分离，突出可恢复的已验证状态；README 的 benchmark 声明尚未由本仓库独立复现。 |
| [`Fuxi`](../../projects/Fuxi/README.md) | 08-04 创建；约 81 stars、7 forks；Apache-2.0。 | Coding Agents 与终端助手 | 多 provider 路由、MCP 与持久会话集成度高；应先审查安装、自动更新、密钥和工具权限。 |
| [`diri`](../../projects/diri/README.md) | 08-04 创建；约 81 stars、2 forks；Apache-2.0。 | Coding Agents 与终端助手 | 用 macOS daemon、PTY 与 worktree 管理并发会话；状态提示不能替代 Git/测试验收，远端连接需最小权限。 |
| [`ironcode`](../../projects/ironcode/README.md) | 08-04 创建；约 11 stars、1 fork；MIT。 | Agent 框架与技能生态 | 将安全、资源、数据访问和真实验证写成 gate；适合作为审阅辅助，不替代威胁建模和人工审核。 |
| [`IngestReasonCreate`](../../projects/IngestReasonCreate/README.md) | 08-04 创建；约 4 stars、0 forks；Apache-2.0。 | RAG、检索与知识处理 | 把抽取、定位、推理、排版和回读分层，针对文档数值幻觉；OCR/表格正确性仍需人工抽检。 |
| [`ai-evals`](../../projects/ai-evals/README.md) | 08-04 创建；约 9 stars、0 forks；API 无 SPDX。 | 模型、训练与推理基础设施 | Rails 的早期评测入口；任务定义、数据许可和复现脚本不足，当前仅列入 watchlist。 |

候选来自 [08-04 创建的 AI/agent/LLM/MCP 仓库 API 搜索](https://api.github.com/search/repositories?q=created%3A2026-08-04+%28agent+OR+ai+OR+llm+OR+mcp%29+stars%3A%3E3&sort=stars&order=desc&per_page=30)、项目 README 与 [GitHub Trending](https://github.com/trending) 观察入口。首日 star 容易受到作者网络和小样本影响，因此不将它表述为固定 Trending 名次或长期采用率。

## X、Instagram 与 YouTube 观察

| 平台 | 可追溯入口与状态 | 本轮可得信号 | 讨论与边界 |
| --- | --- | --- | --- |
| X | [LongHorizon-Harness 搜索入口](https://x.com/search?q=%22LongHorizon-Harness%22&src=typed_query)；搜索结果读取受登录和动态加载影响。 | 未取得可独立核验的原帖时间或互动量。 | 不将 GitHub star 增长归因于 X，也不写“X 热传”结论。 |
| Instagram | [LongHorizon Harness 标签搜索](https://www.instagram.com/explore/tags/longhorizonharness/)；公开标签入口。 | 未独立核验对应项目贴文、日期或互动量。 | 不以无关的 agent/AI 内容替代项目层面证据。 |
| YouTube | [LongHorizon-Harness 搜索入口](https://www.youtube.com/results?search_query=LongHorizon-Harness)；可作为后续 demo 观察入口。 | README 自带演示视频链接，但本轮未独立核验 YouTube 当日发布或观看数据。 | 不将仓库内视频演示等同于平台传播热度。 |
| GitHub | [Trending](https://github.com/trending) 与上述 API 查询。 | 六个候选首日约 4--173 stars；创建日期、fork 与许可证可由 API 复查。 | 这是本轮唯一的可量化发现信号，仍是早期、小样本观察。 |

## 后续跟踪

- 对 LongHorizon-Harness 用受控任务复测其状态持久与独立审计流程，并验证失败/恢复路径；对 Fuxi 和 diri 分别审查安装脚本、日志留存、MCP/SSH 权限与并发 worktree 冲突。
- 将 ironcode 的 gate 映射到真实 CI 命令；用含表格、扫描件和敏感字段的脱敏样本检验 IngestReasonCreate 的页码、数值和外发边界。
- 等待 `ai-evals` 补齐任务、数据、许可证与可重现实验；模型选型仍应以自有样本、人工盲评、成本、延迟和安全测试为主。
