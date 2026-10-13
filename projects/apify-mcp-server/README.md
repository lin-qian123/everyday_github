<!-- markdownlint-disable MD013 -->

# Apify MCP Server（apify/apify-mcp-server）中文解读

> 上游仓库：<https://github.com/apify/apify-mcp-server> · 归类：Agent 框架与技能生态 · 本页基于 2026-10-14 的 README、tool surface、telemetry / privacy 说明、Release、许可证与 GitHub REST API 静态整理；未登录 Apify、运行 Actor、抓取网站、付款或写入外部系统。

## 定位

Apify MCP Server 把 Apify Store 中数千个 scraper、crawler 和 automation Actor 暴露给 MCP client。它既提供托管 Streamable HTTP / OAuth 入口，也提供本地 stdio 包，并支持搜索 Actor、动态读取 schema、执行任务、读取 dataset / storage，以及显式启用 task、schedule、build、source 与通用 API 写操作。

## 用法

最小方式是在 MCP client 连接 `https://mcp.apify.com`，通过 OAuth 或 `APIFY_TOKEN` 认证；本地可运行 `npx @apify/actors-mcp-server`。默认 tool set 包含 actor discovery、文档搜索、RAG Web Browser 与 Web Fetch；生产配置应使用显式 `tools=` allowlist，不加载不需要的写入、支付或动态 Actor 能力。

## 原理

- server 读取 Actor input schema 并动态生成 MCP tool，让模型发现和调用 store 中的 Actor。
- Actor run 返回 run / storage metadata，结果再由 dataset 与 key-value store tools 分页读取。
- 支持 AGI prepaid token、x402 USDC 与 Skyfire 等 agentic payment；写工具和付费字段走单独校验 / redaction 路径。
- tool annotations 标记 read-only、destructive 与 open-world 倾向，但真正权限仍由 token、Actor 和 server 配置决定。

## 价值

- 用统一 MCP surface 复用成熟爬取、搜索、地图、电商和自动化 Actor，减少每个 Agent 重写 connector。
- schema discovery、run metadata 与 storage 分页比把抓取结果一次性塞入上下文更可控。
- hosted / stdio、OAuth / token 与显式 tool selection 为不同信任边界提供部署选择。

## 风险边界

- 默认遥测开启，stdio 还启用 Sentry；README 提供关闭方式，但关闭前不能假设 tool name、错误和环境 metadata 不外发。
- 请求与 Actor input 会发送到 Apify API；Actor 还可能访问社媒、地图、电商和任意网站，必须同时审查目标站点条款、个人数据与机器人访问规则。
- 动态发现不能证明 Actor 安全、合法、稳定或价格合理；`call-actor`、schedule、build、source、API write 与支付会产生真实外部副作用和费用。
- tool annotation 是提示性 metadata，不是可靠授权边界；prompt injection 可能诱导 Agent 选择高权限 Actor 或导出数据。

## 补充建议

- 从单一只读 Actor、测试 token、硬预算和固定 input schema 开始，关闭 telemetry，保存 run ID、费用和结果 provenance。
- 在模型外实现域名 / Actor allowlist、最大费用、最大结果量、PII redaction、写操作人工确认和写后回读。
- 对每个 Actor 分开记录 maintainer、版本、价格、网站授权、数据字段、保留期与删除方法，不以 Apify Store 收录替代审计。

## 参考资料

- GitHub 仓库：<https://github.com/apify/apify-mcp-server>
- GitHub REST API：<https://api.github.com/repos/apify/apify-mcp-server>
- `v0.18.0` Release：<https://github.com/apify/apify-mcp-server/releases/tag/v0.18.0>
- Hosted configurator：<https://mcp.apify.com>
- Apify MCP 文档：<https://docs.apify.com/platform/integrations/mcp>
- README telemetry / privacy：<https://github.com/apify/apify-mcp-server#-telemetry>
- LICENSE：<https://github.com/apify/apify-mcp-server/blob/master/LICENSE.md>
