<!-- markdownlint-disable MD013 -->

# 2026-07-07 AI 热点

## 今日摘要

今天 GitHub Trending 的 AI 相关热点明显集中在三条线：

1. **agent skill 与提示词透明度**：`system_prompts_leaks`、`agent-skills`、`claude-skills`、`last30days-skill` 继续说明“可安装能力包”和“系统层约束”正在成为 agent 生态的新分发对象。
2. **跨 agent 协作与会话管理**：`codex-plugin-cc`、`herdr`、`gastown` 把 Codex、Claude Code、Copilot、Gemini 等工具放进同一工作流或同一 workspace。
3. **多模态办公入口**：`claude-video` 和 `meetily` 分别覆盖视频理解 skill 与本地会议记录，说明“视频/会议资料可被 agent 直接处理”正在从 demo 进入可安装工具。

## GitHub 热点

### 1. system_prompts_leaks：系统提示词从猎奇资料变成 agent 架构样本

- 出处：<https://github.com/asgeirtj/system_prompts_leaks>
- 热度信号：GitHub Trending 今日头部；GitHub API 抓取时约 51k stars、8.3k forks；README 列出 Claude Sonnet 5、Claude Design、GitHub Copilot macOS、GPT-5.5 Codex 等近期更新项。
- 讨论点：当 agent 产品暴露 shell、浏览器、文件系统、skills、MCP 和长期记忆时，系统提示词记录的是产品真实边界、工具说明和安全策略。
- 评价：适合作为研究材料和 agent harness 设计参考，但不能把社区捕获文本直接当成厂商当前线上实现。
- 今日动作：新增 [`projects/system_prompts_leaks/README.md`](../../projects/system_prompts_leaks/README.md)。

### 2. codex-plugin-cc：Claude Code 内调用 Codex 做审查和任务委派

- 出处：<https://github.com/openai/codex-plugin-cc>
- 热度信号：GitHub Trending 今日头部；GitHub API 抓取时约 26k stars；README 明确提供 `/codex:review`、`/codex:adversarial-review`、`/codex:rescue`、`/codex:transfer` 等命令。
- 讨论点：agent 生态开始从“单工具替代”转向“互相调用与交接”。一个主 agent 可以把审查、救援或接续任务交给另一个 agent。
- 评价：这是跨 agent 互操作的重要样本，但后台任务会消耗 Codex 额度，且第二视角审查仍需人工判断。
- 今日动作：新增 [`projects/codex-plugin-cc/README.md`](../../projects/codex-plugin-cc/README.md)。

### 3. herdr：终端原生的多 agent session 管理器

- 出处：<https://github.com/ogulcancelik/herdr>
- 热度信号：GitHub Trending 今日头部；GitHub API 抓取时约 12.8k stars；README 自述支持 Claude Code、Codex、Copilot CLI、opencode、Devin CLI、Kimi Code 等 agent 状态识别。
- 讨论点：多 agent 并行后，开发者需要的不只是 agent 本身，还需要可持久、可远程重连、能看 blocked / working / done 状态的终端层。
- 评价：比 GUI manager 更适合 SSH 和服务器环境，但状态识别不能替代测试和人工验收。
- 今日动作：新增 [`projects/herdr/README.md`](../../projects/herdr/README.md)。

### 4. claude-video：把视频变成 agent 可读取输入

- 出处：<https://github.com/bradautomates/claude-video>
- 热度信号：GitHub Trending 今日头部；GitHub API 抓取时约 4.1k stars；README 给出 Claude Code plugin 与 Agent Skills CLI 两条安装路径。
- 讨论点：项目把 `yt-dlp`、`ffmpeg`、caption、Whisper、帧抽取和 agent 图片读取串成 `/watch` 技能，适合发布会、课程、bug 录屏和社媒视频分析。
- 评价：这是多模态 agent skill 的实用样本；长视频和私密视频仍需要注意采样完整性、API 成本和授权边界。
- 今日动作：新增 [`projects/claude-video/README.md`](../../projects/claude-video/README.md)。

### 5. meetily：本地优先 AI 会议助手继续上榜

- 出处：<https://github.com/Zackriya-Solutions/meetily>
- 热度信号：GitHub Trending 今日头部；GitHub API 抓取时约 19k stars；README 强调本地转写、Ollama summary、Parakeet / Whisper 和无云处理。
- 讨论点：会议 AI 从云端 bot 进入本地/自托管路线，核心卖点是隐私、合规和数据主权。
- 评价：对敏感会议场景有价值，但录音同意、存储周期、云模型 fallback 和社区版/商业版边界仍需明确。
- 今日动作：新增 [`projects/meetily/README.md`](../../projects/meetily/README.md)。

### 6. gastown：多 agent workspace manager 走向任务治理层

- 出处：<https://github.com/gastownhall/gastown>
- 热度信号：GitHub Trending 今日头部；GitHub API 抓取时约 16.6k stars；README 用 Mayor、Rig、Polecat、Hooks、Convoy、Beads、Refinery 等概念描述多 agent 工作流。
- 讨论点：当 4 到 30 个 agent 并行时，核心问题从“让 agent 写代码”变成“如何持久化状态、分配任务、处理卡住、合并结果和留下审计轨迹”。
- 评价：概念完整但复杂度高，更适合作为高级团队和研究型工作流样本，不宜直接替代成熟 CI/CD。
- 今日动作：新增 [`projects/gastown/README.md`](../../projects/gastown/README.md)。

## X 热点

- 可复核入口：<https://x.com/search?q=Codex%20Claude%20Code%20agent%20skills&src=typed_query&f=live>
- 热度信号：公开搜索中，Codex、Claude Code、agent skills、GitHub Copilot agent 和多 agent 管理仍是高频组合词；但 X 原生互动数需要登录且动态变化，本仓库不写不可复核计数。
- 讨论点：
  - 开发者更关心 agent 的成本、额度、审查质量和是否能真正接入现有仓库。
  - agent skills 被大量包装成“给 Claude / Codex / Cursor 增加某种能力”的可安装资产。
  - 多 agent 并行管理开始从个人脚本变成专门工具。
- 争议：社媒传播常把“可安装 skill”写成“模型突然获得新能力”，需要区分宿主模型能力、外部脚本能力和用户本地权限。

## Instagram 热点

- 可复核入口 1：<https://www.instagram.com/p/DaVG2Z1gO-r/>
- 可复核入口 2：<https://www.instagram.com/p/DaQIGKjjKrj/>
- 热度信号：近期 Instagram AI 开发内容仍偏“Top GitHub repos”“GitHub 变成 AI teammate”“开源工具替代付费软件”这类短内容包装。
- 讨论点：
  - 面向大众开发者的传播重点不是架构细节，而是“哪些 repo 可以马上用”。
  - 本地会议助手、视频理解、coding agent、开源替代品更容易被短视频平台复述。
- 争议：Instagram 可见内容常缺少版本、许可证、维护状态和风险边界，因此只能作为传播热度信号，不能作为选型依据。

## YouTube 热点

- 可复核入口 1：<https://www.youtube.com/watch?v=f5OWBYcJc9o>
- 可复核入口 2：<https://www.youtube.com/watch?v=8QMKzGFaZxQ>
- 热度信号：YouTube 近期围绕“Top GitHub repositories”“AI agents taking over GitHub”“Claude Code / Codex 教程”的内容持续出现。
- 讨论点：
  - 教程内容越来越偏工作流：怎么安装、怎么省 token、怎么让 agent 处理视频/会议/代码审查。
  - GitHub 热榜解读视频会放大单日 star 增长，但通常缺少长期维护验证。
- 评价：适合发现候选项目和观察大众采用叙事，不适合直接判断项目成熟度。

## 评价与争议

- **事实层**：GitHub 今日头部 AI 项目确实集中在 skills、prompt transparency、多 agent session、多模态办公输入。
- **判断层**：agent 生态正在从“单个强 agent”走向“可安装能力 + 多 agent 协作 + 本地权限治理”。
- **不确定性**：GitHub star 增长可能受短期传播、自动化账号或话题包装影响；X / Instagram 互动指标受登录、地区和反爬限制影响，今天仍只记录可复核入口。

## 今日新增项目

- `system_prompts_leaks` -> `Agent 框架与技能生态`
- `codex-plugin-cc` -> `Coding Agents 与终端助手`
- `herdr` -> `Coding Agents 与终端助手`
- `claude-video` -> `语音、视频与多模态`
- `meetily` -> `办公、商业与行业应用`
- `gastown` -> `Agent 框架与技能生态`

## 明日跟踪建议

- 观察 `codex-plugin-cc` 是否成为 Claude Code 用户引入 Codex 审查的默认入口。
- 跟踪 `herdr` 与 `gastown` 的分工：终端 session 管理和任务治理是否会分成两个稳定层。
- 继续观察 `claude-video`、`meetily` 是否把视频/会议输入做成 agent 的日常工作流，而不是单日 demo。
- 对 `system_prompts_leaks` 保持谨慎使用：重点看产品架构线索，不把泄露文本当成官方规范。
