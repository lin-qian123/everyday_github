# OpenOPC

<!-- markdownlint-disable MD013 MD012 -->

## 定位

`OpenOPC` 是 HKUDS 推出的 AI-native company 工作台。它试图把复杂任务组织成“招聘角色、分派任务、交接协作、沉淀组织记忆”的自动化公司流程，覆盖软件开发、投研、媒体、电商、教育等多个场景。

它不是单个聊天助手，而是把多角色 agent、办公室式 UI、CLI、工作区、权限和记忆层组合成一个可运行的个人 AI 公司原型。

## 用法

项目支持 CLI 与浏览器 Office UI。典型启动流程包括：

```bash
uv sync
uv run playwright install chromium
uv run opc init
uv run opc office
```

用户需要配置 LLM key 或环境变量，然后可以通过 UI 创建任务、选择组织架构、查看 kanban、管理 workspace，也可以用 CLI 进行交互、一次性任务、公司模式和脚本化运行。

## 原理

OpenOPC 的核心思路是把“公司”抽象成若干可配置包：

- Architecture：预置或自定义组织架构。
- Role / Employee：按任务招聘或分配角色型 agent。
- Workspace：承载文件、项目、记忆、skills 和任务状态。
- Task handoff：让不同角色按流程交接，而不是单 agent 一次性完成。
- Office UI：用可视化工作台呈现公司、任务、kanban、组织和交付物。

从 README 看，项目使用 Python 3.10+、React、Phaser 和 Playwright，强调本地初始化、可导入导出组织包以及 Feishu 等外部连接。

## 价值

- 对多 agent 产品：提供了“组织结构即编排结构”的实验样本。
- 对非工程任务：把投研、媒体、销售、教育等场景也纳入 agent 协作，而不只关注 coding。
- 对个人自动化：适合观察 AI 工作台如何从聊天窗口演化成任务/组织/文件/审批一体化系统。
- 对生态复用：可导入 talent library 与组织架构包，接近 agent 角色市场的雏形。

## 风险边界

- “AI 公司”概念很强，但真实交付质量仍依赖模型、工具、数据源和人类验收。
- 多角色协作会放大成本和错误传播，必须明确审批、权限和任务边界。
- 浏览器工具、外部连接和文件工作区可能触及隐私数据，应先在隔离目录中试用。
- 当前热度主要来自新项目增长，生产可用性仍需长期验证。

## 补充建议

- 优先用低风险场景试跑，例如资料整理、公开信息调研和 demo 原型。
- 对每个角色设定明确的输入/输出协议，避免“职位名很丰富、交付物很模糊”。
- 关注它后续是否补充 benchmark、失败案例、成本统计和权限审计。
- 可与 `agent-runtime`、`gastown`、`ai-maestro` 等项目横向比较：一个偏组织工作台，一个偏 runtime，一个偏工程治理。

## 参考资料

- GitHub 仓库：<https://github.com/HKUDS/OpenOPC>
- HKUDS 组织：<https://github.com/HKUDS>
