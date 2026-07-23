# AgentBar

## 定位

`AgentBar` 是原生 macOS 菜单栏应用，用一个状态入口显示 Claude Code、Codex、Copilot 与 Antigravity 等 coding agent 会话，并可处理 Claude Code 权限请求。仓库创建于 2026-07-23，截至 2026-07-24 约 3 stars。

## 用法

在 macOS 12+ 上用项目脚本安装，或通过 Homebrew cask / 源码构建；重启新 agent 会话后，菜单栏会显示工作状态和待批准请求。安装前阅读脚本输出，确认其对 `~/.claude/settings.json`、`~/.codex/config.toml` 等配置的合并范围。

## 原理

应用通过各 agent 的 hook/notify 入口收集会话状态，以项目、分支和状态汇总显示。Claude Code 的权限操作可从菜单栏回传；安装器将 hook 写入相应配置，并保留已有 hook。

## 价值

- 减少多终端 agent 状态查看和权限批准的上下文切换。
- 本地运行、无遥测的声明对开发桌面工作流有吸引力。
- 代表 coding agent 正从 CLI 走向轻量控制面的趋势。

## 风险边界

- 菜单栏批准会改变人工确认的交互位置，仍应逐条阅读写权限、网络和命令请求。
- 安装脚本会修改多个 agent 配置文件；升级或卸载前应保留快照并检查 diff。
- 其他 agent 的支持程度随 hook 格式变化，不能假定全量兼容。

## 补充建议

先在测试仓库启用，并保留只读/沙箱审批策略。团队场景不应把菜单栏快捷批准当作生产凭据操作的授权流程。

## 参考资料

- GitHub：<https://github.com/michalstrnadel/AgentBar>
