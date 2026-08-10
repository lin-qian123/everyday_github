<!-- markdownlint-disable MD013 -->

# 2026-08-11 AI 热点日报

> 抓取时间：2026-08-11（Asia/Shanghai）。创建时间、stars、forks 与许可证来自 GitHub REST API 快照，之后会变化。下表项目均创建于 2026-08-10，是早期开发者信号，不代表 GitHub 全站 Trending 或生产成熟度。X、Instagram、YouTube 的搜索、登录和动态加载限制使本轮无法独立验证同项目级的当日互动量，故不填写。

## 今日判断

- 今天较有代表性的不是“又一个通用 agent”，而是 agent 权限、网页执行、工程可审计性与专业安全工具四个执行层。`desktop-harness` 将 GUI 操作转为 AX 优先的本地能力；`moli` 则尝试把浏览器的成本模型改成 DOM 优先、像素按需。
- `AuditSentry`、`constitution` 和 `inside-coding-agents` 从专业审计、规则版本化和证据型教学三个方向强调约束与验证。前者的性能/检出率主张尚待独立复现；后两者也不能以“有规则”或“有实验”代替宿主权限隔离和真实任务验收。

## GitHub 热点项目

| 项目 | 可核验信号 | 分类 | 评价 |
| --- | --- | --- | --- |
| [`AuditSentry`](../../projects/ai-smart-contract-auditor/README.md) | 08-10 创建；约 75 stars、2 forks；MIT。 | Coding Agents 与终端助手 | 面向 Claude Code 的合约审计技能/MCP 组合，需逐项复核 PoC、基准和链上操作。 |
| [`constitution`](../../projects/constitution/README.md) | 08-10 创建；约 23 stars、1 fork；CC-BY-4.0。 | Agent 框架与技能生态 | 固定版本的 coding-agent 原则文件；应以审阅后的下游副本使用，不能替代权限控制。 |
| [`moli`](../../projects/moli/README.md) | 08-10 创建；约 15 stars、5 forks；API 未声明 SPDX。 | 前端、UI 与 Agent 交互层 | 用 Rust 构建 DOM 优先、按需渲染的 agent 浏览器；兼容性、网络和存储边界需实测。 |
| [`desktop-harness`](../../projects/desktop-harness/README.md) | 08-10 创建；约 10 stars、3 forks；MIT。 | Coding Agents 与终端助手 | macOS AX 优先的桌面控制 CLI；辅助功能权限带来高风险执行面，必须最小授权。 |
| [`inside-coding-agents`](../../projects/inside-coding-agents/README.md) | 08-10 创建；约 8 stars、0 forks；Apache-2.0。 | Agent 框架与技能生态 | 将 coding-agent 机制、证据和可重放实验组织成双语教材；不是任一产品的官方或性能认证。 |

候选来自 [08-10 创建的 AI/agent/LLM/MCP 仓库 API 搜索](https://api.github.com/search/repositories?q=created%3A2026-08-10+%28agent+OR+llm+OR+mcp+OR+rag%29&sort=stars&order=desc&per_page=50)、各项目 README 与 [GitHub Trending](https://github.com/trending) 观察入口。已按 `projects/` 去重，并排除交易机器人、游戏脚本、未能从公开材料确认 AI 工具关联的结果；短期 star 与搜索排序均不代表安全、可信或长期采用。

## X、Instagram 与 YouTube 观察

| 平台 | 可追溯入口与状态 | 本轮可得信号 | 讨论与边界 |
| --- | --- | --- | --- |
| X | [AI agent 搜索入口](https://x.com/search?q=%22AI%20agent%22&src=typed_query)；结果受登录和动态加载影响。 | 未取得能独立核验、且与上述五项目对应的当日原帖或互动量。 | 不以泛 agent 讨论或 GitHub stars 推断项目在 X 热传。 |
| Instagram | [AI agents 标签入口](https://www.instagram.com/explore/tags/aiagents/)；公开标签观察。 | 未独立核验同日且对应上述项目的贴文或互动量。 | 泛 AI 内容不能替代项目级传播证据。 |
| YouTube | [AI coding agent 搜索入口](https://www.youtube.com/results?search_query=AI+coding+agent)；演示观察入口。 | 未独立核验上述项目在当天发布的演示或观看量。 | 不将 README 示例或搜索结果等同于平台热度。 |
| GitHub | [Trending](https://github.com/trending) 与上述 API 查询。 | 五个候选创建后约 8--75 stars；创建日期、fork 与许可证可由 API 复查。 | 这是本轮唯一量化的项目级发现信号，且是早期小样本观察。 |

## 后续跟踪

- 用公开历史漏洞集、固定版本依赖和无资产 fork 独立核验 AuditSentry 的发现、PoC 和误报；禁止其链上工具使用生产私钥或直接广播。
- 试用 `moli` 时优先测登录、cookie、上传下载、跨域、网络代理和反自动化差异；对 `desktop-harness` 限制可控应用和窗口断言，所有破坏性动作保留人工确认。
- 对 `constitution` 固定 release 后再合并规则，验证它与本地 `AGENTS.md` 的优先级；从 `inside-coding-agents` 选择确定性 lesson/trace 复跑，避免把旧 snapshot 当作产品现况。
