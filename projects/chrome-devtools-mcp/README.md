# Chrome DevTools MCP

## 为什么是今天的热门
GitHub Trends 频道在今天的趋势推送中重点提到了 `chrome-devtools-mcp`，并给出了安装与用途摘要，显示其在日榜中热度上升。citeturn1search5

## 这是什么
`chrome-devtools-mcp` 是一个 MCP（Model Context Protocol）服务器，让编码类 AI 代理可以控制和检查一个真实运行中的 Chrome 浏览器，从而把 Chrome DevTools 的能力带给 AI。它支持自动化、深度调试与性能分析等场景。citeturn0search1

## 能做什么（关键能力）
- 性能洞察：调用 Chrome DevTools 录制性能 trace，生成性能分析线索。citeturn0search1
- 调试与排障：查看网络请求、控制台信息、截图等。citeturn0search1
- 可靠自动化：通过 Puppeteer 自动执行浏览器操作，并自动等待结果。citeturn0search1

## 工作原理（简述）
它作为 MCP Server 暴露工具接口，MCP 客户端（如各类编码助手）通过该接口驱动一个真实的 Chrome 实例；底层使用 Puppeteer 与 Chrome DevTools 协作完成自动化与诊断。citeturn0search1

## 快速上手
在 MCP 客户端配置中加入：

```json
{
  "mcpServers": {
    "chrome-devtools": {
      "command": "npx",
      "args": ["-y", "chrome-devtools-mcp@latest"]
    }
  }
}
```

使用 `@latest` 可以保证始终使用最新版本。citeturn0search1

## 关键配置项
- `--autoConnect`：自动连接到已开启远程调试的 Chrome（需要 Chrome 145+ 并在 `chrome://inspect/#remote-debugging` 中启用远程调试）。citeturn0search1
- `--browserUrl`/`-u`：连接到一个可调试的 Chrome 实例（如 `http://127.0.0.1:9222`）。citeturn0search1
- `--wsEndpoint`/`-w`：使用 WebSocket 端点连接（替代 `--browserUrl`）。citeturn0search1
- `--wsHeaders`：为 WebSocket 连接提供自定义 header（JSON 格式）。citeturn0search1

## 适合的使用场景
- 需要 AI 直接验证前端改动的真实性能与控制台报错
- 需要在真实浏览器环境里执行回归与可视化检查
- 需要可靠的、非“静态 HTML”层面的自动化测试

（以上为基于工具能力的场景归纳）citeturn0search1

## 安全与隐私提醒
该 MCP 服务器会让客户端访问浏览器内容并能修改 DevTools 中的数据，因此不应在敏感或隐私页面上进行联通测试，避免敏感信息泄露。citeturn0search1

## 参考链接

```text
https://github.com/ChromeDevTools/chrome-devtools-mcp
https://github.com/mcp/ChromeDevTools/chrome-devtools-mcp
https://t.me/s/githubtrending/15329
```
