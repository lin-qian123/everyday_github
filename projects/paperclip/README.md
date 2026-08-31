<!-- markdownlint-disable MD013 MD034 -->

# paperclip：用组织结构、目标、预算和心跳管理工作型 agents

## 项目概览

- 上游仓库：https://github.com/paperclipai/paperclip
- GitHub API 快照（2026-09-01）：79,765 stars、14,632 forks、5,442 个开放 issue
- 当前 release：`v2026.824.1`
- 主要技术：TypeScript、Node.js、Postgres、Web control plane
- 许可证：MIT

## 定位

Paperclip 是 agent 管理控制面，而不是基座模型或单一执行 agent。它把 Claude Code、OpenClaw 等外部 agent 组织成公司/团队，用组织图、目标、项目、任务、心跳、预算和审计记录协调工作。

## 用法

上游要求 Node.js 24.11+ 与 pnpm 9.15+，快速入口围绕 CLI onboarding。典型流程是先创建 organization、使命与项目，再注册 agent、上下级关系、预算和触发方式。

本地默认由一个 Node 进程连接嵌入式 Postgres 与本地文件；部署环境可改用独立 Postgres。接入真实业务系统前，应从只读、低预算、无敏感数据的测试 organization 开始。

## 原理

Paperclip 用组织结构约束委派关系，用 goal/project/task 建立工作来源，用 heartbeat 或事件唤醒 agent，用 checkout/ownership 避免重复领取，用月度预算限制模型花费，并记录任务、决策和状态。

控制面只能协调它能够观察到的 agent 行为。外部 CLI 的文件、终端、浏览器、OAuth 和网络权限仍由各自 runtime 决定；预算停止也不等于操作已被撤销。

## 价值

- 为多 agent 长任务提供统一的组织、任务与成本视图。
- 将目标到任务的链路显式化，便于审阅 agent 为什么在做某件事。
- BYO agent 设计允许复用不同执行器，而不把工作流锁在单一模型。
- 多 organization 与日志适合团队试验、对比和故障复盘。

## 风险边界

- “zero-human company”是产品叙事，不是无人监督即可可靠经营的证据。
- 预算只能限制可计量的模型成本，不能自动限制发信、删除、交易、发布或凭据泄露等副作用。
- 多 agent 委派会放大提示注入、错误目标、重复执行、上下文污染和责任模糊。
- 单一 control plane 与数据库会成为高价值权限和审计目标；多组织隔离需独立测试。
- 本页依据上游静态资料与 API，未部署、未测试隔离，也未验证任务完成率。

## 补充建议

1. 把 agent 权限放在 runtime/OS/OAuth 层最小化，不依赖 Paperclip UI 作为唯一安全边界。
2. 对外发布、付款、删除、合并和权限变更设置不可绕过的人类审批。
3. 使用幂等任务、租约、超时和补偿动作，测试 heartbeat 重复与断网恢复。
4. 为每个 agent 记录模型、工具、预算、数据域、owner 和停止条件。
5. 用合成公司跑长时回归，衡量重复任务、失控成本、升级链和审计完整性。

## 参考资料

- 仓库与 README：https://github.com/paperclipai/paperclip
- 官方站点：https://paperclip.ing
- Releases：https://github.com/paperclipai/paperclip/releases
- 官方 X 账号：https://x.com/papercliping
- 可观测性说明：https://github.com/paperclipai/paperclip#observability
