<!-- markdownlint-disable MD013 -->

# Microsoft MCP Servers（microsoft/mcp）

> 上游仓库：<https://github.com/microsoft/mcp> · 归类：Agent 框架与技能生态 · 本页基于 2026-09-27 的 GitHub API、README、server 目录、Release、Security Policy 与 LICENSE 静态整理，未登录 Azure / Fabric / Microsoft 365 或运行任何 MCP server。

- 抓取快照：3,715 stars、629 forks、306 open issues。
- 热度信号：GitHub C# Trending 抓取时约 +6 当日 stars。
- 版本与许可：MIT；多 server 独立发布，latest GitHub Release 为 `Azure.Mcp.Server-3.0.0-beta.47`，根 tags 还包含独立的 Template server alpha 版本。

## 定位

`microsoft/mcp` 是 Microsoft MCP server 的官方目录与共享工程仓库。源码部分当前包含 Azure MCP、Fabric MCP 和 Template MCP 的核心库、测试、pipeline 与 tooling；README 还索引 Microsoft / Azure 其他仓库、NuGet / npm 包及 remote MCP endpoints，因此它不是一个可一次安装的单体 server。

## 用法

用户应先按目标服务选择具体条目，再进入对应 README 确认 local / remote 类型、认证、preview 状态与安装方式。例如 Azure MCP 可与 VS Code、Visual Studio、IntelliJ、Eclipse 或 Claude Code 集成，Fabric server 有自己的 README / changelog / release。不要把根仓库 clone 后默认暴露全部工具，也不要把目录中的 install badge 当作统一授权。

## 原理

仓库为内置 server 共享 .NET core libraries、test frameworks、engineering systems 与 release pipeline，以减少各团队重复实现；各 server 再把 Azure / Fabric 等 API 映射为 MCP tools。根 README 同时承担 registry 功能，列出 local stdio、local package 与 remote HTTP endpoints，并把外部实现链接到各自仓库和文档。

## 价值

它提供了追踪 Microsoft 官方 MCP 能力、发布与文档的集中入口，也让 Azure / Fabric server 共享工程基础。对企业 Agent 来说，官方来源、独立 troubleshooting / support 文档和明确的 local / remote 标记，比从第三方目录猜测工具身份更可审计。

## 风险边界

- 根 README 是 catalog，不是所有条目的统一源码、许可、安全审计或 SLA；外链 server 必须回到各自仓库、服务条款和部署文档核验。
- Azure、SQL、Microsoft 365、Sentinel、Teams、SharePoint 等工具可能读取或修改高价值企业资源；MCP 传输协议不替代 Entra scope、RBAC、tenant、审批与 audit。
- local 与 remote server 的数据流、凭据位置、日志和 retention 不同；“官方”不等于最小权限或默认适合生产。
- latest Release 指向单个 Azure server beta，root tags 又含 Template alpha；根仓库没有可代表全部 server 的统一版本号。
- README 描述的 server、endpoint 与 preview 状态会持续变化，安装前必须固定文档时间、package / release 和 endpoint。

## 补充建议

建立 owner / server / transport / package / auth scope / data class / write capability 清单，只在非生产 tenant 逐个启用。先使用 read-only 或最小 RBAC，明确哪些 tools 能 create / update / delete / deploy / send；记录 MCP client、server version、tenant 与 audit ID。remote endpoint 还应核验 region、retention、DPA 与 incident response。

## 参考资料

- [GitHub 仓库](https://github.com/microsoft/mcp)
- [GitHub REST API](https://api.github.com/repos/microsoft/mcp)
- [Azure MCP server](https://github.com/microsoft/mcp/tree/main/servers/Azure.Mcp.Server)
- [Fabric MCP server](https://github.com/microsoft/mcp/tree/main/servers/Fabric.Mcp.Server)
- [Release 列表](https://github.com/microsoft/mcp/releases)
- [Security Policy](https://github.com/microsoft/mcp/blob/main/SECURITY.md)
- [LICENSE](https://github.com/microsoft/mcp/blob/main/LICENSE)
- [MCP specification](https://modelcontextprotocol.io/specification/latest)
