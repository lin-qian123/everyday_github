# CodexBar

概览
CodexBar 是一款 macOS 菜单栏应用，用于展示 OpenAI Codex、Claude Code、Cursor、Gemini 等多家 AI 开发工具的使用额度与重置时间。它以“会话窗口 + 周度窗口”的双条形图形式呈现状态，避免在编码时频繁打开网页或 CLI 查看配额。

为什么值得关注
- 多平台额度集中可视化：同一菜单栏里就能看到多个供应商的会话/周度额度。
- 低打扰体验：无 Dock 图标、最小 UI、仅在需要时查看。
- 适合高频使用：帮助开发者避免突然撞到额度上限。

主要功能
- 多供应商状态条：Codex / Claude / Cursor / Gemini / Copilot / 等。
- 会话与周度额度进度条 + 重置倒计时。
- 错误/不可用状态提示（图标变暗、状态标记）。
- 内置 CLI（`codexbar`）便于脚本或 CI 查询。
- 可选 WidgetKit 小组件（镜像菜单卡片）。

如何工作（原理简述）
- CodexBar 优先读取本地 CLI/RPC 的使用信息（如 Codex / Claude CLI）。
- 对需要网页面板的数据，复用浏览器已登录会话的 cookie（Safari/Chrome/Firefox），不存储密码。
- 当 cookie 缺失时，回退到本地 CLI 输出。
- 主要逻辑本地执行，不需要持续上传敏感数据。

安装方式
- Homebrew：`brew install --cask steipete/tap/codexbar`
- GitHub Releases：下载预编译包
- Linux：提供 CLI 版本（不含菜单栏 UI）

快速上手
1. 安装并打开 CodexBar。
2. 进入 Settings → Providers，启用你使用的服务。
3. 若需网页面板额度信息，按提示授予读取浏览器 cookie 的权限。
4. 菜单栏会显示会话/周度条形图与重置时间。

适用人群
- 多平台 AI 编程助手重度用户。
- 需要清楚掌握额度与成本的个人或团队。

注意与权限
- 读取浏览器 cookie 仅用于已登录面板信息获取，不存储密码。
- 可能需要 Full Disk Access（针对 Safari cookie 导入）。

参考链接
- https://github.com/steipete/CodexBar
- https://codexbar.app/
