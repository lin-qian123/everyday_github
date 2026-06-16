# postman-mcp-server（postmanlabs/postman-mcp-server）

- GitHub: https://github.com/postmanlabs/postman-mcp-server
- 产品页: https://www.postman.com/product/mcp-server/
- 记录日期: 2026-06-16 (Asia/Shanghai)

## 定位

`postman-mcp-server` 是 Postman 官方提供的 MCP Server，把工作区、集合、环境、API 定义和代码生成等能力开放给 AI agent。它不是“跑一次 Postman 测试”的小工具，而是把 Postman 整个 API 工作流接进 agent 生态。

## 热度信号

1. GitHub API 在 2026-06-16 抓取时显示约 `262 stars`、`77 forks`。
2. 官方 README 明确把它定位为连接 Postman 与 AI tools 的官方入口，并持续维护远程托管版与本地版两条路径。
3. 近期 GitHub 趋势页和 MCP Registry 都能看到该项目，说明 API 工具链正在加速向 MCP 化迁移。

## 用法

### 1) 远程模式

把下面地址加到支持 OAuth 的 MCP host：

```text
https://mcp.postman.com/minimal
```

如果需要更多能力，可切换到：

- `https://mcp.postman.com/code`
- `https://mcp.postman.com/mcp`

### 2) 本地模式

```bash
npx @postman/postman-mcp-server
```

如果要启用更大工具面：

```bash
npx @postman/postman-mcp-server --code
npx @postman/postman-mcp-server --full
```

本地模式通常需要配置 `POSTMAN_API_KEY`。

## 原理

1. 远程托管版通过标准 MCP 协议向 agent 暴露 Postman 能力。
2. 官方把工具面拆成 `Minimal`、`Code`、`Full` 三档，避免一上来就把 `100+ tools` 全塞给模型。
3. `Code` 模式额外偏向代码生成与 API 上下文消费，适合让 agent 基于接口定义产出客户端代码。
4. 远程版优先走 OAuth，本地版和 EU 区域则保留 API key 路线。

## 价值

- 对 API-first 团队很有意义，因为 agent 可以在同一上下文里读接口、改环境、生成代码和检查工作区对象。
- 相比“复制 OpenAPI 再喂给模型”，这种方式更接近真实工程工具链。
- 对 MCP 生态来说，它代表官方 SaaS 厂商开始把一整套产品能力以标准接口开放给 agent。

## 风险边界

- 如果给了过宽的 Postman 访问权限，agent 可能误改环境变量、集合结构或团队资产。
- `Full` 模式工具太多时，模型的工具选择质量会下降，增加误调用概率。
- 托管版更省事，但要评估 OAuth、远程调用和企业内部 API 资产的合规边界。

## 补充建议

1. 优先从 `Minimal` 开始，按任务逐步扩到 `Code` 或 `Full`。
2. 区分“只读设计审查”和“可写工作区自动化”两类配置，避免混用。
3. 把关键集合和环境做备份或版本化，降低 agent 误操作的恢复成本。

## 参考资料

- https://github.com/postmanlabs/postman-mcp-server
- https://github.com/mcp/com.postman/postman-mcp-server
- https://www.postman.com/product/mcp-server/
- https://learning.postman.com/docs/postman-ai-agent-builder/mcp-server/overview/
