<!-- markdownlint-disable MD013 -->

# 2026-08-09 AI 热点日报

> 抓取时间：2026-08-09（Asia/Shanghai）。创建时间、stars、forks 与许可证来自 GitHub REST API 快照，之后会变化。下表项目均创建于 2026-08-08，是早期开发者信号，不代表 GitHub 全站 Trending 或生产成熟度。X、Instagram、YouTube 的搜索与时间线受登录、索引和动态加载影响，未独立复核的互动量不填写。

## 今日判断

- 今日新增项目的共同方向是把 agent 能力纳入更严格的边界：KADATH 将优化对象与评分内核分离；Unreal MCP 和 Cove 将工具访问限定在本地工程或显式媒体路径；科研证据审计与中文写作 skill 则试图控制主张类型和文本改写损耗。
- KADATH 的首日约 145 stars 高于其余候选，但仅反映短期收藏信号。每个项目均仍须做本地复现、供应链和权限审计，尤其不要将模型输出、自动改写或 agent 评分直接视为研究、工程或发布结论。

## GitHub 热点项目

| 项目 | 可核验信号 | 分类 | 评价 |
| --- | --- | --- | --- |
| [`KADATH`](../../projects/KADATH/README.md) | 08-08 创建；约 145 stars、1 fork；Apache-2.0。 | Agent 框架与技能生态 | 将种群进化、独立评分和冻结证据组合为 agent runtime；模型成本、基准正确性和外部能力需先受控。 |
| [`unreal-mcp`](../../projects/unreal-mcp/README.md) | 08-08 创建；约 23 stars、0 forks；MIT。 | Agent 框架与技能生态 | 以增量索引和细粒度 Blueprint 操作降低上下文成本；所有写操作都应在副本工程人工验收。 |
| [`research-evidence-agent`](../../projects/research-evidence-agent/README.md) | 08-08 创建；约 20 stars、1 fork；BSD-3-Clause。 | RAG、检索与知识处理 | 用 manifest 和 claim ledger 抑制科研证据类型混淆；不能证明实验或论文结论正确。 |
| [`Cove Sensory MCP`](../../projects/cove-sensory-mcp/README.md) | 08-08 创建；约 15 stars、4 forks；Apache-2.0。 | 语音、视频与多模态 | 本地 MCP 以授权目录和 provider 能力提供媒体感知；被选云端 provider 仍会接触媒体。 |
| [`remove-chinese-ai-tics`](../../projects/remove-chinese-ai-tics/README.md) | 08-08 创建；约 13 stars、2 forks；MIT。 | Agent 框架与技能生态 | 将中文去模板化做成可模式化 skill；beta 规则和语义损耗必须用真实稿件回归。 |

候选来自 [08-08 创建的 AI/agent/LLM/MCP 仓库 API 搜索](https://api.github.com/search/repositories?q=created%3A2026-08-08+%28agent+OR+ai+OR+llm+OR+mcp%29&sort=stars&order=desc&per_page=100)、各项目 README 与 [GitHub Trending](https://github.com/trending) 观察入口。已排除搜索结果中的游戏脚本/瞄准类噪声和未能与 AI 工具主题相符的项目；不把短期 star 或搜索结果视为安全、可信或长期采用证明。

## X、Instagram 与 YouTube 观察

| 平台 | 可追溯入口与状态 | 本轮可得信号 | 讨论与边界 |
| --- | --- | --- | --- |
| X | [KADATH 搜索入口](https://x.com/search?q=KADATH%20agent&src=typed_query)；搜索结果受登录与动态加载影响。 | 本轮没有取得可独立核验的原帖时间或互动量。 | 不将 GitHub stars 归因于 X，也不写“X 热传”结论。 |
| Instagram | [AI agents 标签入口](https://www.instagram.com/explore/tags/aiagents/)；公开标签搜索。 | 未独立核验与上述项目对应的当日贴文或互动量。 | 泛 AI 内容不能代替项目级传播证据。 |
| YouTube | [KADATH 搜索入口](https://www.youtube.com/results?search_query=KADATH+evolutionary+agents)；可作为演示观察入口。 | 未独立核验当天发布或观看数据。 | 不将 README 的演示或自述视为 YouTube 平台热度。 |
| GitHub | [Trending](https://github.com/trending) 与上述 API 查询。 | 五个候选首日约 13--145 stars；创建日期、fork 与许可证均可由 API 复查。 | 这是本轮唯一量化的项目级发现信号，且仍是小样本早期观察。 |

## 后续跟踪

- 对 KADATH 用无敏感的确定性 benchmark 验证评分锁定、容器隔离、成本上限与证据冻结；不要先接入生产工具和凭据。
- 对 Unreal MCP 在副本 UE 项目做只读索引与可撤销写入的完整回归，审查 TCP 监听范围和插件版本匹配。
- 对 Cove 逐 provider 审阅数据条款，只开放测试目录；对 research-evidence-agent 和中文 skill 分别用公开 evidence bundle 与人工标注稿做误报、漏报和语义保持测试。
