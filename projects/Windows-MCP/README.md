<!-- markdownlint-disable MD013 -->

# Windows-MCP（CursorTouch/Windows-MCP）

> 上游仓库：<https://github.com/CursorTouch/Windows-MCP> · 归类：Coding Agents 与终端助手 · 本页基于 2026-10-09 的 GitHub API、README、manifest、security / transport、tool 与 analytics 源码静态整理，未在真实 Windows 登录态、注册表、文件或桌面应用上运行。

- 抓取快照：8,313 stars、923 forks、24 open issues。
- 热度信号：GitHub Python Trending 抓取时约 +411 当日 stars；最后 push 为 2026-10-08。
- 版本与许可：最新 Release / tag / manifest 均为 `v0.8.7` / `0.8.7`，MIT；本页固定审计 commit `b455c2766c63`。

## 定位

Windows-MCP 是在 Windows 7--11 上运行的 MCP server，用 UI Automation、IAccessible2、Win32 与可选截图把桌面状态暴露给 Agent，并提供 click、type、shortcut、application、filesystem、PowerShell、process、registry、clipboard、notification 等高权限工具。它服务 computer-use 与 QA，不是独立桌面沙箱。

## 用法

推荐经 `uvx windows-mcp serve` 使用 stdio；若必须 SSE / streamable HTTP，先绑定 loopback。远程绑定需同时配置 bearer auth、TLS、IP allowlist、host validation 与明确 CORS origin。默认所有 tools 开启，试用时应通过 `--tools` 只启 screenshot / snapshot / wait 等读面，按任务逐步增加 click / type，继续排除 PowerShell、registry、process 和 filesystem 写删。

## 原理

server 枚举窗口与 UIA tree，把控件 label / id / coordinate 和可选 screenshot 返回给模型，再把动作映射到鼠标、键盘、UIA、PowerShell、filesystem、registry 与 process API。浏览器 DOM mode 为 Chrome / Edge 与 Firefox 提供不同 accessibility 路径；control hook 通过用户鼠标接管信号暂停 AI，network middleware 处理 auth、allowlist、CORS 与 DNS-rebinding 边界。

## 价值

相较纯视觉 computer-use，它可返回结构化控件树和 DOM 文本，降低定位与 token 成本；同时保留 screenshot-first 路径处理无 accessibility 信息的界面。一个 MCP endpoint 覆盖传统桌面、浏览器和系统工具，也便于在测试自动化中组合观察、等待和动作。

## 风险边界

- server 与当前用户同权；PowerShell、filesystem 写删、process kill、registry 修改、clipboard 和键盘输入可直接破坏系统或泄露登录态。
- 默认所有 tools 启用；MCP client 的确认 UI 不是 OS 隔离，恶意网页、文档和应用文本可通过 prompt injection 诱导高权限动作。
- HTTP 远程面若用 `0.0.0.0` 而缺 auth、TLS、allowlist 或 host validation，会把桌面控制权暴露到网络。
- screenshot、UI tree、clipboard、日志和工具输出可能包含密码、token、聊天、客户信息与通知内容；视觉裁剪不保证脱敏。
- manifest 的匿名 telemetry 默认开启；源码使用 PostHog，记录 tool、client、时延、成功 / 失败，异常事件还可包含 exception 文本。
- README 的 0.2--0.5 秒延迟和“2M+ users”是上游主张，本轮未复核统计口径、设备矩阵或实际成功率。

## 补充建议

只在专用 Windows VM 与测试账户运行，准备快照回滚，关闭真实邮箱、密码管理器、云盘和生产 VPN。以 read-only tool allowlist 起步，动作前显示目标窗口 / 参数并要求人工确认；禁用 telemetry 或检查事件字段，远程面做端口扫描、DNS rebinding、auth、CORS 与失效 token 负测试。

## 参考资料

- [GitHub 仓库](https://github.com/CursorTouch/Windows-MCP)
- [GitHub REST API](https://api.github.com/repos/CursorTouch/Windows-MCP)
- [README 与远程安全](https://github.com/CursorTouch/Windows-MCP/blob/main/README.md)
- [MCPB manifest 与工具清单](https://github.com/CursorTouch/Windows-MCP/blob/main/manifest.json)
- [Server 配置](https://github.com/CursorTouch/Windows-MCP/blob/main/src/windows_mcp/infrastructure/config.py)
- [Analytics 源码](https://github.com/CursorTouch/Windows-MCP/blob/main/src/windows_mcp/infrastructure/analytics.py)
- [安全策略](https://github.com/CursorTouch/Windows-MCP/blob/main/SECURITY.md)
- [v0.8.7 Release](https://github.com/CursorTouch/Windows-MCP/releases/tag/v0.8.7)
