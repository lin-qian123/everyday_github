# mcpsnoop

<!-- markdownlint-disable MD013 MD012 -->

## 定位

`mcpsnoop` 是一个面向 Model Context Protocol 的透明代理调试器，项目自称“Wireshark for MCP”。它把真实 AI client 与 MCP server 之间的 JSON-RPC 帧放到可观察路径上，帮助排查工具没调用、参数错误、server 卡住、stderr 污染协议流等问题。

截至 2026-07-10 抓取时，GitHub 仓库约 `232` stars、`15` forks，主语言为 Go，许可证为 MIT。

## 用法

- 快速体验：`mcpsnoop demo`。
- stdio MCP server 可在客户端配置中用 `mcpsnoop -- <server command>` 包裹原 server 命令。
- streamable HTTP MCP server 可用 `mcpsnoop http --target http://localhost:3000/mcp --listen :7000` 做反向代理。
- 运行 `mcpsnoop` 打开 TUI，可查看 session、过滤 tool/method/status、重放调用、导出 JSON/HTML/text。

## 原理

`mcpsnoop` 同一个二进制承担两个角色：一端作为透明 shim 转发 client 与 server 的字节流，一端作为 hub/TUI 读取 socket 和磁盘日志。它位于真实数据路径中，不像 MCP Inspector 那样作为独立 client 连接 server，因此能看到 Cursor、Claude Code、Codex 等真实客户端实际发出的请求。

## 价值

- 对 MCP 开发者来说，能区分“模型没调工具”“客户端没暴露能力”“server 收到错误参数”和“server 处理慢”。
- 对 agent 用户来说，能把工具调用证据导出成 HTML/JSON，便于复盘和 issue 报告。
- 单二进制、无 runtime 依赖，适合临时插入已有 MCP 配置。
- 补齐 MCP 生态从“能连上”到“能调试真实会话”的 observability 层。

## 风险边界

- 它会捕获工具调用 payload，可能包含文件路径、账号信息或业务数据，导出前必须脱敏。
- 透明代理适合调试，不应在生产环境长期无治理运行。
- 对非标准 MCP 实现或特殊 transport，仍可能需要额外适配。
- 它解释的是协议帧，不替代 server 端日志、权限审计和业务语义检查。

## 补充建议

- 与 `mcphub`、`postman-mcp-server`、`open-connector` 一起观察，MCP 生态正在从 server 数量扩张转向调试、治理和凭据边界。
- 建议团队在 MCP server 模板中加入“如何用 mcpsnoop 复现问题”的文档段落。
- 对安全敏感工具调用，应配合日志保留周期、密钥过滤和导出审批。

## 参考资料

- GitHub 仓库：<https://github.com/kerlenton/mcpsnoop>
- MCP Inspector：<https://github.com/modelcontextprotocol/inspector>
- Go package：<https://pkg.go.dev/github.com/kerlenton/mcpsnoop>
