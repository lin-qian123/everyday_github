<!-- markdownlint-disable MD013 -->

# CC GUI（zhukunpenglinyutong/jetbrains-cc-gui）中文解读

> 上游仓库：<https://github.com/zhukunpenglinyutong/jetbrains-cc-gui> · 归类：Coding Agents 与终端助手 · 本页基于 2026-10-15 的中英文 README、Codex / MCP / settings 源码入口、SECURITY、Release、JetBrains Marketplace、许可证与 GitHub REST API 静态整理；未安装插件、连接真实 CLI / provider 或验证其权限提示与会话恢复。

## 定位

CC GUI 是 IntelliJ 平台插件，为 Claude Code、OpenAI Codex、Grok / Kimi / OpenCode / PI / OMP CLI 等提供统一图形界面。它把对话、文件引用、图片、diff、代码跳转、历史会话、Agent / skills、MCP、provider 与使用统计放进 IDE，属于现有高权限 CLI 的交互层，而不是新的模型或 sandbox。

## 用法

普通用户可从 JetBrains Marketplace 安装 `CC GUI（Claude, Codex and More）`，再只启用一个已登录的 CLI，在无敏感测试仓库中检查工作目录、文件引用、permission dialog、diff 和 session 保存。开发者可分别安装 webview / ai-bridge 依赖，并用 Gradle `runIde` 在 JetBrains sandbox 调试。

## 原理

- IntelliJ plugin 负责项目 / editor context、文件跳转、设置、MCP marketplace、权限提示和会话容器。
- webview 提供聊天、diff、MCP 与配置 UI；Node `ai-bridge` 连接不同 CLI 并适配它们的事件与会话格式。
- Codex / Claude settings manager 可读写 provider、MCP、prompt、skill、working directory 与 session template。
- 当前 manifest / Gradle 版本为 `0.5.9`，声明兼容 JetBrains build `233` 到 `263.*`。

## 价值

- 对偏 IDE 的开发者，能把终端 Agent 的多轮会话、文件上下文与 diff 审阅拉回同一界面。
- 多 CLI adapter 有助于比较不同宿主，而不用为每个工具重新学习完整交互层。
- 权限弹窗、MCP 状态和 Git diff 若实现正确，可让高风险动作比裸终端更可见。

## 风险边界

- GUI 不会收窄底层 CLI 的文件、shell、网络、MCP 或 provider 权限；“允许”按钮也不是 OS 隔离或副作用证明。
- 插件会管理用户 / 项目配置、provider credentials、MCP server 与历史会话，形成集中敏感面；第三方 marketplace / registry 还增加供应链风险。
- 多个引擎仍处 Beta，适配层可能误解析 approval、tool state 或恢复点；6999 stars 与 528 个 open issues 只能说明公开关注和维护负荷，不能推断稳定性。
- 项目由社区维护，不应把名称中的 Claude / Codex 当成 Anthropic / OpenAI 官方插件背书。

## 补充建议

- 用专用 JetBrains profile 和无 secrets 仓库试用，逐项记录插件文件、配置、子进程、端口和网络访问；先禁用 MCP marketplace 自动安装。
- 为同一只读任务比较 GUI 与原 CLI 的 tool log、approval、diff 和会话恢复，验证 UI 没有漏报或扩权。
- 固定 Marketplace `0.5.9` 与 checksum，备份配置；升级前审阅 changelog、安全记录和新增 provider / MCP 权限。

## 参考资料

- GitHub 仓库：<https://github.com/zhukunpenglinyutong/jetbrains-cc-gui>
- GitHub REST API：<https://api.github.com/repos/zhukunpenglinyutong/jetbrains-cc-gui>
- JetBrains Marketplace：<https://plugins.jetbrains.com/plugin/29342-cc-gui-claude-or-codex->
- `v0.5.9` Release：<https://github.com/zhukunpenglinyutong/jetbrains-cc-gui/releases/tag/v0.5.9>
- 中文 README：<https://github.com/zhukunpenglinyutong/jetbrains-cc-gui/blob/main/README.zh-CN.md>
- Codex 集成：<https://github.com/zhukunpenglinyutong/jetbrains-cc-gui/tree/main/docs/codex>
- SECURITY：<https://github.com/zhukunpenglinyutong/jetbrains-cc-gui/blob/main/SECURITY.md>
- LICENSE：<https://github.com/zhukunpenglinyutong/jetbrains-cc-gui/blob/main/LICENSE>
