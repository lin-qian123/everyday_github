<!-- markdownlint-disable MD013 -->

# n8n Skills（czlonkowski/n8n-skills）

> 上游仓库：<https://github.com/czlonkowski/n8n-skills> · 归类：Agent 框架与技能生态 · 本页基于 2026-10-08 的 GitHub API、README、安装 / 用法 / MCP 测试记录与 skill 文件静态整理，未连接真实 n8n instance、创建 workflow、写入 credential 或触发 webhook。

- 抓取快照：6,389 stars、1,054 forks、16 open issues。
- 热度信号：GitHub Shell Trending 抓取时约 +6 当日 stars；最后 push 为 2026-09-16。
- 版本与许可：最新 Release / tag `v1.35.0`，MIT；部分 hooks 思路改写自 Apache-2.0 的官方 n8n Skills，并在 NOTICES 中归属；本页固定审计 commit `19cd793f4789`。

## 定位

n8n Skills 是面向 Claude Code / Claude.ai 与 n8n-mcp 的 14 个工作流知识 skill、常驻 router 和 hooks 约束层，覆盖表达式、node 配置、workflow pattern、validation、JavaScript / Python Code node、AI Agent、错误处理、多实例和自托管。它提供操作知识，不是 n8n runtime 或权限代理。

## 用法

可通过 Claude plugin marketplace 安装，也可把选定 skill 复制到宿主目录；随后配置独立的 n8n-mcp。优先只启用 node 搜索、模板与 `validate_workflow` 等无业务写入工具；需要 API 时，再为测试 instance 配置 `N8N_API_URL` / `N8N_API_KEY`，并要求 Agent 在创建或更新前输出完整 workflow diff 与目标 instance。

## 原理

router 根据任务把 Agent 引导到专门 SKILL.md；SessionStart / PreToolUse / PostToolUse hooks 在高影响工具前后提醒多实例、credential 和 validation 规则。内容以 n8n-mcp 的实际 tool response、模板库与错误样例编写，区分无需 n8n API 的本地验证工具和需要真实 API 的 workflow create / update / trigger 工具。

## 价值

它把 n8n 容易出错的 nodeType、expression、AI connection、Code node 限制、validation profile 和 error workflow 写成可复用知识，并明确“validation necessary but insufficient”。多实例检查与 credential-write 提醒对减少 Agent 写错环境尤其有现实价值。

## 风险边界

- Skill / hook 只是提示和路由，不是强制 policy；Agent 仍可调用 n8n-mcp 的 create、partial update、credential management 与 webhook trigger。
- 显式切换到错误 instance 后，server 可能照常把 secret 写入错误环境；多实例场景必须在每次写前回读 `current` 和 instance identity。
- validation 主要检查 schema / 配置，不证明业务逻辑、幂等、速率限制、费用、数据保护、第三方 API side effect 或生产可恢复性。
- 工作流可能携带 credential reference、PII、prompt、binary 和下游 service 数据；调试日志、模板分享与模型上下文都需脱敏。
- 自托管 skill 涉及 VM、Docker、Redis、Postgres、encryption key、telemetry 与备份；生成“安全默认值”不能替代主机加固、升级和恢复演练。
- MCP testing log 与模板统计是上游特定时点材料；n8n / n8n-mcp 版本变化会使 node property、tool envelope 与 validation 行为漂移。

## 补充建议

把 dev / staging / prod 分成不同 API key 与网络 endpoint，Agent 默认只接 dev；credential write、activation、trigger、delete 和生产 update 全部外部审批。用 fake Slack / database fixture 做创建—验证—运行—回读—回滚测试，并锁定 n8n、n8n-mcp 与 skill pack 版本。

## 参考资料

- [GitHub 仓库](https://github.com/czlonkowski/n8n-skills)
- [GitHub REST API](https://api.github.com/repos/czlonkowski/n8n-skills)
- [安装说明](https://github.com/czlonkowski/n8n-skills/blob/main/docs/INSTALLATION.md)
- [使用说明](https://github.com/czlonkowski/n8n-skills/blob/main/docs/USAGE.md)
- [MCP testing log](https://github.com/czlonkowski/n8n-skills/blob/main/docs/MCP_TESTING_LOG.md)
- [Notices](https://github.com/czlonkowski/n8n-skills/blob/main/NOTICES)
- [n8n-mcp](https://github.com/czlonkowski/n8n-mcp)
- [v1.35.0 Release](https://github.com/czlonkowski/n8n-skills/releases/tag/v1.35.0)
