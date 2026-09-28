<!-- markdownlint-disable MD013 -->

# AnythingMCP（HelpCode-ai/anythingmcp）

> 上游仓库：<https://github.com/HelpCode-ai/anythingmcp> · 归类：Agent 框架与技能生态 · 本页基于 2026-09-29 的 GitHub API、README、connector / deployment / tool-definition 文档、Security Policy、Release 与 LICENSE 静态整理，未接入 ERP、数据库、企业 API 或真实 MCP client。

- 抓取快照：561 stars、71 forks、27 open issues。
- 热度信号：GitHub TypeScript Trending 抓取时约 +84 当日 stars。
- 版本与许可：核心 AGPL-3.0-only；latest Release、tag 与根 `package.json` 均为 `v0.15.0` / `0.15.0`，cloud-operator `ee/` 代码另行许可。

## 定位

AnythingMCP 是自托管 MCP gateway / connector builder，把 OpenAPI / REST、SOAP / WSDL、GraphQL、OData、SQL 数据库或既有 MCP server 转成 Claude、ChatGPT、Copilot 等客户端可调用的 tools。上游称内置 265 个 adapters、2,400+ tools；这些是作者目录快照，不代表每个目标系统都已独立兼容验证。

## 用法

快速路径以 Docker Compose 启动本地实例，并生成 `JWT_SECRET` 与 `ENCRYPTION_KEY`；随后导入 adapter、API spec、Postman collection、WSDL 或数据库连接，配置 connector，再只把选中的 connectors 分配给一个 MCP server URL。默认 quickstart 绑定 `127.0.0.1` 且没有 TLS；对外部署应使用上游 `setup.sh` / Caddy 路径，并为角色、OAuth 与工具范围单独配置。

## 原理

adapter 是可复用定义，connector 是带目标地址与凭据的实例，MCP server 则只暴露被分配的 connectors。系统在运行时生成工具 schema、处理认证与参数映射；per-tool response mapping 可删减送给模型的字段，凭据以 AES-256-GCM 静态加密，RBAC / SSO / SCIM 约束用户与工具，audit log 在本地数据库保存完整上游输入输出。

## 价值

它把传统企业 API 与数据库接入 Agent 时常被重复实现的 schema、认证、审计、权限和响应裁剪集中起来，尤其适合 SOAP、ERP 与内部 API 仍多于原生 MCP server 的环境。read-only database 默认、角色工具白名单与 response mapping 为最小暴露提供了可操作起点。

## 风险边界

- gateway 同时集中 ERP / CRM / 数据库凭据、业务响应和 MCP action，攻陷、误配或 prompt injection 的爆炸半径很大。
- “self-hosted”只说明 gateway 位置；被允许的字段仍会送往所选模型 / 客户端，cloud 版本又有独立托管数据流。
- 数据库工具虽默认限制单条 `SELECT`，仍应使用数据库原生只读账号；REST / SOAP / GraphQL adapter 可能包含写操作，自动生成 schema 不等于安全授权。
- audit log 保存完整上游 response，既利于追责也可能形成新的 PII、商业秘密和 retention 风险。
- `ENCRYPTION_KEY` 丢失会导致 connector 全部重新授权，泄露则威胁集中凭据；备份、轮换与灾难恢复必须作为 secret management 设计。
- AGPL 网络 copyleft 与 `ee/` 单独许可需按修改、托管和再分发方式审查；“production at”与 connector 数量均为上游陈述，本页未复现。

## 补充建议

先在非生产环境以单个 read-only connector 验证；使用源系统最小权限 service account、角色工具白名单、静态参数化 query 和严格 response mapping。对 connector spec 与工具描述做 prompt-injection / confused-deputy 审计，限制 gateway egress，设置审计日志脱敏与保留期，并把 `ENCRYPTION_KEY` 纳入受控 secret backup。任何写操作都应增加 MCP 外的人工审批、预算 / 速率限制与结果回读。

## 参考资料

- [GitHub 仓库](https://github.com/HelpCode-ai/anythingmcp)
- [GitHub REST API](https://api.github.com/repos/HelpCode-ai/anythingmcp)
- [v0.15.0 Release](https://github.com/HelpCode-ai/anythingmcp/releases/tag/v0.15.0)
- [Deployment Guide](https://github.com/HelpCode-ai/anythingmcp/blob/main/docs/deployment.md)
- [Database connectors](https://github.com/HelpCode-ai/anythingmcp/blob/main/docs/connectors/database.md)
- [Tool definition 与 response mapping](https://github.com/HelpCode-ai/anythingmcp/blob/main/docs/tool-definition.md)
- [Security Policy](https://github.com/HelpCode-ai/anythingmcp/blob/main/SECURITY.md)
- [License FAQ](https://github.com/HelpCode-ai/anythingmcp/blob/main/docs/license-faq.md)
- [LICENSE](https://github.com/HelpCode-ai/anythingmcp/blob/main/LICENSE)
