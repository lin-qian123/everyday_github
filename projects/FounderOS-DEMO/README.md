<!-- markdownlint-disable MD013 -->

# Founder OS Demo（Bennettxai/FounderOS-DEMO）

> 上游仓库：<https://github.com/Bennettxai/FounderOS-DEMO> · 归类：办公、商业与行业应用 · 本页基于 2026-10-05 的 GitHub API、README、环境变量模板、agent / connector / access-gate 源码、manifest 与 LICENSE 静态整理，未接入邮箱、支付、CRM、社媒、broker 或真实公司数据，也未执行 Agent / trading 流程。

- 抓取快照：965 stars、277 forks、5 open issues。
- 热度信号：GitHub TypeScript Trending 抓取时约 +9 当日 stars。
- 版本与许可：MIT；无 GitHub Release / tag，private npm manifest 写 `1.0.0`；仓库明确是 seeded demo build，不是已部署生产系统。

## 定位

Founder OS Demo 是为一人公司设计的 AI 辅助业务控制台样板，把 communications、funnel、social、content、finances、agents、tasks、knowledge graph、workflows、brand deals 与 trading 放在一个 Next.js 界面。所有页面默认使用占位数据，展示的是架构和交互，不是一个已连接真实业务的 SaaS。

## 用法

Node 22 下运行 `npm install`、复制可选 `.env.example`，再用 `npm run dev` 启动本地 4100 端口；SQLite 会首次自动 seed，无凭据也可浏览。若要接真实系统，需要按 connector 填写 IMAP、Slack、Stripe、Notion、calendar、CRM、social 等密钥，并将 stub / seeded repository 替换为真实后端。

## 原理

Next.js route 和页面只通过 typed repository 访问 SQLite，Zod 在 DB / API 边界校验数据；connector 统一返回 `connected`、`not_configured` 或 `error`，runtime agent 的 `run()` 写入持久状态。知识层概念上把 Markdown / hybrid retrieval 的 G-Brain 与 `Source → Signal → Claim → Fact → Memory` 的 promotion gate 分开，但生产服务和真实向量 / memory backend 不在 demo 中完整交付。

## 价值

它是一个覆盖面很广的业务 Agent UI / data-contract 参考实现：seed、repository、schema、connector status、agent run、task board 和知识 promotion 都能在无真实凭据时审阅。对原型设计者，比只有静态截图更容易讨论哪些模块需要审批、来源、状态与可观察性。

## 风险边界

- README 多次强调 demo-first；占位客户、收入、社媒数字、Agent reasoning 和连接状态不能被当作真实业务能力、收益或自动化成功证明。
- `.env.example` 集中邮箱、Slack、支付、Notion、CRM、社媒、broker 与模型密钥；一旦接实，单一应用会成为高价值权限汇聚点。
- Finances、brand deals、comms 和 trading 属于高影响写操作；UI 中的 autopilot、agent roster 或 limit 展示不证明服务端不可绕过，必须逐 connector 建立确定性审批与幂等回执。
- G-Brain / Optimal Engine 的混合检索、事实 promotion 与生产 companion service 主要是设计说明；demo fallback 和 seed 不能证明生产 provenance、删除、隔离或恢复。
- README 的 cohort / product 链接使用 `example.com` 占位域名，说明对外服务与商业承诺不可由本仓库核实。
- 无 Release / tag，生产部署建议又依赖 Railway 与多项第三方服务；本轮未验证 access gate、密钥加密、tenant 隔离、provider 数据流或测试覆盖。

## 补充建议

把它当 UI / contract 样板而非现成 ERP：固定 commit `ef75fe898702`，先用 seed 和 fake connector 审查每条数据的来源、刷新时间、错误态和审批点。若接真实系统，按 connector 拆分低权限账号与独立 secret，所有发信、付款、发布、CRM 写入和交易先走 dry-run + 人工二次确认，并为 tenant、audit、删除、backup 和 incident response 补齐生产设计。

## 参考资料

- [GitHub 仓库](https://github.com/Bennettxai/FounderOS-DEMO)
- [GitHub REST API](https://api.github.com/repos/Bennettxai/FounderOS-DEMO)
- [README、架构与 demo 边界](https://github.com/Bennettxai/FounderOS-DEMO/blob/main/README.md)
- [环境变量与 connector 清单](https://github.com/Bennettxai/FounderOS-DEMO/blob/main/.env.example)
- [npm manifest](https://github.com/Bennettxai/FounderOS-DEMO/blob/main/package.json)
- [Credential helper](https://github.com/Bennettxai/FounderOS-DEMO/blob/main/lib/creds.ts)
- [Access gate](https://github.com/Bennettxai/FounderOS-DEMO/blob/main/lib/access-gate.ts)
- [LICENSE](https://github.com/Bennettxai/FounderOS-DEMO/blob/main/LICENSE)
