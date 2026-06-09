# craft-agents-oss（记录日期：2026-05-01）

- GitHub：<https://github.com/lukilabs/craft-agents-oss>
- 趋势信号：GitHub Trending（今日榜单出现，且近期 star 增长快）

## 1. 项目定位
`craft-agents-oss` 是一个面向“文档/知识工作流 + 多模型代理协作”的桌面应用框架。它强调：
- 多会话 Inbox 管理
- 多模型/多 Provider 接入
- MCP、REST、文件系统等外部源联动
- 自动化（定时/事件触发）

本质上，它是把“Agent IDE”从纯代码编辑场景扩展到“文档中心协作场景”。

## 2. 如何使用（快速上手）
1. 一键安装（macOS/Linux/Windows 均有脚本）。
2. 首次启动后选择模型连接方式（Anthropic / OpenAI / Copilot / Google 等）。
3. 创建 workspace，配置来源（MCP、API、本地文件）。
4. 在多会话界面分配任务状态（Todo/In Progress/Done 等）。
5. 为重复工作配置 automation（如日报、周报、标签触发任务）。

## 3. 原理拆解
- 会话与状态机：把 agent 任务抽象为“可跟踪工单流”。
- 连接器层：通过 MCP/REST 把外部系统工具化。
- 多模型编排：按任务类型切换/并行不同模型，提高性价比。
- 差异审阅：提供多文件 diff 视图，降低自动改动不可见风险。

这类架构的核心不是“单次对话能力”，而是“持续任务系统能力”。

## 4. 价值与风险
### 价值
- 适合跨文档、跨系统的知识型团队协作。
- 自动化能力可显著减少重复运营工作。
- 对“长周期任务”比一次性聊天工具更友好。

### 风险
- 多连接器意味着更复杂的权限与凭证治理。
- 自动化触发链一旦设计不当，容易产生噪声任务或误操作。

## 5. 建议的落地顺序
1. 先接本地文件 + 单一模型，跑通最小流程。
2. 再接入关键外部系统（如 GitHub/Slack/Docs）。
3. 最后开放自动化和高权限模式，并补审计日志。

## 6. 补充资料
- 发布页（查看迭代节奏）：<https://github.com/lukilabs/craft-agents-oss/releases>
- 安装与功能说明：仓库 README（同上）
