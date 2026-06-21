# mcphub（samanhappy/mcphub）

- GitHub: https://github.com/samanhappy/mcphub
- 官网: https://www.mcphub.app
- 文档: https://docs.mcphub.app/
- 记录日期: 2026-06-21 (Asia/Shanghai)

## 定位

`mcphub` 是一个集中管理多个 MCP Server 的统一入口层。它要解决的问题不是“再造一个 MCP server”，而是把多个 server、多个分组、多个客户端连接方式统一成一个可管理、可路由、可扩展的网关。

## 热度信号

1. GitHub API 在 2026-06-21 抓取时显示约 `2.2k stars`、`270 forks`，`updated_at` 为 `2026-06-20T17:49:47Z`。
2. 官方 README 直接把项目定义为 `A unified hub for centrally managing and dynamically orchestrating multiple MCP servers/APIs into separate endpoints`。
3. README 首页在功能列表中连续强调 `Centralized Management`、`Flexible Routing`、`Smart Routing`、`OAuth 2.0`、`Tool Result Compression`，说明它的关注点已经从 demo 进入网关化和生产化。

## 用法

### 1) 编写配置文件

README 的最小示例是创建 `mcp_settings.json`：

```json
{
  "mcpServers": {
    "time": {
      "command": "npx",
      "args": ["-y", "time-mcp"]
    },
    "fetch": {
      "command": "uvx",
      "args": ["mcp-server-fetch"]
    }
  }
}
```

### 2) 运行服务

官方推荐的 Docker 方式：

```bash
docker run -p 3000:3000 \
  -v ./mcp_settings.json:/app/mcp_settings.json \
  -v ./data:/app/data \
  samanhappy/mcphub
```

### 3) 连接客户端

README 给出的入口包括：

- `http://localhost:3000/mcp`
- `http://localhost:3000/mcp/{group}`

适合给 Claude Desktop、Cursor 等支持 MCP 的客户端统一接入。

## 原理

1. 它把多个 MCP server 收敛到一个 HTTP / SSE 网关层，减少每个客户端分别配置的负担。
2. 通过 group、路由和可见性控制，把“哪些工具暴露给哪个客户端”做成中心化配置。
3. `Smart Routing` 与结果压缩说明它不仅是转发器，还在尝试承担部分工具发现和响应治理职责。

## 价值

- 对 MCP server 越来越多的团队，`mcphub` 能明显降低接入和运维复杂度。
- 它代表了 MCP 生态从“单工具试玩”转向“多 server 编排与治理”的趋势。
- 如果要把 MCP 真正接入团队环境，认证、分组、压缩和无停机更新这类能力都比简单 demo 更重要。

## 风险边界

- 网关层越强，单点复杂度也越高；一旦配置错误，可能影响多个客户端和多个后端 server。
- `Smart Routing` 与压缩类功能如果调得过 aggressive，可能带来可解释性下降或工具选择偏差。
- 接入 OAuth、数据库和社交登录后，部署与安全边界会明显复杂于“本地跑两个 server”的轻量模式。

## 补充建议

1. 小规模使用时先从只做统一入口开始，不要一开始同时启用全部高级路由和认证能力。
2. 评估重点应放在：故障隔离、权限边界、工具暴露策略，以及客户端兼容性。
3. 如果你已经维护多个 MCP server，这个项目值得和 `modelcontextprotocol/servers`、`postman-mcp-server`、`chrome-devtools-mcp` 一起看，理解它在生态中的中间层位置。

## 参考资料

- https://github.com/samanhappy/mcphub
- https://www.mcphub.app
- https://docs.mcphub.app/
