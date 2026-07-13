<!-- markdownlint-disable MD013 MD034 -->

# Browser Harness

- GitHub: https://github.com/browser-use/browser-harness
- 分类：前端、UI 与 Agent 交互层
- 主要语言：Python
- 抓取日期：2026-07-14

## 定位

`browser-harness` 是 Browser Use 团队推出的浏览器 agent harness。它让 LLM 通过 Chrome DevTools Protocol 直接连接真实浏览器，把站点操作、helper 函数和 domain skill 作为可编辑工作区逐步沉淀。

GitHub API 样本显示该项目约 `15.9k stars`，创建于 2026-04-17，topics 包括 `browser-agent`、`browser-automation`、`playwright`、`persistent-browser`、`web-automation`。

## 用法

README 建议把安装提示直接交给 Claude Code 或 Codex，例如要求 agent 使用 `uv` 安装稳定版、注册 `browser-harness skill`，并连接本地浏览器。之后用户需要在 Chrome 远程调试设置中允许连接。

典型工作流：

1. 安装 `browser-harness`。
2. 连接本地 Chrome/Chromium CDP endpoint，或使用 Browser Use Cloud 浏览器。
3. 让 agent 执行具体网站任务。
4. agent 在 `agent-workspace/agent_helpers.py` 中补 helper。
5. 成功经验沉淀到 `agent-workspace/domain-skills/`，用于后续相同站点。

## 原理

该项目的设计重点是“薄 harness + 可编辑技能层”：

- 核心包保持较小，负责连接浏览器、提供页面状态和执行能力。
- helper 文件由 agent 在运行中补齐，解决上传文件、表单操作、复杂选择器等具体问题。
- domain skills 记录站点级流程，避免每次重新探索 UI。
- 通过真实浏览器而非模拟 DOM，让 agent 能处理登录态、扩展、复杂前端和实际网络环境。

## 价值

- 对 GUI agent：比纯 Playwright 脚本更适合探索性任务，也比黑盒浏览器自动化更容易审计。
- 对 coding agent：把浏览器验证、网页操作、账号登录态和站点知识接进开发循环。
- 对团队：domain skill 可以成为可复用资产，记录“某个网站如何稳定完成某个操作”。

## 风险边界

- 连接真实浏览器意味着 agent 可能看到登录态、Cookie、隐私页面和内部系统。
- 远程调试端口暴露不当会造成严重安全风险。
- 自动沉淀的 domain skill 需要审查，避免把敏感选择器、账号路径或内部 URL 提交到公开仓库。
- 对金融、支付、社交账号等站点，必须保留人工确认。

## 补充建议

- 使用专门的测试浏览器 profile，不要连接日常主浏览器。
- 为每个任务限定目标域名和允许动作。
- 把生成的 domain skill 作为代码审查对象，而不是默认可信资产。
- 与 `Browser-BC`、`page-agent`、`Agent-S` 对照观察：一个偏实际浏览器 harness，一个偏能力蒸馏，一个偏页面/GUI agent 框架。

## 参考资料

- GitHub 仓库：https://github.com/browser-use/browser-harness
- Browser Use Cloud：https://cloud.browser-use.com/
- Browser Use 项目：https://github.com/browser-use/browser-use
