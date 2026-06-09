# cmux

## 项目定位
cmux 是一个面向 macOS 的 AI 编码工作台终端，强调多会话并行、通知与开发效率体验，定位于“人类开发者 + 多智能体协作”的本地入口。

- GitHub: https://github.com/manaflow-ai/cmux
- Trending 参考: https://github.com/trending

## 用法
1. 按仓库说明安装并授予 macOS 所需权限。
2. 配置你常用的模型/代理工具（如 Codex、Claude Code、Cursor 等）。
3. 建立多标签工作区，把不同任务分配给不同会话。
4. 用通知与日志回放机制追踪长任务结果。

## 原理
- 终端增强层：在原生终端能力上叠加多会话和提醒机制。
- Agent 编排层：把多个编码 Agent 当作并行执行节点。
- 人在回路层：开发者负责审阅、合并和风险决策。

## 价值
- 提高多任务并行处理效率，减少上下文切换损耗。
- 适合“本地优先”的研发团队快速落地智能体协作。

## 风险边界
- 多 Agent 并行会放大误改代码风险。
- 通知驱动流程可能导致“过度自动化依赖”。
- 需严格区分实验环境与生产环境权限。

## 补充建议
- 为每个会话绑定独立目录与最小权限。
- 默认要求关键改动必须人工 code review 后再合并。
- 增加失败重试与操作审计，避免不可追责。

## 参考资料
- 仓库主页：https://github.com/manaflow-ai/cmux
- GitHub Trending：https://github.com/trending
