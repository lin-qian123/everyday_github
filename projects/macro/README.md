<!-- markdownlint-disable MD013 -->

# Macro（macro-inc/macro）

> 上游仓库：<https://github.com/macro-inc/macro> · 归类：办公、商业与行业应用 · 本页基于 2026-09-29 的 GitHub API、README、local-stack / Agent / MCP 文档、Release、Security 说明与 LICENSE 静态整理，未注册托管服务、同步邮件或运行完整本地栈。

- 抓取快照：4,477 stars、435 forks、172 open issues。
- 热度信号：GitHub Rust Trending 抓取时约 +16 当日 stars。
- 版本与许可：AGPL-3.0；latest GitHub Release 为 `v2026.9.28.0`，根 `VERSION` 仍为 `v2026.4.28.0`，版本平面需按 artifact / commit 分开确认。

## 定位

Macro 是把 email、team chat、Markdown docs、tasks、calls、CRM、GitHub PR 与 Agents 合并的团队工作区。它以双向 `@link`、统一权限和 nightly team memory 把人、内容与 Agent 放进同一上下文；既提供托管产品，也公开可本地运行的 AGPL 全栈代码。

## 用法

普通用户可使用托管 app；开发者可在 Nix shell 中只运行前端并连接 hosted dev services，或用 Docker 启动包含 Postgres、Redis、LocalStack、OpenSearch、Kafka、FusionAuth 与 Rust services 的完整本地栈。Agent 可从内置聊天或 MCP 接入，搜索团队数据、编辑文档、创建任务和操作其他已授权对象；真实 Google / GitHub / Stripe 等集成需要另行提供 secrets。

## 原理

邮件、消息、文档、任务、联系人与 PR 都以可链接 block / graph 组织，channel membership 决定分享范围。协作文档基于 CRDT，Agent 作为 peer 参与编辑；系统每晚把会话、邮件、任务等汇总进 team-level memory，同时用 MCP / tool surface 暴露 UI 中的大部分动作。本地开发栈还可把 Agent prompt、output 与 tool activity 写入 tracing 系统。

## 价值

把“沟通上下文—任务—Agent—PR”放在同一引用链中，有助于减少跨 Slack、邮箱、文档和工单系统复制上下文，也使 Agent 行为更容易回到来源对象审计。完整 AGPL 代码、本地 fixture 与多 persona permission seed 为独立评估提供了比纯 SaaS 更好的起点。

## 风险边界

- 统一 team memory 汇集邮件、DM、通话转录、文档、任务与 CRM，能提高检索，也形成高敏感、跨角色的集中数据资产。
- channel-based sharing、`@mention` 和 Agent action 可能造成权限扩散或 confused-deputy；离开 channel 是否彻底撤销派生 memory / cache 需独立验证。
- “zero data retention with model providers”、SOC 2 / ISO 标识与托管服务声明来自上游；具体 provider、region、DPA、日志与删除承诺需回到合同和实际配置。
- 前端连接 hosted dev services 不是本地数据路径；完整本地栈也可能在启用真实 integrations / model provider 后外发数据。
- CRDT 合并保证协作收敛，不保证 Agent 编辑正确；nightly synthesis 会放大错误、过时信息与 prompt injection。
- AGPL 网络使用义务、托管服务与商业安排需法律审查；Release 与根 `VERSION` 的明显漂移要求固定 commit / artifact。

## 补充建议

先用本地 stack、dummy integration 与 seed personas 做权限矩阵测试，避免把真实邮箱直接接入评估。为 Agent 分配独立身份、最小 channel 与只读 tools，对 send email、share、CRM update、task assignment 和 PR action 增加人工审批。把 memory source、更新时间、可见范围与删除传播纳入审计；关闭不需要的 GenAI content tracing，并为日志设置脱敏与保留期。

## 参考资料

- [GitHub 仓库](https://github.com/macro-inc/macro)
- [GitHub REST API](https://api.github.com/repos/macro-inc/macro)
- [v2026.9.28.0 Release](https://github.com/macro-inc/macro/releases/tag/v2026.9.28.0)
- [Running locally](https://github.com/macro-inc/macro/blob/main/docs/RUNNING_LOCALLY.md)
- [Agents documentation](https://docs.macro.com/product/agents)
- [MCP setup](https://docs.macro.com/AI/mcp/overview)
- [README：Security](https://github.com/macro-inc/macro/blob/main/README.md#security)
- [LICENSE](https://github.com/macro-inc/macro/blob/main/LICENSE.txt)
