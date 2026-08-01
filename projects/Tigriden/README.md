# Tigriden

## 定位

`Tigriden` 是以“监督 AI coding agents”为单一目标的轻量 macOS 桌面 IDE：每个项目目录有嵌入终端、文件树、编辑器与查看器，可并排运行 `claude`、`codex`、`gemini` 等终端 agent。截至 2026-08-02 的 GitHub API 快照：项目创建于 2026-08-01，约 4 stars、0 forks，MIT。

## 用法

macOS 可从 Release 下载通用应用，或使用稳定 Rust 执行 `cargo build --release` 后运行二进制。打开项目文件夹后，用可配置预设启动 terminal agent；Tigriden 负责展示、编辑与会话管理，不替用户配置模型、登录状态或项目权限。

## 原理

项目用 Rust、Slint UI、PTY/终端模拟和文件监视将“agent + 文件 + 编辑器”组合为每目录会话；实时树会随 agent 修改刷新，内置查看器覆盖图片、Markdown、CSV/TSV 与 PDF 文本。它没有 LSP、调试器或聊天面板，刻意保持为观察与干预层。

## 价值

- 为多目录、多 agent 的开发任务提供比终端复用器更直观的检查入口。
- 本地会话、文件树和轻量编辑器在同一窗口，可降低切换与遗漏成本。

## 风险边界

- README 以 macOS 为主要目标，Linux/Windows 未测试；新项目尚无长期兼容性证据。
- 可视化监督不等于权限隔离：agent 仍在用户 shell 与项目权限范围内执行。
- 未 notarize 的 app 需要用户显式处理 macOS 隔离属性，下载与构建均应核验来源与签名。

## 补充建议

先在无敏感仓库验证终端、文件刷新与撤销流程；配合 Git worktree、最小权限 token、独立测试命令和人工代码审查，而不是把 GUI 视为安全控制。

## 参考资料

- GitHub：<https://github.com/Sompote/Tigriden>
- Releases：<https://github.com/Sompote/Tigriden/releases>
- GitHub API 快照：<https://api.github.com/repos/Sompote/Tigriden>
