<!-- markdownlint-disable MD013 -->

# Founder OS（Bennettxai/FounderOS）中文解读

> 上游仓库：<https://github.com/Bennettxai/FounderOS> · 归类：办公、商业与行业应用 · 本页基于 2026-10-13 的 README、SYSTEM、SECURITY、compose / env、tag、许可证与 GitHub REST API 静态整理；未接入邮箱、Slack、WhatsApp、支付、广告、交易、真实客户或公司数据。

## 定位

Founder OS 是面向个人公司、自由职业者与小团队的自托管业务控制台。v2 构建在 BusinessOS 上，将统一通讯、客户漏斗、内容、财务、Agent roster、任务、skills 和知识图谱整合进一个 workspace-scoped 操作界面。

## 用法

上游本地 quickstart 需要 Node、Go、PostgreSQL + pgvector、Redis、Elixir 和 Python，以 `make dev-local` 启动后创建本地账户，再运行 `make demo` 导入四个演示 workspace。默认 connector 展示 seeded 数据和真实连接状态；只有显式开启 `FOUNDEROS_WRITES=1` 与 `FOUNDEROS_CRONS=1` 才允许外部写入和定时 Agent。

## 原理

- SvelteKit 前端显示业务视图，Go / Gin 后端将 workspace-scoped Postgres 数据、connectors 和 Agent actions 组合成页面。
- Redis 承担 session / runtime 状态，Optimal Engine 负责 source、signal、claim、fact 与语义检索；事实采用 promotion gate。
- 24 类 connector 以 `connected`、`not_configured` 或 `error` 明示状态，演示数据和真实连接走同一页面路径。
- BusinessOS 的 RBAC、workspace 与 credential vault 提供底层身份和数据边界；Electron shell 为可选桌面入口。

## 价值

- 比纯 dashboard demo 更明确地区分应用状态、知识记忆、connector 状态和 Agent 执行开关。
- outbound writes 与 cron 默认关闭，为个人公司场景提供了可检查的 deny-by-default 起点。
- v2 直接继承 BusinessOS / Optimal Engine 的 workspace、权限、检索和恢复能力，适合研究 Agent 如何进入真实业务台账。

## 风险边界

- 它把邮件、聊天、客户、财务、广告、交易、知识和 Agent 集中到一个高权限控制面；单租户演示通过不代表多租户、灾备或合规通过。
- 开发 compose 暴露 PostgreSQL、Redis、engine、backend 和 frontend 端口，并带开发默认密码 / key；只能用于隔离本机，生产必须换密钥和收敛绑定。
- SECURITY 描述的 RBAC、加密、审计和合规计划属于上游设计 / 自述，仓库也注明 MFA、依赖扫描、数据导出和认证仍有未完成项。
- `FOUNDEROS_WRITES` 是应用开关，不替代各外部系统自身的 scope、审批、预算、幂等、回滚和写后回读。
- 无 GitHub Release，只有旧 v1 的 `v1-nextjs` tag；直接跟随 `main` 会增加部署漂移。

## 补充建议

- 从纯 demo、测试 connector 和虚构 workspace 开始；逐个连接真实系统，并为每个 action 声明读取 / 写入 / 费用 / 不可逆边界。
- 生产部署先完成 secret rotation、loopback / private network、TLS、备份恢复、tenant 越权和审计日志测试。
- 固定 commit 与 schema migration；把 Agent 生成的 claim 保持为待审状态，不让检索层自动晋升为业务事实。

## 参考资料

- GitHub 仓库：<https://github.com/Bennettxai/FounderOS>
- GitHub REST API：<https://api.github.com/repos/Bennettxai/FounderOS>
- README / v2 架构：<https://github.com/Bennettxai/FounderOS/blob/main/README.md>
- System model：<https://github.com/Bennettxai/FounderOS/blob/main/SYSTEM.md>
- Security policy：<https://github.com/Bennettxai/FounderOS/blob/main/SECURITY.md>
- 环境变量模板：<https://github.com/Bennettxai/FounderOS/blob/main/.env.example>
- LICENSE：<https://github.com/Bennettxai/FounderOS/blob/main/LICENSE>
