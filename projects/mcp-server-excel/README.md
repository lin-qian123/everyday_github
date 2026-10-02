<!-- markdownlint-disable MD013 -->

# ExcelMcp（sbroenne/mcp-server-excel）

> 上游仓库：<https://github.com/sbroenne/mcp-server-excel> · 归类：办公、商业与行业应用 · 本页基于 2026-10-03 的 GitHub API、README、architecture / privacy / security 文档、package manifest、Release 与 LICENSE 静态整理，未在 Windows / Excel 中运行 COM、VBA、Power Query、DAX 或 Python in Excel。

- 抓取快照：800 stars、90 forks、24 open issues。
- 热度信号：GitHub C# Trending 抓取时约 +6 当日 stars。
- 版本与许可：MIT；latest Release / tag 与根 changeset package 均为 `v2.1.3` / `2.1.3`，只支持最新已发布版本的安全修复。

## 定位

ExcelMcp 是让 AI 助手或脚本控制真实 Microsoft Excel 的 Windows-only 自动化工具组，提供 MCP Server、token 较省的 CLI、VS Code 扩展和 MCPB。它不是只改 `.xlsx` 压缩包的 parser，而是经 Excel COM API 操作工作簿，覆盖 Power Query、DAX、Power Pivot、PivotTable、chart、VBA、Python `=PY()` 等 Excel 原生能力。

## 用法

前提是 Windows、Excel 2016+ 与 interactive desktop，开始前需关闭已打开工作簿以获得 exclusive access。对话式客户端安装 MCP Server；coding agent / script 可安装 `excelcli`，后者用后台 daemon 保持 workbook session。两条入口共享 Core command，当前 README 统计 31 个 tools、326 个 operations。

## 原理

MCP Server 在进程内调用 ExcelMcp service；CLI 通过仅本机、按用户 SID 命名并受 ACL 约束的 Windows named pipe 连接 daemon。Core command 再调用真实 Excel COM object，因此公式计算、格式、宏、Data Model 和图表由 Excel 自身读写。release build 可发送经过结构化分类的匿名 invocation telemetry；返回给 AI 助手的 tool result 则受该助手的数据政策约束。

## 价值

对依赖 Power Query、Pivot、宏、格式和 Data Model 的工作簿，使用 Excel 原生执行链比纯文件库更接近人工操作结果；用户还能在真实 Excel 中即时检查并继续编辑。MCP 适合探索式对话，CLI 则把大量 schema 收敛为较小工具面，便于自动化和减少上下文成本。

## 风险边界

- 运行要求限制在 Windows + 已安装 Excel + 交互桌面，不能据 README 推断支持 macOS、Linux 或无人值守服务器。
- 工具按当前 Windows 用户权限读写文件并控制 Excel；同用户任意进程可连接 CLI daemon，named-pipe ACL 只隔离其他用户，不隔离同用户恶意程序。
- VBA 写入 / 执行需要用户启用 Excel 的 VBA project object model 信任；宏、外部连接、Power Query refresh 与公式都可能产生真实副作用。
- telemetry 默认行为应按构建与配置实测；上游称不含 workbook 内容、路径、参数和错误文本，但会把使用分类等指标发送到 Azure Application Insights。
- `formatMCode=true`、`formatDax=true` 会把代码发往第三方 formatter；Python in Excel 会把 Python 和引用单元格数据交给 Microsoft cloud，这些都不是纯本地处理。
- AI assistant 会收到所请求的 workbook result；ExcelMcp 的 privacy policy 不能覆盖 Claude、Copilot 或其他模型的保存、训练、地域和账号条款。

## 补充建议

固定 `v2.1.3`，在可丢弃 Windows VM、测试账号和不含真实业务数据的工作簿副本中试用；禁用 VBA trust、remote formatter、Python in Excel 和 telemetry，除非任务确实需要并完成单独审批。以 cell / formula / format / Pivot / query / macro 金标做写后回读和视觉检查，限制 allowlist 目录，为每次保存保留版本化副本与操作日志。

## 参考资料

- [GitHub 仓库](https://github.com/sbroenne/mcp-server-excel)
- [GitHub REST API](https://api.github.com/repos/sbroenne/mcp-server-excel)
- [README 与安装入口](https://github.com/sbroenne/mcp-server-excel/blob/main/README.md)
- [Architecture](https://github.com/sbroenne/mcp-server-excel/blob/main/docs/ARCHITECTURE.md)
- [Privacy policy](https://github.com/sbroenne/mcp-server-excel/blob/main/PRIVACY.md)
- [Security policy](https://github.com/sbroenne/mcp-server-excel/blob/main/SECURITY.md)
- [v2.1.3 Release](https://github.com/sbroenne/mcp-server-excel/releases/tag/v2.1.3)
- [LICENSE](https://github.com/sbroenne/mcp-server-excel/blob/main/LICENSE)
