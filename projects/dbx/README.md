<!-- markdownlint-disable MD013 -->

# DBX（t8y2/dbx）

> 上游仓库：<https://github.com/t8y2/dbx> · 归类：办公、商业与行业应用 · 本页基于 2026-09-30 的 GitHub API、README、MCP / CLI 文档、数据安全迁移说明、Release、Security Policy 与 LICENSE 静态整理，未连接真实数据库、调用模型或验证插件隔离。

- 抓取快照：21,941 stars、2,084 forks、1,248 open issues。
- 热度信号：GitHub 综合与 Rust Trending 抓取时约 +349 当日 stars。
- 版本与许可：Apache-2.0；latest Release 与 tag 均为 `v0.6.28`。

## 定位

DBX 是 Rust / Tauri 构建的跨平台数据库客户端，同时提供 Web / Docker、CLI、AI SQL 助手和独立 MCP server。它把数据库浏览、查询、ER 图、导入导出和 Agent 访问放在同一连接配置上；“100+ databases”包含原生、JDBC 与 agent-based profile，多种接入的能力并不完全等价。

## 用法

桌面端可用 Homebrew 或 Release 安装，Web 版可通过 Docker 部署。AI SQL 助手支持 Claude、OpenAI、本地 Ollama 和 OpenAI-compatible endpoint。MCP server 以 `npx @dbx-app/mcp-server` 启动，并复用 DBX 已配置连接；应在 Settings → MCP 明确连接 allowlist 与 `read_only`、`safe_write`、`high_risk_write` 权限。CLI 可安装 `@dbx-app/cli`，再用 `dbx agent setup`、`connections list` 和 `query` 接入脚本或 Agent。

## 原理

桌面端用 Tauri / Rust 承载连接与查询能力，前端负责编辑器、数据网格和可视化；MCP server 与 CLI 作为独立包读取同一策略和连接资料。桌面构建把凭据放入平台 credential store，Web / Docker 以持久 secret key 加密 `dbx.db`；插件包声称先验签，UI 与 sidecar 分离运行。MCP 最终仍把列举 schema、执行 SQL 和打开表等能力暴露给外部 Agent。

## 价值

对同时维护多类数据库的团队，统一连接、查询、脚本和 Agent 接口能减少在 GUI、终端与聊天窗口间复制 schema / SQL。权限模式和连接 allowlist 比“给模型一个数据库账号”更可审计；独立 CLI / MCP 也便于在 CI 或 coding-agent 工作流中只启用需要的表面。

## 风险边界

- MCP 的 `safe_write` / `high_risk_write` 会把自然语言请求转成真实数据库副作用；权限标签不能替代最小权限账号、事务、备份、审批和查询回读。
- AI 生成 SQL 的内置检查只是一层启发式防线，不证明语义正确、无越权或不会触发锁表、全表更新和高成本查询。
- “100+ databases”跨原生 driver、JDBC 和 agent profile；兼容、事务、类型、TLS 与认证能力须按具体数据库复核。
- 凭据加密依赖平台 credential store 或持久 key；直接复制 `dbx.db` 不是跨平台同步方案，迁移旧明文凭据时必须备份并验证回滚。
- README 的签名 / sandboxed plugin 主张未在本轮做恶意插件测试；插件 sidecar、网络出口和 SDK 权限仍需独立审计。
- Apache-2.0 只覆盖仓库代码；数据库驱动、服务端、模型 provider、插件、商标和数据本身可有额外条款。

## 补充建议

先用只读测试账号和合成数据库验证 schema 浏览、超时、行数限制与日志脱敏，再逐项开放写权限。把 MCP allowlist、数据库 RBAC、网络 ACL 和审计日志同时纳入变更评审；生产写入默认要求事务、影响行数上限、人工确认和可恢复备份。升级时固定 Release，备份 `dbx.db` 与密钥并实际演练恢复。

## 参考资料

- [GitHub 仓库](https://github.com/t8y2/dbx)
- [GitHub REST API](https://api.github.com/repos/t8y2/dbx)
- [v0.6.28 Release](https://github.com/t8y2/dbx/releases/tag/v0.6.28)
- [MCP server README](https://github.com/t8y2/dbx/blob/main/packages/mcp-server/README.md)
- [CLI README](https://github.com/t8y2/dbx/blob/main/packages/cli/README.md)
- [数据安全迁移说明](https://github.com/t8y2/dbx/blob/main/docs/data-security-migration.md)
- [Security Policy](https://github.com/t8y2/dbx/blob/main/SECURITY.md)
- [LICENSE](https://github.com/t8y2/dbx/blob/main/LICENSE)
