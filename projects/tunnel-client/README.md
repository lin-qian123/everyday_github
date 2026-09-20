<!-- markdownlint-disable MD013 MD034 -->

# tunnel-client：把私有 MCP Server 接入 OpenAI 产品的出站隧道客户端

> 上游仓库：https://github.com/openai/tunnel-client · 归类：Agent 框架与技能生态 · 本页基于 2026-09-21 的 README、官方 Secure MCP Tunnel 文档、architecture、permissions、release 与许可证静态整理；未创建 Tunnel、API key、connector 或长驻 daemon。

## 定位

`openai/tunnel-client` 是客户侧运行的 Secure MCP Tunnel 客户端：它从笔记本、VM、Kubernetes 或私有网络主动连接 OpenAI 托管的 tunnel endpoint，使 ChatGPT、Codex、Responses API 和 AgentKit 能访问不公开暴露的 MCP server。它解决的是连接与运维可见性，不是替 MCP 工具定义业务授权。

2026-09-21 的 GitHub 官方 Go Trending 抓取显示约 `+18 stars today`；REST API 快照为 `449 stars / 88 forks / 13 open issues`，Apache-2.0，最新 release 为 `v0.0.14`（9 月 1 日）。

## 用法

macOS 支持路径是 OpenAI Homebrew tap；直接下载的 ZIP 目前可能因未 notarize 被 Gatekeeper 阻止，上游明确不建议绕过系统检查：

```sh
brew install openai/tools/tunnel-client
tunnel-client --version
tunnel-client help quickstart
tunnel-client doctor --profile local-stdio --explain
tunnel-client run --profile local-stdio
```

首次使用需在 Platform 侧创建 Tunnel 与独立 Runtime API key，并赋予 Tunnels `Read + Use`；Admin key 仅用于管理命令，不应交给长驻 daemon。Codex 管理的长期 runtime 应使用 `runtimes connect` 和 `runtimes status`，而不是 `nohup`。

## 原理

- 客户侧 client 发起出站连接，MCP server 可继续绑定 localhost、Unix socket、stdio 或私网地址。
- OpenAI tunnel control plane 按 tunnel ID、角色 / 组和 runtime key 识别连接；ChatGPT connector 或 API 请求通过该通道到达 MCP。
- client 暴露 `/healthz`、`/readyz`、`/metrics` 与本地 UI，便于在依赖连接前检查 daemon、上游与 MCP 状态。
- Go SDK 可通过 in-memory transport 把 MCP server 与 tunnel client 放在同一进程，避免再开放本地端口。
- release 提供 checksum、SPDX sidecar、vulnerability report 与 Sigstore provenance；仓库中的 baseline SBOM 只证明基线文件本身，不等于某个 ZIP 的实际内容。

## 价值

- 无需新增公网入口或入站防火墙规则，就能连接已有私有 MCP 服务。
- 角色、组、Tunnel、Runtime / Admin key 与健康状态提供可运维的企业接入面。
- 配置、部署、权限、协议、排障和 release evidence 文档较完整，便于安全团队逐层审计。
- 同一 client 可覆盖前台 daemon、受管理 runtime、容器 / Kubernetes 和进程内 SDK。

## 风险边界

- “不暴露公网”不等于“工具不可被滥用”：一旦 connector 获准，MCP 的读写权限、参数校验、租户映射和人工审批仍由应用负责。
- Runtime API key、Tunnel ID、Admin key 与 MCP 后端凭据作用域不同；混用或把 Admin key 放进 daemon 会扩大 blast radius。
- stdio 部署同一 tunnel ID 只支持一个 active client；重启重叠会把初始化与后续调用送到不同 child。
- health / ready 表示连接条件，不证明工具结果正确、数据最小化、审计完整或业务副作用安全。
- 本页未验证组织权限、自助开通范围、ChatGPT connector、Responses API、断线恢复或 release provenance。

## 补充建议

1. 先用内置 stateless stub 和专用测试组织核验连接，再接只读、无敏感数据的 MCP server。
2. 将 Tunnel 管理、Runtime 使用和业务工具审批拆成不同角色；key 分环境、短周期轮换并保留撤销演练。
3. 对 MCP 工具实施 schema 校验、租户级授权、幂等、写前确认与写后回读，不把 tunnel 当成 authorization layer。
4. 生产部署固定 release，并验证 ZIP、SPDX sidecar、checksum 与 provenance；同时测试双实例重叠、断网、child 崩溃和 key 撤销。

## 参考资料

- 上游 README：https://github.com/openai/tunnel-client
- Secure MCP Tunnel 指南：https://developers.openai.com/api/docs/guides/secure-mcp-tunnels
- 架构：https://github.com/openai/tunnel-client/blob/master/docs/architecture.md
- 权限：https://github.com/openai/tunnel-client/blob/master/docs/permissions.md
- `v0.0.14` release：https://github.com/openai/tunnel-client/releases/tag/v0.0.14
- GitHub REST API：https://api.github.com/repos/openai/tunnel-client
- LICENSE：https://github.com/openai/tunnel-client/blob/master/LICENSE
