<!-- markdownlint-disable MD013 MD034 -->

# fastmcp

`PrefectHQ/fastmcp` 是一个用 Python 快速构建 MCP servers 和 clients 的框架。它把 Python 函数声明、schema 生成、transport、认证、生命周期和客户端连接封装起来，让开发者专注工具逻辑。

- GitHub：https://github.com/PrefectHQ/fastmcp
- 文档：https://gofastmcp.com
- PyPI：https://pypi.org/project/fastmcp/
- 分类：Agent 框架与技能生态
- 许可证：Apache-2.0

## 热度信号

- 2026-07-15 通过 GitHub API 抓取时约 `26.2k stars`、`2.1k forks`。
- 仓库在 2026-07-14 仍有 push，topics 覆盖 `mcp`、`mcp-servers`、`mcp-clients`、`model-context-protocol`。
- README 声称 FastMCP 1.0 曾并入官方 MCP Python SDK，独立项目仍在维护。

## 定位

FastMCP 是 MCP 工具生态的 Python 开发入口。对多数团队来说，写 MCP server 的难点不在“让模型调用一个函数”，而在 schema、协议、transport、认证、错误处理和生产部署。FastMCP 试图把这些默认做好。

## 用法

最小示例：

```python
from fastmcp import FastMCP

mcp = FastMCP("Demo")

@mcp.tool
def add(a: int, b: int) -> int:
    """Add two numbers"""
    return a + b

if __name__ == "__main__":
    mcp.run()
```

安装通常从文档或 PyPI 开始：

```bash
pip install fastmcp
```

## 原理

FastMCP 的核心抽象包括：

- servers：把 Python 函数、资源和 prompts 暴露给 MCP client。
- clients：连接本地或远程 MCP server。
- apps：让工具具备可交互 UI 表面。
- transport / auth / lifecycle：框架处理协议细节，开发者写业务逻辑。

它的工程价值在于让 MCP server 代码更接近普通 Python 应用，而不是手写 JSON-RPC 胶水。

## 价值

- 降低 MCP server 原型门槛。
- Python 生态友好，适合数据、自动化、内部工具团队。
- 同时覆盖 server 和 client，方便做端到端测试。
- 与 Prefect 的背景结合，后续可能加强部署、治理和观测。

## 风险边界

- MCP server 一旦暴露写操作，风险不在框架本身，而在工具权限和输入校验。
- 框架生成 schema 不代表语义安全，仍要写清楚副作用。
- 生产部署需要额外考虑身份、网络边界、审计日志和速率限制。
- MCP 生态变化快，版本兼容性要固定并测试。

## 补充建议

- 从只读工具或内部查询工具开始练手。
- 给每个 tool docstring 明确副作用、失败条件和权限要求。
- 在 CI 里启动 MCP server 并跑客户端调用测试。
- 与 `awesome-mcp-servers`、`chrome-devtools-mcp`、`playwright-mcp` 配套看，区分“框架”和“具体工具 server”。

## 参考资料

- GitHub 仓库：https://github.com/PrefectHQ/fastmcp
- 文档：https://gofastmcp.com
- PyPI：https://pypi.org/project/fastmcp/
- MCP 官网：https://modelcontextprotocol.io/
