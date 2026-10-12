<!-- markdownlint-disable MD013 -->

# Unreal Engine Skills for Claude Code（EpicGames/unreal-engine-skills-for-claude-code-plugin）中文解读

> 上游仓库：<https://github.com/EpicGames/unreal-engine-skills-for-claude-code-plugin> · 归类：Agent 框架与技能生态 · 本页基于 2026-10-13 的 README、hooks、skills、setup / operations、许可证与 GitHub REST API 静态整理；未启动 Unreal Editor、MCP server、Live Coding 或修改任何 `.uproject` / asset。

## 定位

这是 Epic Games 发布的 Claude Code 插件，为 Unreal Engine 的实验性 MCP / AllToolsets 能力提供安装说明、上下文 hook 和 Agent skills。运行时可通过 30+ toolsets 操作 actor、Blueprint、material、mesh、animation、Sequencer、Niagara、UI、Gameplay Ability System、测试和编辑器脚本。

## 用法

插件可从 Anthropic 官方 marketplace 安装，也可在项目 `.claude/settings.json` 中启用。Unreal 工程还需显式开启 `ModelContextProtocol` 与 `AllToolsets`，启动 editor MCP server，并生成 `.mcp.json` / Codex 配置。默认 server 为 `localhost:8000/mcp`；Windows 的 SessionStart hook 另需 Git Bash 或 WSL。

## 原理

- SessionStart shell hook 向 Claude 注入 Unreal 项目类型、`.uproject` 与 MCP 配置状态。
- tool-search 模式只暴露 `list_toolsets`、`describe_toolset`、`call_tool`，按需发现并 server-side dispatch 大量编辑器工具。
- MCP server 在 editor 进程中调用 ToolsetRegistry；可选 proxy 缓存 tool catalog 并在 editor 重启时保持客户端连接。
- companion skills 规定 tool discovery、并发、compile、结果检查、project-specific skill 与 toolset authoring 流程。

## 价值

- 由 Epic 官方仓库给出 MCP 接入和安全说明，降低第三方 Unreal automation 文档的来源不确定性。
- 按需 tool discovery 控制 prompt / cache 负担，同时保留 Blueprint、资产、测试与 Live Coding 的统一入口。
- setup 明确区分“插件已安装”“MCP 已连接”“proxy 有缓存”和“Unreal 实际可达”，有利于避免假成功。

## 风险边界

- MCP 在编辑器权限内可创建、修改、移动或删除大量 `UObject` 和磁盘资产；部分操作跨编译边界不可可靠 undo。
- `ProgrammaticToolset.execute_tool_script` 可在 editor 进程执行任意 Python；localhost 与 origin validation 不能防同用户恶意进程。
- `--dangerously-skip-permissions` 会移除逐 tool 审批；不可信 prompt 或素材可能迅速扩大为全工程写入。
- proxy 连接或缓存 catalog 不证明 editor 正常，也不证明工具调用成功；每次变更必须检查具体返回和工程 diff。
- 仓库只包含 skills / hooks，不包含完整 Unreal MCP runtime；引擎版本、实验插件可用性与 marketplace 版本必须成套固定。

## 补充建议

- 只在工程副本中启用，开始前 commit / shelve，限制 toolset，关闭跳过权限，并串行执行会触及同一 asset 的调用。
- 首先做 read-only actor / asset 列表验证，再做单资产编辑、compile、save、reopen、diff 与运行测试。
- MCP 仅绑定 loopback；共享机器上禁用 server，审计 generated client config、proxy binary、Python 脚本与 editor log。

## 参考资料

- GitHub 仓库：<https://github.com/EpicGames/unreal-engine-skills-for-claude-code-plugin>
- GitHub REST API：<https://api.github.com/repos/EpicGames/unreal-engine-skills-for-claude-code-plugin>
- Unreal MCP skill：<https://github.com/EpicGames/unreal-engine-skills-for-claude-code-plugin/blob/main/skills/unreal-mcp/SKILL.md>
- 首次设置：<https://github.com/EpicGames/unreal-engine-skills-for-claude-code-plugin/blob/main/skills/unreal-mcp/references/setup.md>
- 运行与恢复：<https://github.com/EpicGames/unreal-engine-skills-for-claude-code-plugin/blob/main/skills/unreal-mcp/references/operations.md>
- LICENSE：<https://github.com/EpicGames/unreal-engine-skills-for-claude-code-plugin/blob/main/LICENSE>
