<!-- markdownlint-disable MD013 -->

# 2026-07-08 AI 热点

## 今日摘要

今天的 GitHub 与社媒信号继续沿着昨天的 agent 生态扩散，但重点从“单个新工具”进一步转向“能力包、委派层和个人 agent 基础设施”：

1. **跨 agent 委派成为真实工作流**：`claude-antigravity-agents` 把 Claude Code 变成主协调者，把长审查和研究任务委派给 Google Antigravity CLI。
2. **系统提示词和 skills 目录继续升温**：`system-prompts-and-models-of-ai-tools`、`awesome-claude-code`、`antigravity-awesome-skills` 说明开发者正在把 prompt、skill、subagent 和插件当成可管理资产。
3. **agent 从 coding CLI 扩展到个人工作台**：`nanobot` 把 WebUI、聊天渠道、MCP、记忆、自动化和模型路由放进轻量个人 agent 内核。

## GitHub 热点

### 1. claude-antigravity-agents：Claude Code 委派 Antigravity 子 agent

- 出处：<https://github.com/markfulton/claude-antigravity-agents>
- 热度信号：2026-07-07 新建仓库，GitHub API 抓取时约 70 stars、22 forks；README 明确提供 `agy -p "<task>"` 后台委派、只读 sandbox、隔离 worktree 和验证流程。
- 讨论点：coding agent 的竞争正在从“谁单独完成任务”走向“谁能调度其他 agent 和其他模型完成可分离任务”。
- 评价：作为模式样本很有价值，但项目很新，适合先用于只读审查和第二意见，不应直接交给生产写入任务。
- 今日动作：新增 [`projects/claude-antigravity-agents/README.md`](../../projects/claude-antigravity-agents/README.md)。

### 2. system-prompts-and-models-of-ai-tools：系统提示词透明度热度继续扩大

- 出处：<https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools>
- 热度信号：GitHub API 抓取时约 141k stars、34k forks；README 描述覆盖 Claude Code、Cursor、Devin、Lovable、Manus、Perplexity、Replit、v0、Windsurf、VS Code Agent 等产品。
- 讨论点：开发者想研究 agent 产品如何描述工具、权限、记忆、shell、浏览器和安全边界。
- 评价：适合做 agent harness 研究参考，但社区捕获文本不能等同官方当前规范。
- 今日动作：新增 [`projects/system-prompts-and-models-of-ai-tools/README.md`](../../projects/system-prompts-and-models-of-ai-tools/README.md)。

### 3. ui-ux-pro-max-skill：UI/UX 设计判断被封装成 agent skill

- 出处：<https://github.com/nextlevelbuilder/ui-ux-pro-max-skill>
- 热度信号：GitHub API 抓取时约 102k stars、10k forks；README 标注 161 条 reasoning rules、67 种 UI styles，并提供 npm CLI。
- 讨论点：前端 agent 的短板不只是写 React，而是能否根据行业、品牌和用户目标生成合适的设计系统，并避免常见 AI UI 反模式。
- 评价：适合作为设计检查清单和设计系统初稿来源，但不能替代真实设计评审。
- 今日动作：新增 [`projects/ui-ux-pro-max-skill/README.md`](../../projects/ui-ux-pro-max-skill/README.md)。

### 4. oh-my-openagent：复杂代码库中的低 token agent harness

- 出处：<https://github.com/code-yeongyu/oh-my-openagent>
- 热度信号：GitHub API 抓取时约 65k stars、5.3k forks；项目描述强调 Codex / OpenCode 生态和 tokenmaxxers。
- 讨论点：大代码库场景下，agent harness 的核心竞争点正在变成上下文选择、压缩、任务编排和交互控制。
- 评价：值得跟踪，但需要真实仓库任务验证其 token 节省和安全边界。
- 今日动作：新增 [`projects/oh-my-openagent/README.md`](../../projects/oh-my-openagent/README.md)。

### 5. awesome-claude-code：Claude Code 生态目录成为选型入口

- 出处：<https://github.com/hesreallyhim/awesome-claude-code>
- 热度信号：GitHub API 抓取时约 49k stars、4.2k forks；topics 覆盖 agent-skills、coding-agent、AI workflow optimization 等。
- 讨论点：Claude Code 生态已经从单工具使用进入 skills、subagents、status lines、plugins、MCP 和教程的目录化阶段。
- 评价：适合作为资源雷达，但 awesome list 本身不是安全审计或质量背书。
- 今日动作：新增 [`projects/awesome-claude-code/README.md`](../../projects/awesome-claude-code/README.md)。

### 6. nanobot：轻量个人 agent kernel 持续活跃

- 出处：<https://github.com/HKUDS/nanobot>
- 热度信号：GitHub API 抓取时约 45k stars、7.9k forks；README 显示 2026-06-22 v0.2.2 发布，覆盖 WebUI transcript、Python SDK runtime controls、automation management、搜索 / STT provider 和 gateway 稳定性。
- 讨论点：个人 AI 基础设施不再只是记忆层，还包括聊天渠道、工具、MCP、自动化、模型路由和部署。
- 评价：适合长期跟踪，但多渠道和多工具权限需要严格最小化配置。
- 今日动作：新增 [`projects/nanobot/README.md`](../../projects/nanobot/README.md)。

## X 热点

- 可复核入口：<https://x.com/search?q=Claude%20Code%20skills%20Codex%20Antigravity%20agent&src=typed_query&f=live>
- 热度信号：公开搜索中，Claude Code、Codex、Antigravity、agent skills、system prompts、MCP 和多 agent 委派仍是高频组合词；X 原生互动数受登录和动态排序影响，本仓库不写不可复核计数。
- 讨论点：
  - 开发者开始比较 Claude Code、Codex、Antigravity、Gemini CLI、OpenCode 的角色分工，而不是只问哪个模型更强。
  - skills 被包装成“给 agent 装能力”的分发单元，热度从单仓库扩散到目录、市场和安装器。
  - 系统提示词泄露/整理仓库继续被用来研究产品边界，但也引发版权、时效和安全争议。
- 争议：社媒常把“第三方 skill 能做到”简化成“模型原生能力提升”，需要区分模型能力、宿主工具能力、本地脚本能力和用户授权范围。

## Instagram 热点

- 可复核入口 1：<https://www.instagram.com/reel/DaLF4hrz8It/>
- 可复核入口 2：<https://www.instagram.com/p/DZjXfIoDWyQ/>
- 可复核入口 3：<https://www.instagram.com/reel/DYGdrXjJxBd/>
- 热度信号：近期 Instagram AI 开发内容仍在传播 “Claude workflow / GitHub repos / Claude Code plugins / skills” 这类短内容，强调可马上收藏、安装和复用。
- 讨论点：
  - 短视频平台更容易放大“多少个 skills / 多少个 repo / 多少倍效率”这样的数字叙事。
  - 设计 skill、Claude Code 资源索引、视频/会议 skill、agent skills 目录都适合被包装成清单型内容。
- 争议：Instagram 内容通常缺少版本、许可证、维护状态和权限边界，只能作为传播信号，不能作为工程选型证据。

## YouTube 热点

- 可复核入口 1：<https://www.youtube.com/watch?v=N0hLmUc3jUs>
- 可复核入口 2：<https://www.youtube.com/watch?v=WvBv6ASCt5E>
- 可复核入口 3：<https://www.youtube.com/watch?v=SY6HkgTW9AA>
- 热度信号：YouTube 近期仍围绕 Claude Code、Codex、开源 coding agent、AI agent skills 教程展开，重点是替代方案、安装流程和真实工作流体验。
- 讨论点：
  - “Claude Code limit 后尝试 Codex”“如何创建 agent skills”“免费替代 Copilot / Claude Code”这类内容说明用户关心成本、额度和可迁移能力。
  - 教程视频把 GitHub 热点从 repo 列表推进到具体操作：如何安装、如何设置技能、如何把 agent 接进现有开发流程。
- 评价：YouTube 对 adoption narrative 很有用，但具体项目成熟度仍要回到 GitHub issue、release、文档和可复现实验。

## 评价与争议

- **事实层**：GitHub API 与公开网页显示，今天高信号 AI 项目集中在 Claude Code / Codex / Antigravity 生态、agent skills、系统提示词和个人 agent workbench。
- **判断层**：agent 生态正在把“模型能力”拆成三层资产：宿主工具、可安装技能、可委派子 agent。
- **不确定性**：GitHub star 数可能受短期传播、榜单站、社媒清单和自动化账号影响；X / Instagram 指标仍不可稳定复核。

## 今日新增项目

- `claude-antigravity-agents` -> `Coding Agents 与终端助手`
- `system-prompts-and-models-of-ai-tools` -> `Agent 框架与技能生态`
- `ui-ux-pro-max-skill` -> `前端、UI 与 Agent 交互层`
- `oh-my-openagent` -> `Coding Agents 与终端助手`
- `awesome-claude-code` -> `Agent 框架与技能生态`
- `nanobot` -> `记忆层与个人 AI 基础设施`

## 明日跟踪建议

- 观察 `claude-antigravity-agents` 是否形成更多跨 agent 委派模式，尤其是隔离 worktree 和验证流程。
- 跟踪 `system-prompts-and-models-of-ai-tools` 与 `system_prompts_leaks` 的来源标注、更新时效和安全争议。
- 观察 `ui-ux-pro-max-skill` 是否从规则库扩展为可验证的设计质量评估工具。
- 跟踪 `nanobot` 是否继续把个人 agent kernel、MCP、聊天渠道和自动化稳定到日常使用层。
