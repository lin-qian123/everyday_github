<!-- markdownlint-disable MD013 -->

# ai-usagebar（akitaonrails/ai-usagebar）

> 上游仓库：<https://github.com/akitaonrails/ai-usagebar> · 归类：Coding Agents 与终端助手 · 本页基于 2026-09-26 的 GitHub API、README、配置文档、Release 与 LICENSE 静态整理，未读取本机凭据、调用 provider endpoint 或安装桌面组件。

- 抓取快照：575 stars、122 forks、5 open issues。
- 热度信号：GitHub Rust Trending 抓取时约 +12 当日 stars。
- 版本与许可：MIT；latest Release / tag 为 `v1.25.0`。

## 定位

ai-usagebar 是用 Rust 实现的 AI 套餐 / 额度监控器，为 Waybar、Omarchy Quattro、GNOME、KDE、macOS / Windows tray 和 TUI 统一显示 Claude、Codex、Copilot、OpenRouter、GLM、Kimi、DeepSeek 等服务的用量、余额与重置时间。

## 用法

Linux 可用 Nix、AUR 或 crates.io，Windows / macOS 可使用 Release 或自行构建；安装后运行 CLI / TUI，并按 provider 复用官方 CLI 登录或显式配置 API key。默认只应启用确实需要的 provider，先用 `vendors --json` 查看认证方式和本机是否存在凭据，再以较低刷新频率验证一个账号。

## 原理

工具读取官方 CLI 的 OAuth / auth 文件、OS Keychain、环境变量或自身 `config.toml`，调用不同服务的 usage / billing endpoint，再把返回值规范化为额度窗口、余额和 reset。共享 cache、文件锁与 429 backoff 防止多个 widget 重复请求；部分 access token 会在刷新后写入权限受限的本地 cache。

## 价值

多 provider 用户可以在一个面板中看到费用和额度临界点，避免逐站登录与意外耗尽；TUI、tray、Waybar 和桌面 shell 的复用也让同一数据面覆盖不同工作站。其文档公开了凭据解析顺序、文件路径和已知 Keychain 问题，便于审计。

## 风险边界

- 工具可读取 Claude / Codex / GitHub / Antigravity 等高价值 OAuth、Keychain 和 CLI session；即便只查 usage，进程被替换或依赖被污染也会扩大凭据泄露面。
- 多个 provider 使用未公开或易变化的 endpoint；字段、限额分母、计费币种和 reset 可能变化，面板显示不能作为账单或服务承诺的唯一依据。
- macOS 文档记录 token write-back 曾改变 Keychain ACL，引发 Claude Code 重复授权提示；刷新行为可能影响拥有同一凭据的其他工具。
- config 内联 key、cache、日志、通知和自定义 endpoint 都需要文件权限与脱敏；`600` 只是本地权限基线，不防同用户恶意进程。
- 额度“剩余”不代表模型可用性、请求成功率或费用封顶，组织、team、预付余额和 subscription 的口径也可能不同。

## 补充建议

从专用低额度测试账号和单一 provider 开始，优先复用只读 / 管理端专用 key，不把生产组织 admin key写进配置。固定 `v1.25.0`，对照官方控制台记录 endpoint、刷新、cache 文件和 Keychain diff；将轮询间隔设为上游建议的保守值，并为未知字段、429、401、token rotation 与系统锁屏建立回归。

## 参考资料

- [GitHub 仓库](https://github.com/akitaonrails/ai-usagebar)
- [GitHub REST API](https://api.github.com/repos/akitaonrails/ai-usagebar)
- [v1.25.0 Release](https://github.com/akitaonrails/ai-usagebar/releases/tag/v1.25.0)
- [配置文档](https://github.com/akitaonrails/ai-usagebar/blob/main/docs/configuration.md)
- [Provider endpoints](https://github.com/akitaonrails/ai-usagebar/blob/main/docs/vendor-endpoints.md)
- [LICENSE](https://github.com/akitaonrails/ai-usagebar/blob/main/LICENSE)
