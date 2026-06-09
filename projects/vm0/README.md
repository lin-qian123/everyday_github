# VM0

VM0 是一个以自然语言为中心的 AI Agent 运行时与编排平台，强调用“写意图”而不是“画流程图”来定义工作流，并提供云端沙箱、可观测性与调度能力，面向 24/7 自动化场景。

## 为什么值得关注
- GitHub Trending Today（全语言）榜单中名列前列，定位为“the easiest way to run natural language-described workflows automatically”。
- 典型定位是“自然语言定义流程 + 云端长期运行 + 运行审计/回放”，适合构建可持续运行的 Agent。

## 核心理念与原理
- 自然语言即工作流：用指令（Instructions）描述任务步骤与约束，系统将其转为可执行的 Agent 行为。
- 状态化会话与可回放：运行以会话为单位，支持日志与执行细节追踪，便于复盘与调试。
- 多模型路由：可在不同模型之间切换或路由，按成本/能力选择最合适的执行后端。
- 云端沙箱与自动化调度：本地开发、云端执行，支持定时与持续运行。

## 快速上手（CLI）
- 一键初始化：`npm install -g @vm0/cli && vm0 onboard`
- 账号登录：`vm0 auth login`
- 配置模型提供方：`vm0 model-provider setup`
- 初始化第一个 Agent：`mkdir my-agent && cd my-agent`，在目录内通过 CLI 引导完成初始化。

## 在 Claude Code 里快速“写 Agent”
- `vm0 onboard` 会完成认证、模型配置、项目创建与技能安装。
- 在项目里执行：`vm0 setup-claude`
- 可使用 Claude Code 内的 `/vm0-agent` 与 `/vm0-cli` 指令以自然语言创建或更新 Agent。

## 常见用法示例
- 内容聚合与发布：抓取 HN/Reddit 等内容并按模板输出到文件或 Notion。
- 市场/竞品情报：定时采集、归纳信息并输出日报。
- 工具链自动化：连接外部 API 或 SaaS（通过 Skills）完成多步骤流程。

## 关键概念速览
- Instructions：用自然语言定义流程步骤与约束。
- Skills：为 Agent 增加工具与 SaaS 集成能力。
- Volumes/Artifacts：运行中使用与产出的文件存储。
- Environment Variables：配置密钥与外部系统参数。

## 参考链接
- 官网与快速开始：https://www.vm0.ai/
- 快速上手文档：https://docs.vm0.ai/docs/quick-start
- Vibe Coder 快速开始：https://docs.vm0.ai/docs/vibe-coder-quickstart
- 文档总览（概念与教程）：https://docs.vm0.ai/
- GitHub Trending Today 榜单：https://github-trending.today/
