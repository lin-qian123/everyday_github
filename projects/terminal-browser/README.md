<!-- markdownlint-disable MD013 -->

# terminal-browser（zenbu-labs/terminal-browser）

> 上游仓库：<https://github.com/zenbu-labs/terminal-browser> · 归类：Coding Agents 与终端助手 · 本页基于 2026-09-27 的 GitHub API、README、Claude Code plugin 文档、Release 与 LICENSE 静态整理，未执行安装脚本、启动 Chromium 或访问真实登录态。

- 抓取快照：3,460 stars、157 forks、68 open issues。
- 热度信号：GitHub TypeScript Trending 抓取时约 +68 当日 stars。
- 版本与许可：MIT；latest Release / tag 为 `v0.11.1`，根 workspace 为 private monorepo。

## 定位

terminal-browser 是在终端画面内运行真实 Chromium 的浏览器，并提供兼容 `agent-browser` 风格的 action CLI，让 coding agent 与网页处于同一 terminal tab / split pane。它面向前端预览、远端 SSH 开发和 Agent 网页操作，而不是文本模式网页抓取器。

## 用法

上游提供 Homebrew 与 `curl ... | bash` 安装，随后可用 `terminal-browser open <url>`、`--split right`、`--ssh <host>`、`ls` 与 `action`。Claude Code plugin 需要 kitty graphics / unicode placeholders、实验性 function hooks 与额外配置；首次试用应优先使用固定 Release、空白浏览器 profile 和无敏感站点。

## 原理

Electron offscreen rendering 从 GPU 读取 Chromium 像素，再通过 kitty graphics protocol 把画面绘入终端。鼠标和键盘事件被转换为 Chromium synthetic events，部分触控板 / 系统输入由后台 Swift app 补充。外层 UI 用 Rust graphics engine 与 React custom renderer 绘制；SSH 模式让浏览器留在本机，仅把网络请求经远端代理。

## 价值

它让网页预览、DevTools、终端 Agent 和远程开发共享一个操作表面，减少 IDE / 浏览器来回切换。真实浏览器引擎也比字符浏览器更适合 canvas、复杂 CSS 和交互调试，action CLI 可把同一实例交给人工与 Agent 协作。

## 风险边界

- README 明确 Agent 可完整操作已打开的 browser；若复用真实 profile，cookie、账号、下载、剪贴板和表单提交都进入高权限范围。
- 浏览器控制面不是 sandbox；网页 prompt injection、恶意下载、OAuth、支付和 destructive action 仍需独立审批与 allowlist。
- `curl | bash`、自动 upgrade 和 browser binary 构成供应链面；应固定 tag、校验 artifact，并避免在生产终端直接安装。
- Claude Code plugin 依赖实验性 function hooks、local HTTP 和终端图形协议；上游已列出 50 FPS、mouse coordinate、multiplexer 与 TUI redraw 限制。
- SSH 模式只代理网络请求，不代表远端身份、内网访问或浏览器数据自动隔离；错误代理配置还可能扩大可达面。

## 补充建议

用独立 OS 用户和空白 Chromium profile，先验证静态本地站点、恶意页面、下载、popup、clipboard、file upload、OAuth 与 SSH localhost 访问。把 action CLI 置于域名 / 方法 allowlist 后面，默认禁止提交、购买、发布和账号改动；记录 Release、terminal、GPU、browser profile 与远端 proxy 配置以便复现。

## 参考资料

- [GitHub 仓库](https://github.com/zenbu-labs/terminal-browser)
- [GitHub REST API](https://api.github.com/repos/zenbu-labs/terminal-browser)
- [v0.11.1 Release](https://github.com/zenbu-labs/terminal-browser/releases/tag/v0.11.1)
- [Claude Code plugin 文档](https://github.com/zenbu-labs/terminal-browser/blob/main/claude-code-plugin/README.md)
- [agent action CLI](https://github.com/zenbu-labs/terminal-browser/tree/main/cli)
- [LICENSE](https://github.com/zenbu-labs/terminal-browser/blob/main/LICENSE)
