# 2026-07-13 AI 热点日报

<!-- markdownlint-disable MD013 -->

抓取时间：2026-07-13 Asia/Shanghai  
范围：GitHub、X、Instagram、YouTube、官方博客与主流技术媒体。  
说明：GitHub stars 来自 GitHub API 抓取；X / Instagram 的原生互动计数仍受登录、地区和反爬限制影响，本日报优先记录可复核链接和讨论方向，不写不可验证的统一互动数。

## 摘要

今天的 GitHub 新增建档重点是 agent 的“长期可维护性”：本地可治理记忆、从历史日志提取个人工作画像、视频证据层、Git-native 上下文控制、Codex 本地环境诊断，以及把 agent loop 写成可评测方法。平台热点继续围绕 OpenAI GPT-5.6 / ChatGPT Work、Google Gemini Managed Agents、Claude Cowork 移动化和 HalluSquatting 安全风险发酵。

## GitHub 今日重点项目

| 项目 | 今日信号 | 分类 | 评价 |
| --- | --- | --- | --- |
| [`lapian-notes`](https://github.com/bkingfilm/lapian-notes) | 约 281 stars，2026-07-08 创建，MIT | 语音、视频与多模态 | 本地拉片笔记把抽帧、字幕、AI 分析包和结构化影视笔记接起来，代表垂直视频理解工具。 |
| [`exxperts`](https://github.com/EXXETA/exxperts) | 约 140 stars，EXXETA 开源，local-first memory | 记忆层与个人 AI 基础设施 | 把 AI rooms、审批式 memory 和本地文件治理组合起来，重点是“记忆需要用户批准”。 |
| [`ditto`](https://github.com/ohad6k/ditto) | 约 132 stars，Claude Code / Codex / Copilot logs | 记忆层与个人 AI 基础设施 | 从真实 coding-agent 日志挖出个人工作画像，补充手写规则文件无法覆盖的隐性偏好。 |
| [`fable-method`](https://github.com/Sahir619/fable-method) | 约 286 stars，MIT，含 eval 记录 | Agent 框架与技能生态 | 把 think / act / prove 写成技能和 judge，适合研究 agent loop 如何被验证。 |
| [`Cognitive-Core-Skills`](https://github.com/eli-labz/Cognitive-Core-Skills) | 约 275 stars，159 skill cards | Agent 框架与技能生态 | 用 taxonomy、schema 和 skill cards 定义 agent 核心能力，可做能力矩阵和评测底稿。 |
| [`watch-skill`](https://github.com/oxbshw/watch-skill) | 约 171 stars，MCP / CLI / REST，MIT | 语音、视频与多模态 | 让 agent 读取视频、录屏和会议，并把可视化工作变成带时间戳的可验证证据。 |
| [`contextvc`](https://github.com/HaochengLu/contextvc) | 约 141 stars，Apache-2.0，Rust CLI | Agent 框架与技能生态 | 把 `.context/` 作为 Git-native 上下文控制面，渲染到 AGENTS / CLAUDE / Cursor / Copilot 等规则文件。 |
| [`codex-hygiene`](https://github.com/sunflower-of-parchman/codex-hygiene) | 约 234 stars，Codex skill | Coding Agents 与终端助手 | 面向 Codex Desktop 的上下文与工具表面诊断，说明本地 agent 工作台也需要 hygiene 工具。 |

## X / 官方账号讨论

- OpenAI GPT-5.6 / ChatGPT Work：OpenAI 官方页面显示 GPT-5.6 已上线，并将 ChatGPT Work 定位为能跨应用和文件完成工作的 agent。X 官方入口发布 GPT-5.6 可用于 ChatGPT、Codex 和 API。可复核来源：<https://openai.com/index/gpt-5-6/>、<https://openai.com/index/chatgpt-for-your-most-ambitious-work/>、<https://x.com/OpenAI/status/2075271435573244008>。
- Google Managed Agents：Google Blog 近 5 天发布 Gemini API Managed Agents 更新，重点是 background execution、remote MCP server、custom function calling 和跨交互 credential refresh。可复核来源：<https://blog.google/innovation-and-ai/technology/developers-tools/expanding-managed-agents-gemini-api/>。
- Anthropic Claude Cowork：Claude 官方博客显示 Cowork 正在向 web 和 mobile rollout，媒体讨论点集中在“关上电脑后 agent 仍可继续工作”。可复核来源：<https://claude.com/blog/cowork-web-mobile>、<https://www.wired.com/story/shut-those-laptops-anthropic-puts-its-claude-cowork-agent-on-your-phone/>。
- HalluSquatting：安全媒体继续讨论 agent 幻觉仓库、包名或 URL 后被攻击者抢注并诱导执行的问题。可复核来源：<https://www.tomshardware.com/tech-industry/cyber-security/hallusquatting-is-the-latest-agentic-ai-exploit-where-models-dream-up-potentially-malicious-urls-in-tool-calls-attack-exploits-a-fundamental-weakness-in-every-available-model>、<https://thehackernews.com/2026/07/new-hallusquatting-attack-could-trick.html>。

## Instagram / 短内容热点

- Google for Startups 继续传播 AI Agents Challenge，说明 agent 主题已经从开发者社区进入创业传播语境。公开入口：<https://www.instagram.com/p/Daih4N5n4N_/>。
- GPT-5.6、Gemini agent、Claude Cowork 和 HalluSquatting 继续被短内容账号打包成“本周 AI 新闻”。公开入口示例：<https://www.instagram.com/p/Dak-Y6Xk9re/>。
- 今日判断：Instagram 的强信号不是单条互动数，而是多个账号把同一组平台发布和安全风险复述给非工程人群；这会推动 agent 从技术工具叙事转向岗位、创业和工作流叙事。

## YouTube 热议

- OpenAI ChatGPT Work / GPT-5.6 官方视频成为模型与工作流合并的主要传播入口：<https://www.youtube.com/watch?v=Wq45rvPGNHs>。
- Google Gemini Managed Agents / Interactions API 的开发者视频继续解释后台执行、远程 MCP 和托管 agent harness：<https://www.youtube.com/watch?v=d9LAQWKUnx8>。
- ditto 的短视频把“从 Claude Code / Codex 日志生成本地 you.md”作为 agent personalization 话题传播：<https://www.youtube.com/shorts/SgMgDwYLe4c>。

## 今日判断

1. 开源侧从“更多 agent”转向“agent 如何长期保持可审计、可记忆、可验证”：`exxperts`、`ditto`、`contextvc`、`codex-hygiene` 都在处理这个问题。
2. 多模态热点不只在生成视频，也在“视频作为证据”：`watch-skill` 和 `lapian-notes` 都把视频拆成可回看、可引用、可编辑的结构化材料。
3. 平台侧的竞争点是后台执行和跨设备入口：OpenAI ChatGPT Work、Google Managed Agents、Claude Cowork 都在把 agent 从 CLI 推向通用工作环境。
4. HalluSquatting 强化了今天新增项目的安全价值：agent 在读取外部资源、生成规则文件、安装 skill 或调用工具前，必须验证来源和权限。

## 今日新增项目页

- [`projects/lapian-notes/README.md`](../../projects/lapian-notes/README.md)
- [`projects/exxperts/README.md`](../../projects/exxperts/README.md)
- [`projects/ditto/README.md`](../../projects/ditto/README.md)
- [`projects/fable-method/README.md`](../../projects/fable-method/README.md)
- [`projects/Cognitive-Core-Skills/README.md`](../../projects/Cognitive-Core-Skills/README.md)
- [`projects/watch-skill/README.md`](../../projects/watch-skill/README.md)
- [`projects/contextvc/README.md`](../../projects/contextvc/README.md)
- [`projects/codex-hygiene/README.md`](../../projects/codex-hygiene/README.md)

## 后续跟踪

- 观察 `exxperts` 的 approval-gated memory 是否能在真实长期项目里保持可审计。
- 跟踪 `ditto` 的日志脱敏、profile 分层和跨工具适配是否稳定。
- 比较 `contextvc` 与手写 `AGENTS.md` / `CLAUDE.md` / Cursor rules 的同步成本。
- 观察 `watch-skill` 是否能成为 agent UI 验收、视频证据和录屏复盘的通用层。
- 跟踪 `codex-hygiene` 是否随 Codex Desktop 本地数据库和插件结构变化持续维护。
