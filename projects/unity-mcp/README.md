<!-- markdownlint-disable MD013 -->

# unity-mcp（CoplayDev/unity-mcp）

> 上游仓库：<https://github.com/CoplayDev/unity-mcp> · 归类：Agent 框架与技能生态 · 本页基于 2026-09-30 的 GitHub API、README、tool / multi-instance / remote-auth 文档、package manifest、Release、Security Policy 与 LICENSE 静态整理，未打开 Unity、修改工程或验证 47 个工具入口。

- 抓取快照：14,603 stars、1,525 forks、99 open issues。
- 热度信号：GitHub C# Trending 抓取时约 +32 当日 stars。
- 版本与许可：MIT；latest Release / tag 为 `v10.2.0`，`beta` 分支 Unity package manifest 为 `10.2.1-beta.6`。

## 定位

MCP for Unity 是连接 Claude、Codex、VS Code、本地模型等 MCP client 与 Unity Editor 的桥梁。它把场景 / GameObject、资源、C# 脚本、测试、profiling 和 build 等编辑器操作组织成 47 个聚焦 tool entrypoints，目的是让 Agent 在真实项目中执行而不只生成代码片段。

## 用法

要求 Unity 2021.3 LTS 至 6.x 和 Python 3.10+ / `uv`。在 Unity Package Manager 中添加 Git URL，可固定 `#v10.2.0`；然后通过 Window → MCP for Unity → Configure All Detected Clients 配置本机 MCP client。默认应使用 loopback transport。多 Unity instance、tool group 和 remote-hosted server 需要额外 routing / auth 配置，正式项目应先在副本或分支试运行。

## 原理

Unity package 在 Editor 内注册 typed 工具与资源 / 场景操作，Python MCP server 负责协议和 client 连接；tool call 进入 Editor 后调用 Unity API，再把结构化结果返回模型。Roslyn 路径用于脚本验证，多实例 routing 避免请求落到错误 Editor。远端模式在 loopback 默认之外增加认证，但仍要由部署者负责网络边界。

## 价值

对 Unity 项目，Agent 最困难的不是写一段 C#，而是把资源、层级、序列化、导入、测试和构建结果闭环。MCP for Unity 将这些动作置于可枚举工具表面，并允许直接运行测试 / profiler；这比单纯复制聊天代码更接近可验证工作流。

## 风险边界

- 工具本来就会修改场景、资源、脚本和项目设置；MCP 协议与 typed schema 不保证生成内容正确、可运行或符合版本控制意图。
- Editor tool 继承 Unity 进程对项目和本机的权限；来自 asset、console、README 或模型上下文的 prompt injection 可能诱导错误调用。
- 默认 loopback 是较安全起点，但 remote server、LAN bind、代理和 token 会扩大攻击面；认证不替代 TLS、防火墙、速率限制和撤销测试。
- Release `v10.2.0` 与 beta manifest `10.2.1-beta.6` 不同；main、beta、Unity package 和 Python server 必须作为一个兼容矩阵固定。
- “run tests”不等于验证画面、物理、性能、平台构建、资产权利或玩家体验，生成的 scene / prefab 仍需人工 review。
- MIT 不自动覆盖 Unity、Asset Store 内容、模型 provider、生成资产和第三方包。

## 补充建议

对生产项目创建可丢弃副本、独立分支和定期 checkpoint，只给 Agent 启用当前任务所需 tool group。每次调用记录目标 Unity instance、输入参数与变更 diff；脚本通过 Roslyn 后仍运行 EditMode / PlayMode、目标平台构建和人工场景检查。远端模式使用短期 token、TLS、IP allowlist 与专用低权限主机。

## 参考资料

- [GitHub 仓库](https://github.com/CoplayDev/unity-mcp)
- [GitHub REST API](https://api.github.com/repos/CoplayDev/unity-mcp)
- [v10.2.0 Release](https://github.com/CoplayDev/unity-mcp/releases/tag/v10.2.0)
- [Tool Catalog](https://coplaydev.github.io/unity-mcp/reference/tools)
- [Multi-Instance Routing](https://coplaydev.github.io/unity-mcp/guides/multi-instance)
- [Remote Server Auth](https://coplaydev.github.io/unity-mcp/guides/remote-server-auth)
- [Security Policy](https://github.com/CoplayDev/unity-mcp/blob/beta/SECURITY.md)
- [LICENSE](https://github.com/CoplayDev/unity-mcp/blob/beta/LICENSE)
