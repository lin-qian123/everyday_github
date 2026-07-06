<!-- markdownlint-disable MD013 -->

# herdr

## 定位

`herdr` 是一个面向 coding agents 的终端多路复用器。它把多个 agent 会话放进真实终端 pane、tab 和 workspace 中，并提供 agent 状态识别、持久会话、远程重连、socket API 和可复用 agent skill。

可以把它理解为“为 agent 时代重写的 tmux”：仍然运行在终端里，但额外理解 Claude Code、Codex、Copilot CLI、opencode、Devin CLI、Kimi Code、Hermes Agent 等 agent 的工作状态。

## 用法

基础安装：

```bash
curl -fsSL https://herdr.dev/install.sh | sh
```

也支持 Homebrew、mise、Nix 和 release 二进制。启动后运行：

```bash
herdr
```

常见操作包括：

- 在不同 pane 中启动不同 agent。
- 通过侧边栏观察 blocked、working、done、idle 状态。
- detach 后让 agent 继续运行，再从另一台机器或手机 SSH 回来 reattach。
- 使用 `herdr --remote` 连接远程服务器上的 herdr 会话。
- 通过 socket API 或 `npx skills add ogulcancelik/herdr --skill herdr -g` 让 agent 自己创建 pane、读取输出和订阅状态。

## 原理

`herdr` 采用 Rust 单二进制和后台 server / 前台 client 架构。每个 agent 仍运行在真实终端里，避免 GUI wrapper 对 TUI 渲染、键盘输入和远程使用的破坏。

它通过进程名匹配、终端输出启发式、集成插件和本地 socket API 获取 agent 状态。这样既能兼容普通 shell 程序，也能对常见 coding agent 提供更语义化的状态显示。

## 价值

- **多 agent 可视化**：不再靠记忆和窗口标题管理十几个长任务。
- **终端原生**：适合 SSH、服务器、远程开发环境和不想引入 Electron 控制面的用户。
- **持久运行**：关闭笔记本或断开连接后，任务不必结束。
- **agent 可编排**：socket API 让 agent 可以驱动 herdr，而不是只能被人手动管理。

## 风险边界

- 项目许可证标注为 AGPL-3.0-or-later + 商业许可，企业内部分发和修改需要评估合规。
- 状态识别依赖启发式和集成质量，不应把 blocked / done 状态当成可靠验收信号。
- 多 agent 并行会放大凭据、写权限和误操作风险，需要结合 worktree、权限隔离和明确任务边界。
- Windows 仍是 preview / beta 路径，跨平台一致性需要实测。

## 补充建议

- 与 `codex-plugin-cc`、`gastown`、`agterm` 一起评估：前者解决跨 agent 委派，后两者解决更高层的工作流和 workspace 管理。
- 在服务器上跑长任务时，把 herdr 与 git worktree、只读审查命令和最小权限 token 配套使用。
- 若团队要采用，先定义 agent 状态标签的人工验收规则，避免“done”被误解为测试已通过。

## 参考资料

- GitHub 仓库：<https://github.com/ogulcancelik/herdr>
- 官方站点：<https://herdr.dev>
- 文档：<https://herdr.dev/docs/>
- GitHub Trending：<https://github.com/trending>
