<!-- markdownlint-disable MD013 -->

# agent-teams-ai（777genius/agent-teams-ai）

> 记录日期：2026-09-06（Asia/Shanghai）。本页依据上游 README、SECURITY、release、LICENSE 与 GitHub REST API 做静态整理；本轮未下载 Electron 应用、未启动任何 agent、未连接订阅或 API key。

## 定位

`agent-teams-ai` 是一个 Electron 桌面多代理编排工作台，将团队/角色、Kanban 任务、跨 agent 消息、代码 diff/review、终端、日志、token/成本预算和多 provider 连接放进一个界面。它可发现本机 Claude Code、Codex、OpenCode，也列出 Cursor、GitHub Copilot、Kiro、SuperGrok 等接入路径。

2026-09-06 的 GitHub 官方 TypeScript Trending 抓取显示约 `+19 stars today`；REST API 快照为 `2,069 stars / 348 forks / 32 open issues`，最新 release 为 `v2.12.0`，许可证为 AGPL-3.0。

## 用法

上游提供 macOS、Windows 与 Linux 安装包；源码开发要求 Node.js 24.16.0 LTS 与 pnpm 10+：

```bash
git clone https://github.com/777genius/agent-teams-ai.git
cd agent-teams-ai
pnpm install
pnpm dev
```

正式使用时应先在无敏感代码的测试项目中选择一个低权限 agent，关闭外部写操作，核对 provider、工作目录、worktree、审批和预算后再逐步增加团队成员。

## 原理

- **桌面控制面**：Electron/React UI 展示团队、任务、进度、依赖、评论、日志、diff、资源和费用。
- **运行时适配**：按已安装 CLI、订阅或 API provider 启动不同模型/agent runtime，而不是自研单一模型。
- **任务协议**：team lead 可拆解任务，成员通过消息、评论和状态变化协作，并形成可回看的任务时间线。
- **工作区策略**：成员可共享主 checkout，或选择独立 Git worktree；额外分支/合并规则仍依赖 provisioning prompt 和 Git 流程。
- **审批与观察**：支持的工具动作可逐项审批，也可选择更高自治；日志、进程、token 和估算成本集中展示。
- **本地数据边界**：上游安全说明称写操作约束在所选项目根目录，同时只读发现会访问 `~/.claude/` 与应用状态路径。

## 价值

- 让非纯终端用户更直观地监督多个 agent 的任务、消息、日志和代码改动。
- 将 provider、模型、agent 角色和预算放到同一控制面，便于比较成本与任务分工。
- 可选 worktree、任务级日志和 diff review 为并行协作提供基础可见性。
- AGPL-3.0 源码和本地开发入口有利于审查桌面控制面的实际行为。

## 风险边界

- 看板、角色、评论和 agent 自评不证明任务正确完成；测试、构建、运行证据与人工 code review 仍须独立执行。
- Git worktree 只隔离工作副本，不隔离进程、网络、用户凭据、主机资源或外部服务权限。
- 多 provider 与自动发现会扩大凭据、订阅条款、数据外发、费用和日志留存面；“free model/no auth”也不代表无数据或服务风险。
- 逐项审批只覆盖被宿主/runtime 暴露为可审批的动作；shell、脚本和下游工具可能把多个外部副作用合并在一次调用中。
- 控制面读取项目、CLI 会话和 `~/.claude/` 数据；需验证路径校验、symlink、终端历史、附件、日志导出和删除。
- AGPL-3.0 对修改、分发和网络交互场景可能触发源码提供义务，组织采用前须按部署形态审查。

## 补充建议

- 用两个 agent 在可丢弃仓库测试同文件冲突、worktree 切换、跨团队消息、rate limit、crash 和任务错误归属。
- 为每个 runtime 建独立低权限配置目录和测试 key，禁止默认继承个人生产凭据。
- 把“agent 报告完成”“代码有 diff”“测试通过”“人工接受”设成四个不同状态，不允许互相替代。
- 验证预算告警是否涵盖缓存、reasoning、工具服务和订阅外费用，并测试 80%/100% 阈值后的真实停止行为。
- 审计安装包签名、自动更新、IPC/HTTP handler、symlink 逃逸、附件路径和日志清除，再考虑真实项目。

## 参考资料

- [GitHub 仓库](https://github.com/777genius/agent-teams-ai)
- [GitHub REST API](https://api.github.com/repos/777genius/agent-teams-ai)
- [v2.12.0 Release](https://github.com/777genius/agent-teams-ai/releases/tag/v2.12.0)
- [项目站点](https://agentteams.live/)
- [Security Policy](https://github.com/777genius/agent-teams-ai/blob/main/.github/SECURITY.md)
- [AGPL-3.0 LICENSE](https://github.com/777genius/agent-teams-ai/blob/main/LICENSE)
