# open-connector

<!-- markdownlint-disable MD013 MD012 -->

## 定位

`open-connector` 是 OOMOL 开源的 AI agent 连接器网关，目标是把 GitHub、Gmail、Notion、BigQuery、Supabase、Slack 等 SaaS 与数据系统通过统一的 SDK、CLI、MCP、HTTP 和 OpenAPI 接口暴露给 agent。它更像是“agent 工具调用的认证与动作网关”，而不是单个 MCP server。

截至 2026-07-10 抓取时，GitHub 仓库约 `1114` stars、`62` forks，主语言为 TypeScript，许可证为 Apache-2.0。

## 用法

- 本地开发可用 `docker compose up --build` 启动网关，再访问 `http://localhost:3000` 和 `http://localhost:3000/docs`。
- agent 宿主可以通过 MCP 访问本地 `/mcp` 端点，也可以直接调用 `/v1/actions/*` HTTP API。
- 应用代码可用 Connector SDK；本地 agent relay 可用 `oo connector` 搜索、检查和执行 actions。
- 管理员通过 Web Console 浏览 provider、配置凭据、创建 runtime token、调试 action，并查看运行日志。

## 原理

项目把 provider catalog、credential/OAuth 边界、action schema、scope、allow/block policy、runtime token 和 redacted run log 放到同一个可审计 runtime 中。agent 看到的是 action 元数据、schema 和执行结果，真实 provider secret 留在网关内。部署形态覆盖本地 Docker/Node、Fly.io、Cloudflare Workers + D1/R2，以及 OOMOL hosted runtime。

## 价值

- 把“给每个 agent 单独配置 OAuth/API key”的问题抽成中心化连接层。
- 对需要连接大量 SaaS 的 agent 产品，比手写几十个 MCP server 更容易统一权限、审计和日志。
- OpenAPI、MCP、SDK 共用一套 action contract，降低自托管和商业 hosted 之间的迁移成本。
- 对团队来说，运行日志、scope 和 token policy 是比“agent 直接拿 token”更可治理的边界。

## 风险边界

- 连接器网关本身会成为高价值凭据边界，部署、备份、日志脱敏和 token 生命周期必须严格管理。
- provider 数量与 action 数量很大时，实际质量取决于每个 action executor 的维护状态，不能只看 catalog 数字。
- OAuth app 审核、provider 速率限制和企业合规要求仍需逐个服务处理。
- 对高度敏感系统，建议先用只读 scope、allowlist action 和测试账号验证。

## 补充建议

- 与 `postman-mcp-server`、`mcphub`、`modelcontextprotocol-servers` 横向比较，区分“单服务 MCP”“MCP 网关”和“OAuth/action gateway”。
- 首轮落地优先接 GitHub、Slack、Notion、Google Workspace 等低风险读操作，逐步扩展写操作。
- 为团队部署补充 secret rotation、审计导出和 action 级审批策略。

## 参考资料

- GitHub 仓库：<https://github.com/oomol-lab/open-connector>
- Connector SDK：<https://github.com/oomol-lab/connector-sdk>
- oo CLI：<https://github.com/oomol-lab/oo-cli>
- Cloudflare quick start video：<https://www.youtube.com/watch?v=R0V1ZdCuTgc>
