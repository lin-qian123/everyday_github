# playwright-mcp（microsoft/playwright-mcp）

- GitHub: https://github.com/microsoft/playwright-mcp
- 记录日期: 2026-04-24 (Asia/Shanghai)

## 这是什么

`playwright-mcp` 是 Microsoft 维护的浏览器自动化 MCP 服务器，让 AI 代理可通过结构化接口执行网页导航、交互与检查任务，适合测试、回归验证和可重复的 web 操作流水线。

## 热度信号

1. GitHub 页面显示约 `31.3k stars`、`2.6k forks`，增长非常快。
2. OSSInsight AI Trending（2026-04-24）将其列入 AI 热门仓库，说明“Agent + Browser Automation”已成为主线方向。

## 怎么用（最短路径）

### 1) 直接加入 MCP 配置

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["@playwright/mcp@latest"]
    }
  }
}
```

### 2) 常见工具链快速接入

- Claude Code: `claude mcp add playwright npx @playwright/mcp@latest`
- Codex: `codex mcp add playwright npx "@playwright/mcp@latest"`

### 3) 在任务中明确自动化目标

例如：登录校验、关键路径回归、表单提交流程录制与复现。

## 核心原理

1. 以 MCP 工具形式暴露浏览器操作，代理通过标准协议调用。
2. 依赖结构化页面表示（而非纯视觉截图）进行稳定交互。
3. 通过脚本化和可重放流程提升测试与验证可复现性。

## 适用场景

1. AI 驱动的端到端回归测试。
2. 发布前 smoke test 与关键业务流程巡检。
3. 需要把“网页操作”纳入 Agent 自动化链路的工程团队。

## 价值与风险

价值：
- 将浏览器动作标准化，减少手工回归时间。
- 可直接纳入代理工作流，提高“生成-验证”闭环完整度。

风险：
- 对动态页面和反自动化策略敏感，稳定性依赖站点实现。
- 误用高权限会话可能带来账号与数据风险。

## 我认为有价值的补充材料

1. 为不同站点维护 selector 健康检查，降低 UI 变动导致的脆弱性。
2. 将失败截图/日志统一归档，便于模型回溯修复。
3. 与 CI 的最小关键路径检查结合，优先保证高价值流程。

## 参考来源

- https://github.com/microsoft/playwright-mcp
- https://ossinsight.io/trending/ai
- https://playwright.dev/
