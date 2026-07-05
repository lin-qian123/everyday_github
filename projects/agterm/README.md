# agterm

## 1. 定位

`agterm` 是一个面向 agentic flow 的 macOS 原生终端。它不是直接内置一个 coding
agent，而是围绕多项目、多会话、多 agent 并行工作重新组织终端窗口、workspace、
session、overlay 和通知。

在 coding agent 越来越多地以长时程 shell session 运行之后，传统 tabbed terminal
很难判断哪个 agent 正在执行、哪个阻塞、哪个完成。agterm 的价值就在于把终端变成
agent 会话控制面。

## 2. 基本用法

预构建版本面向 Apple Silicon macOS 14+，可通过 Homebrew cask 安装：

```bash
brew install --cask umputun/apps/agterm
```

应用内 Help 菜单提供三类可选安装：

- 安装 `agtermctl` 命令行工具。
- 安装 agent status hooks，让 Claude Code、Codex 等把 active、blocked、
  completed 状态显示在 session 行上。
- 安装 agent skill，让 Claude Code 或 Codex 学会通过 `agtermctl` 管理布局、
  overlay、窗口和 inline image。

## 3. 核心原理

agterm 底层使用 Ghostty 的 libghostty 负责终端渲染、VT parsing 和 shell I/O。
它在上层增加自己的 workspace/session 模型、control API、CLI、scratch terminal、
quick terminal、overlay 和 agent status。

`agtermctl` 通过本地 Unix domain socket 控制应用，可以创建 session、发送输入、
运行 overlay 程序、调整窗口和发送通知。这使得人类脚本和 agent 都可以编排终端
布局，而不需要直接操作 UI。

## 4. 工程价值

agterm 解决的是“多个 agent 同时跑时，人类如何保持控制感”的问题。对频繁使用
Claude Code、Codex、OpenCode、Cursor agent 的用户来说，状态标记、workspace
分组、overlay 和脚本化控制比单纯换一个终端主题更有价值。

它也说明 coding agent 生态正在倒逼开发工具重构：终端不再只是 shell 容器，而是
长任务协调、状态提示和人机交接界面。

## 5. 风险边界

agterm 本身不是安全沙箱。agent 在其中执行命令时，权限仍取决于本机 shell、项目
目录和模型工具配置。安装 status hooks 或 skill 后，agent 能够更主动地控制终端，
应当先确认 `agtermctl` 暴露能力是否符合自己的安全预期。

此外，当前预构建包主要面向 Apple Silicon macOS，跨平台用户不能直接假设可用。

## 6. 补充建议

- 用 workspace 对应项目或客户环境，避免多个 agent session 混在同一视图。
- 给生产环境 session 使用醒目的命名和主题，减少 agent 误操作风险。
- 将 blocked/completed 状态作为人工介入提醒，而不是自动信任完成结论。
- 与 `Godcoder`、`orca`、`workbench-cli` 比较：agterm 更像终端层控制面，不是完整
  coding agent。

## 7. 参考资料

- GitHub 仓库：<https://github.com/umputun/agterm>
- 官网：<https://agterm.com>
- 关键技术：Swift、libghostty、`agtermctl`
