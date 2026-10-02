<!-- markdownlint-disable MD013 -->

# WebBrain（webbrain-one/webbrain）

> 上游仓库：<https://github.com/webbrain-one/webbrain> · 归类：Agent 框架与技能生态 · 本页基于 2026-10-03 的 GitHub API、README、architecture / security / privacy / prompt-injection 文档、package manifest、Release 与 LICENSE 静态整理，未安装浏览器扩展、登录真实网站或执行自动化任务。

- 抓取快照：1,184 stars、134 forks、16 open issues。
- 热度信号：GitHub JavaScript Trending 抓取时约 +18 当日 stars。
- 版本与许可：API 许可证字段为 `NOASSERTION`，根 LICENSE 明确 33.0.0 以后为 GPL-3.0-or-later；latest Release / tag 与 package 均为 `v38.0.13` / `38.0.13`。

## 定位

WebBrain 是 Chrome、Edge 与 Firefox 的开源侧栏式浏览器 Agent，可围绕当前页面问答，也可点击、输入、滚动、导航、上传、下载并执行多步流程。它支持托管默认模型、云 API、本地 OpenAI-compatible server 与 WebGPU，并可通过 MCP 把已登录的真实浏览器 session 交给 Claude Code、Codex、Cursor 等外部 Agent。

## 用法

普通用户可从浏览器商店安装；开发者用 Node 22、`npm install` 后构建 Chromium / Firefox 版本。Ask 模式只读，Act 增加页面交互，Dev 还暴露源码、样式、console、network 与可逆页面编辑。MCP 路径运行 `npx -y @webbrain/mcp-server`，再让 Chromium 扩展连接本地 WebSocket；本地模型可接 llama.cpp、Ollama、LM Studio、vLLM 等，云端则按 provider 单独配置。

## 原理

扩展优先把页面 accessibility tree 转为带 ref 的结构化上下文，按模型能力分为 compact / mid / full 工具集，再在 ask / act / dev 权限模式下循环计划、调用、检查结果和压缩上下文。MCP 只暴露高层 browser task，而不直接暴露约 50 个底层 primitive，以保留扩展内 permission gate；每个 tab 保存独立会话，并可选本地用户记忆与可复用 workflow。

## 价值

相较于无登录的 headless 抓取，WebBrain 能在用户已经通过 SSO、保有 cookie 的真实 tab 中读取 client-rendered 页面，同时把网站级 permission prompt、计划预览与工具层级放在同一界面。多 provider 与本地模型支持也便于在成本、隐私和能力间做显式选择。

## 风险边界

- 真实浏览器登录态意味着 Agent 可触达账号、cookie、表单、上传下载和敏感页面；侧栏、MCP bridge 与模式名都不是账户或 OS sandbox。
- 网页内容可包含 prompt injection；上游有专门防御文档和 permission gate，但也明确存在已知缺口，不能把恶意页面交给高权限长期自动运行。
- README 提供 `/dangerously-skip-permissions`；一旦绕过确认，错误模型决策或网页诱导可直接扩大真实副作用。
- 托管默认、云 provider 与“Share queries for research”会产生不同数据流；分享开关虽默认关闭且称已 scrub，仍应按 provider 检查 prompt、response、diagnostics 与排队清理。
- MCP 可复用已登录 browser profile；localhost WebSocket 及同用户进程、外部 coding agent、模型 provider 和浏览器扩展共同构成信任链。
- API 的 `NOASSERTION` 与根 GPL-3.0-or-later 需以根许可为准；扩展 bundle 集成 GPL Xapian/libzim，分发修改版要评估 copyleft 义务。

## 补充建议

使用专用、低权限浏览器 profile 和测试账号，先保持 Ask + local model；为 Act / Dev 逐站点 allowlist 域名、动作、下载目录和最大步数，不启用跳过权限。用带恶意指令、跨 iframe、shadow DOM、文件上传和交易确认的 fixture 测 permission gate 与停止 / 恢复；检查扩展 storage、MCP socket、provider 请求和分享队列后，再决定是否进入真实账号。

## 参考资料

- [GitHub 仓库](https://github.com/webbrain-one/webbrain)
- [GitHub REST API](https://api.github.com/repos/webbrain-one/webbrain)
- [README 与安装说明](https://github.com/webbrain-one/webbrain/blob/main/README.md)
- [Security model](https://github.com/webbrain-one/webbrain/blob/main/docs/security-model.md)
- [Prompt-injection defense](https://github.com/webbrain-one/webbrain/blob/main/docs/prompt-injection-defense.md)
- [Privacy and data flow](https://github.com/webbrain-one/webbrain/blob/main/docs/privacy-and-data-flow.md)
- [v38.0.13 Release](https://github.com/webbrain-one/webbrain/releases/tag/v38.0.13)
- [LICENSE](https://github.com/webbrain-one/webbrain/blob/main/LICENSE)
