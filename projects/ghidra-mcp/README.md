<!-- markdownlint-disable MD013 -->

# Ghidra MCP（bethington/ghidra-mcp）

> 上游仓库：<https://github.com/bethington/ghidra-mcp> · 归类：Coding Agents 与终端助手 · 本页基于 2026-10-08 的 GitHub API、默认 `dev` 分支 README、安全 / Docker 文档与源码静态整理，未加载未知二进制、运行 Ghidra script、连接 debugger 或共享 Ghidra Server。

- 抓取快照：4,764 stars、222 forks、48 open issues。
- 热度信号：GitHub Java Trending 抓取时约 +192 当日 stars；最后 push 为 2026-10-07。
- 版本与许可：latest Release `v6.0.0`，首个 tag `v7.0.0-rc.1`，Apache-2.0；本页固定审计 commit `1d8fc95dbfc2`。

## 定位

Ghidra MCP 把 Ghidra GUI plugin、独立 headless server 与 Python MCP bridge 组合成 200+ 逆向工具，覆盖反编译、符号 / 类型、批量注释、项目版本、BSim、debugger 和脚本管理。它面向已授权逆向与内部软件分析，不提供目标许可或恶意样本安全保证。

## 用法

先在可丢弃 VM 安装与当前 Ghidra 兼容的固定 release，导入公开测试二进制副本；MCP 优先使用 stdio，或仅在 `127.0.0.1` 使用 streamable HTTP。启用 lazy tool group 与 README 给出的 minimal read-only allowlist，设置 `GHIDRA_MCP_REQUIRE_PROGRAM_SELECTORS=1`；只有明确需要时才单独打开 script、filesystem 或共享 server 能力。

## 原理

Java plugin / headless server 在本机 HTTP 暴露 Ghidra Program、Listing、Decompiler、DataType、Project 等 API，Python bridge 将 catalog 转换为 MCP tools，并支持按组 lazy load。GUI 与 headless 覆盖并不完全相同；可选 debugger proxy 和 Ghidra Server 工具又扩展了进程 / 共享仓库权限。

## 价值

它让 Agent 以地址、函数、引用、反编译结果和批量操作为结构化对象，而不是靠截图或手工复制；strict selector、只读 allowlist、默认关闭 script 与 file root 提供了可组合的收敛手段。Headless 与 Docker 路线也利于在固定样本上做可复现批处理。

## 风险边界

- 工具包含 rename、delete、import、project 管理、server permission、checkout 终止、debugger 控制与 script 执行；完整 catalog 远非只读分析。
- localhost 默认无认证，只适合可信单用户工作站；非 loopback 必须配置 bearer token，但 TLS、网络 ACL、日志脱敏和 secret 轮换仍由部署者负责。
- `GHIDRA_MCP_ALLOW_SCRIPTS` 打开后可在 Ghidra 进程中执行任意 Java / Ghidra script；分析恶意样本时这不是 sandbox。
- 多 client 共享“当前 program”可能把写操作落到错误二进制；strict program selector 能拒绝缺失目标的调用，但仍需 workspace 隔离和回读。
- `GHIDRA_MCP_FILE_ROOT` 只约束相关 filesystem-path endpoint；项目数据库、Ghidra Server、debugger 与脚本权限是独立边界。
- latest Release 仍是 v6.0.0，而默认分支 / 首个 tag 已进入 v7 RC；部署必须固定一套 Ghidra、plugin、bridge 和 schema，不能混用 README head。

## 补充建议

采用“样本哈希 → VM snapshot → 只读导入 → minimal tools → 人工批准写入 → 导出 diff”的流程；无真实凭据、无生产共享 server、默认断网。分别记录 Ghidra、Java、plugin、bridge、sample 与 project 版本，并用第二种分析器 / 人工证据交叉验证 Agent 结论。

## 参考资料

- [GitHub 仓库](https://github.com/bethington/ghidra-mcp)
- [GitHub REST API](https://api.github.com/repos/bethington/ghidra-mcp)
- [默认分支 README](https://github.com/bethington/ghidra-mcp/blob/dev/README.md)
- [安全策略](https://github.com/bethington/ghidra-mcp/blob/dev/SECURITY.md)
- [Docker 文档](https://github.com/bethington/ghidra-mcp/blob/dev/docker/README.md)
- [连接排障](https://github.com/bethington/ghidra-mcp/blob/dev/docs/connection-triage-guide.md)
- [v6.0.0 Release](https://github.com/bethington/ghidra-mcp/releases/tag/v6.0.0)
- [v7.0.0-rc.1 Tag](https://github.com/bethington/ghidra-mcp/tree/v7.0.0-rc.1)
