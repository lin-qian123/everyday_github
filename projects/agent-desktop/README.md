<!-- markdownlint-disable MD013 MD034 -->

# agent-desktop：基于系统无障碍树的 Agent 桌面控制 CLI

> 上游仓库：https://github.com/lahfir/agent-desktop · 归类：Coding Agents 与终端助手 · 本页基于 2026-09-21 的 README、Concepts、release、许可证与 REST API 静态整理；未安装二进制、授予 macOS 权限或执行真实桌面动作。注意它与仓库已收录的 Solo.io `agentdesktop` 不是同一项目。

## 定位

`lahfir/agent-desktop` 是面向通用 AI Agent 的桌面自动化 CLI / Rust 库。它优先读取 macOS Accessibility tree，用带 snapshot 身份的 element refs 观察和操作原生应用；截图、物理鼠标与 CDP 是补充路径，而不是把所有界面动作都退化成像素坐标猜测。

2026-09-21 的 GitHub 官方 Rust Trending 抓取显示约 `+41 stars today`；REST API 快照为 `1,334 stars / 88 forks / 22 open issues`，Apache-2.0，最新 release 为 `v0.9.2`（9 月 17 日）。

## 用法

上游推荐通过 npm 安装预构建二进制；macOS 需要按功能授予 Accessibility、Screen Recording 和 Automation 权限：

```sh
npm install -g agent-desktop
agent-desktop permissions
agent-desktop snapshot --app Finder -i --compact
agent-desktop click @s8f3k2p9:e3
```

复杂应用可先做 skeleton snapshot，再按局部 ref 深入；高后果操作前应固定 session、保存 trace，并在动作后重新 snapshot 回读状态。

## 原理

- platform adapter 将 macOS Accessibility 元素规范化为带 role、name、bounds 与稳定证据的树。
- snapshot 生成带 ID 的命名空间；qualified ref 同时包含 snapshot 与 element 身份，避免并发或新快照下把裸序号误用到另一元素。
- 动作前执行 visibility、stability、enabled、supported action、policy 与 editability 等 actionability 检查；歧义目标返回错误而不是任意点击。
- session 把多进程 trace、截图和 refs 收到同一运行记录；多 Agent 仍须为各自快照 pin qualified refs 并协调共享桌面。
- Chromium 应用可由 `launch --cdp` 暴露只绑定 `127.0.0.1` 的 DevTools endpoint；原生菜单、窗口和系统对话框继续走无障碍路径。

## 价值

- 结构化树和 JSON error contract 比纯视觉坐标更适合可重试、可审计的 Agent loop。
- skeleton / scoped traversal 可压缩密集桌面 UI 的上下文体积；上游给出的 78--96% token 降幅仍需在目标应用复现。
- CLI、C ABI 与 bundled skill 可让不同语言和 Agent 宿主复用同一操作协议。
- trace export、session namespace 和 stale-ref recovery 为桌面任务提供比“录屏证明”更细的过程证据。

## 风险边界

- Accessibility、Screen Recording、Automation 与 CDP 都是高权限能力；结构化 refs 不会自动限制 Agent 可读、可写或可发送的内容。
- 默认 headless 只减少静默焦点 / 鼠标副作用，不等于 OS sandbox、应用级授权或业务动作审批。
- 本地 `127.0.0.1` CDP endpoint 对同用户本地进程仍可达；会话 trace 和截图可能包含密码、通知、客户信息或私有代码。
- macOS 是当前完整支持面，Windows / Linux 多项能力仍标为 planned；跨平台包存在不等于功能等价。
- 上游 token 降幅、稳定 ref 与安全重试是项目自报能力，本页未在 Finder、Slack、VS Code 或系统对话框上实测。

## 补充建议

1. 从专用 macOS 测试用户、无真实账号的副本应用和只读动作开始，逐项授予权限。
2. 为 delete、send、publish、purchase、credential 等后果性动作增加外部 policy gate 与人工确认。
3. 每次动作保存前后 snapshot、command、result 与窗口身份；遇到 `STALE_REF` 或 `AMBIGUOUS_TARGET` 先重观测，不盲目重试。
4. 将 trace / screenshot 当敏感日志管理，设置脱敏、最小访问、TTL 和安全删除。

## 参考资料

- 上游 README：https://github.com/lahfir/agent-desktop
- Concepts：https://github.com/lahfir/agent-desktop/blob/main/CONCEPTS.md
- 安全策略：https://github.com/lahfir/agent-desktop/blob/main/SECURITY.md
- `v0.9.2` release：https://github.com/lahfir/agent-desktop/releases/tag/v0.9.2
- GitHub REST API：https://api.github.com/repos/lahfir/agent-desktop
- LICENSE：https://github.com/lahfir/agent-desktop/blob/main/LICENSE
