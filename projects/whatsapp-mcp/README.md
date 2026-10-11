<!-- markdownlint-disable MD013 -->

# WhatsApp MCP（lharries/whatsapp-mcp）中文解读

> 上游仓库：<https://github.com/lharries/whatsapp-mcp> · 归类：办公、商业与行业应用 · 本页基于 2026-10-12 的 README、Release、源码目录、许可证与 GitHub REST API 静态整理；未扫描二维码、连接个人 WhatsApp、读取消息或发送任何外部通信。

## 定位

WhatsApp MCP 把个人 WhatsApp 的联系人、聊天、消息与媒体暴露成 MCP tools，让 Claude Desktop / Cursor 等 host 可以检索历史、下载媒体并向个人或群组发送文本、文件和语音。它直接连接真实个人通信，因此价值和风险都远高于只读知识库 connector。

## 用法

先在 `whatsapp-bridge/` 运行 Go bridge，并用手机扫描二维码连接 multi-device session；再用 uv 启动 `whatsapp-mcp-server/` 下的 Python MCP server，把 stdio 配置写入 host。Windows 还需要 CGO 与 C compiler。消息历史保存在 bridge 的本地 SQLite store。

## 原理

- Go bridge 基于 `whatsmeow` 连接 WhatsApp Web multi-device API，处理登录、同步和消息收发。
- bridge 把联系人、聊天和消息写入 SQLite，并提供给 Python MCP server。
- MCP tools 覆盖 contact / chat / message search、context、send、download media 和 audio conversion。
- Agent 请求经 MCP → Go bridge → WhatsApp；读取结果沿反向链路进入模型上下文。

## 价值

- 将消息搜索、上下文回看和媒体处理统一成结构化 tools，减少 Agent 依赖屏幕操作。
- 本地 SQLite 便于离线检索、备份和明确数据位置。
- 上游 README 主动提示 prompt injection / data exfiltration 的“lethal trifecta”风险，没有把 MCP 接入描述成天然安全。

## 风险边界

- private messages + untrusted content + external send tool 构成高风险组合；消息中的恶意指令可能诱导模型读取其他聊天并向外发送。
- QR session、SQLite、下载媒体、MCP host 日志和模型上下文都包含敏感个人数据；“本地存储”不代表加密、最小可见或不进入 provider。
- 项目使用非官方 WhatsApp Web 库，可能受平台条款、协议变化、账号限制和重新认证影响。
- latest Release 仍为 2025-04-06 的 `v0.0.1`，仓库最后 push 为 2025-07-13；2026-10-12 的 Trending 热度不等于当前维护活跃或生产成熟。

## 补充建议

- 仅用专用测试账号与无敏感对话试验，默认禁用 send / file / audio tools，把每次外发置于独立人工确认。
- 将聊天内容视作不可信输入；对 recipients、group JID、media path 与消息正文做 allowlist、预览和发送后回读。
- 加密 / 隔离 SQLite 与 session 文件，限制 MCP host / provider 日志，并准备撤销 linked device 和清除本地 store 的流程。

## 参考资料

- GitHub 仓库：<https://github.com/lharries/whatsapp-mcp>
- GitHub REST API：<https://api.github.com/repos/lharries/whatsapp-mcp>
- `v0.0.1` Release：<https://github.com/lharries/whatsapp-mcp/releases/tag/v0.0.1>
- Go bridge：<https://github.com/lharries/whatsapp-mcp/tree/main/whatsapp-bridge>
- Python MCP server：<https://github.com/lharries/whatsapp-mcp/tree/main/whatsapp-mcp-server>
- whatsmeow：<https://github.com/tulir/whatsmeow>
- LICENSE：<https://github.com/lharries/whatsapp-mcp/blob/main/LICENSE>
