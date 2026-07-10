# OpenTag

<!-- markdownlint-disable MD013 -->

## 定位

`OpenTag` 是一个 Slack-first 的开源团队 agent gateway。它让团队在 Slack 线程中 `@OpenTag` 调用 Codex、Claude Code、OpenCode、Docker agent、HTTP agent 或自定义 CLI，并把上下文、审批、记忆、运行日志和产物留在同一个可审计线程里。

截至 2026-07-11，GitHub API 显示该仓库约 266 stars，创建于 2026-06-27，主要语言为 JavaScript，topics 包含 `agent-gateway`、`slack`、`codex`、`claude-code`、`mcp`、`team-collaboration`。README 标注状态为 MVP，许可证为 Apache-2.0。

## 用法

本地试用：

```bash
npm install
npm run smoke
npm run start:console
```

Slack gateway 初始化示例：

```bash
npm link
opentag init --project . --runtime mock --open-slack
opentag setup launch
opentag doctor --strict
```

在 Slack 中的体验类似：

```text
@OpenTag summarize why this deployment failed
@OpenTag check this thread and draft the fix plan
/runtime codex-readonly explain the current project structure
/opentag approvals
```

## 原理

OpenTag 把 Slack channel/thread 作为 agent 工作入口。每个 channel 可以有自己的 project、instructions、memory、permissions、default runtime、allowed users、approvers 和 run limits。用户在同一线程里补上下文，agent 执行进度、审批请求和结果也回到同一线程。

项目包含 Slack gateway、console mode、runtime adapters、Channel Profiles / Access Bundles、Team Knowledge、local storage、sessions、messages、approvals、runs、audit records 和 artifacts。它不是托管 SaaS，而是本地/团队自托管 MVP。

## 价值

- 解决“一个人在终端跑 agent，然后把结果粘回群里”的协作断层。
- 把团队知识、审批和权限绑定到 channel，适合多项目团队。
- 支持多个 agent runtime，避免只绑定一个供应商。
- 运行、审批、输出和产物可审计，利于安全与复盘。

## 风险边界

- MVP 状态，不宜直接当作成熟生产 SaaS。
- Slack token、runtime API key 和本地 workspace 权限必须严格管理。
- 写操作需要审批和文件系统边界，否则 channel mention 可能触发高风险自动化。
- 多实例存储、OAuth 安装、Web 管理 UI 和 sandbox hardening 仍在计划中。

## 补充建议

- 与 `open-connector` 区分：OpenTag 是团队 channel gateway，open-connector 是 SaaS action/auth gateway。
- 与 `homerail` 区分：OpenTag 面向 Slack 团队协作，HomeRail 面向本地 DAG runtime 和语音入口。
- 后续重点观察 Teams、Discord、GitHub issue 等新 channel 是否进入 gateway contract。

## 参考资料

- GitHub 仓库：<https://github.com/linxidnju/OpenTag>
- 中文 README：<https://github.com/linxidnju/OpenTag/blob/main/README.zh-CN.md>
- 安全文档：<https://github.com/linxidnju/OpenTag/blob/main/SECURITY.md>
- Open connector：<https://github.com/oomol-lab/open-connector>
