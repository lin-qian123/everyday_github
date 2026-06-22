# stitch-mcp（davideast/stitch-mcp）

- GitHub: https://github.com/davideast/stitch-mcp
- 官网: https://davideast.github.io/stitch-mcp/
- 记录日期: 2026-06-22 (Asia/Shanghai)

## 定位

`stitch-mcp` 是一个把 Google Stitch 生成的 UI 设计接入本地开发与 coding agent 工作流的 CLI / MCP 代理层。它的重点不是再做一个设计工具，而是把设计结果变成开发可消费的上下文、页面代码和站点骨架。

## 热度信号

1. GitHub API 在 2026-06-22 抓取时显示约 `913 stars`、`108 forks`，`updated_at` 为 `2026-06-21T01:27:23Z`。
2. GitHub Trending Developers 的 TypeScript 榜单在 2026-06-22 抓取时把 `stitch-mcp` 作为热门仓库展示。
3. 官方 README 直接把定位写成 `A CLI for moving AI-generated UI designs into your development workflow`，并明确支持 `VS Code`、`Cursor`、`Claude Code`、`Gemini CLI`、`Codex`、`OpenCode`。

## 用法

### 1) 初始化认证与 MCP 配置

README 的推荐入口是：

```bash
npx @_davideast/stitch-mcp init
```

它会处理 `gcloud`、OAuth 和 MCP 客户端配置。

### 2) 本地预览或生成站点

```bash
npx @_davideast/stitch-mcp serve -p <project-id>
npx @_davideast/stitch-mcp site -p <project-id>
```

前者用本地开发服务器预览全部屏幕，后者把设计页面映射成 Astro 站点骨架。

### 3) 让 coding agent 直接读取设计上下文

README 给出的 MCP 代理配置是：

```json
{
  "mcpServers": {
    "stitch": {
      "command": "npx",
      "args": ["@_davideast/stitch-mcp", "proxy"]
    }
  }
}
```

它还提供 `build_site`、`get_screen_code`、`get_screen_image` 这类更高层的虚拟工具。

## 原理

1. 它把 Stitch 平台里原本偏封闭的 HTML/CSS 设计结果拉到本地开发链路中。
2. 通过 CLI + MCP 代理的组合，一方面服务人类开发者做预览和导出，另一方面也服务 coding agent 做页面理解和实现。
3. `build_site` 这类虚拟工具说明它不满足于底层 API 透传，而是在尝试把设计交付抽象成更适合 agent 调用的动作。

## 价值

- 它代表了设计生成与代码生成之间的新接口层，不再只停留在“设计师给一张图，工程师手写还原”。
- 对前端 agent 工作流，这类桥接层比单纯截图识别更有工程价值，因为它保留了结构化设计上下文。
- 如果 Google Stitch 继续扩张，这类 MCP 包装层很可能会成为设计到代码链路中的标准中间件。

## 风险边界

- 它依赖 Stitch 平台、Google API 和认证链路，稳定性不完全由本仓库控制。
- 从 AI 设计直接生成代码骨架可以加速开发，但不自动保证组件语义、可访问性和工程结构合理。
- OAuth、API Key、项目计费与平台配额都会影响团队内的实际可用性。

## 补充建议

1. 先拿低风险营销页或内部工具页面试验，不要直接把复杂产品 UI 全量交给自动映射。
2. 评估时重点看三个点：设计变更回流是否顺畅、生成站点是否易于接管维护、agent 调用结果是否稳定。
3. 建议把它与 `openui`、`agent-native`、`chatbot-ui` 一起看，理解“设计上下文直接进入 agent 工作流”这条路线。

## 参考资料

- https://github.com/davideast/stitch-mcp
- https://davideast.github.io/stitch-mcp/
- https://github.com/trending/developers/typescript
