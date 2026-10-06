<!-- markdownlint-disable MD013 -->

# REA（morluto/rea）

> 上游仓库：<https://github.com/morluto/rea> · 归类：Coding Agents 与终端助手 · 本页基于 2026-10-07 的 GitHub API、README、安装 / 安全文档与 manifest 静态整理，未分析真实第三方程序、启动浏览器场景或运行 Hopper / Ghidra / IDA。

- 抓取快照：9,133 stars、1,002 forks、101 open issues。
- 热度信号：GitHub 综合与 TypeScript Trending 抓取时约 +2,963 当日 stars；最后 push 为 2026-10-06。
- 版本与许可：GitHub Release / npm manifest 均为 `rea-agents-4.1.0` / `4.1.0`，MIT；本页固定审计 commit `472b72a53068`。

## 定位

REA 是面向 Coding Agent 的逆向工程 CLI 与 MCP：把原生二进制、JavaScript / Electron、.NET、APK、固件和网页运行行为的检查统一成证据驱动工作流，再把观察、推断、限制与未知项一并交回 Agent。它不是自动恢复原始源码或一键克隆产品的工具。

## 用法

上游推荐 `npx rea-agents setup`，由交互式计划为选中的 Agent 注册 MCP 与匹配 skill；静态 JavaScript 检查也可直接运行 `npx -y rea-agents@4.1.0 analyze-javascript-application /absolute/path/to/app --json`。原生分析需自备兼容的 Hopper、Ghidra 或 IDA；采用前应固定版本与目标副本，先跑 `doctor --json`，逐项审阅 setup 将修改的配置和可选安装。

## 原理

CLI / MCP 把目标交给不同 provider adapter：静态 provider 读取文件与结构，Hopper / Ghidra / IDA 提供反汇编和伪代码，CDP 工具被动观察已运行网页，Playwright 场景则按声明动作捕获运行行为。结果可保存为带制品身份、位置、provider、置信度和限制的 Evidence / snapshot；本地 bridge 使用随机 capability token 与当前用户 socket，但上游明确这不是 sandbox。

## 价值

它把“找到字符串”提升为可追踪的调查链：函数、交叉引用、运行捕获、差分与未解决问题都能进入同一证据模型。静态 JavaScript 路径无需执行目标，snapshot 也利于复核同一字节和同一参数下的结论，适合合法的软件互操作、内部审计和已授权迁移研究。

## 风险边界

- 逆向工程受软件许可、著作权、反规避条款、商业秘密与司法辖区影响；必须先确认目标所有权、书面授权和允许用途，不能把“本地分析”当法律授权。
- setup 会修改 Agent 配置并可在明确同意后安装 Hopper；`curl ... | bash` 浮动安装路径不适合生产，宜固定 npm 版本或 commit 并核对变更计划。
- capability token、私有 socket、临时项目和资源限制只缩小意外暴露；同一 OS 用户下的恶意进程、解析器漏洞和被分析的恶意制品仍可突破这些边界。
- 被动 CDP 可接触真实页面状态，受控 Playwright / Electron / process capture 会执行目标和动作；真实账号、Cookie、下载、网络副作用与测试环境必须隔离。
- 伪代码、调用关系与运行相关性都不是原始源码或因果证明；缺失观察应保留为 unknown，不能自动补成“功能相同”。
- 仓库 `main`、npm 包和外部 provider 版本可能错位；Hopper、Ghidra、IDA、JADX、Binwalk 等还各有独立许可与供应链。

## 补充建议

只在可丢弃 VM / 低权限用户与目标副本中使用，先从无执行的 JavaScript fixture 和公开测试二进制开始；为每次调查保存目标哈希、REA / provider 版本、操作清单、Evidence 与人工复核结论。浏览器与动态分析使用专用 profile、关闭生产凭据和出站网络，交付中将“静态观察、动态观察、分析推断、实现选择”分栏记录。

## 参考资料

- [GitHub 仓库](https://github.com/morluto/rea)
- [GitHub REST API](https://api.github.com/repos/morluto/rea)
- [README 与调查模型](https://github.com/morluto/rea/blob/main/README.md)
- [安装说明](https://github.com/morluto/rea/blob/main/docs/installation.md)
- [安全策略与边界](https://github.com/morluto/rea/blob/main/SECURITY.md)
- [MCP 合约](https://github.com/morluto/rea/blob/main/docs/mcp-contracts.md)
- [Browser observation](https://github.com/morluto/rea/blob/main/docs/browser-observation.md)
- [4.1.0 Release](https://github.com/morluto/rea/releases/tag/rea-agents-4.1.0)
