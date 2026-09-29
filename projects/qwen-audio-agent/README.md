<!-- markdownlint-disable MD013 -->

# qwen-audio-agent（QwenAudio/qwen-audio-agent）

> 上游仓库：<https://github.com/QwenAudio/qwen-audio-agent> · 归类：语音、视频与多模态 · 本页基于 2026-09-30 的 GitHub API、README、架构 / backend / remote-access 文档、Privacy、Security Policy、Release 与 LICENSE 静态整理，未采集音视频、连接后台 Agent 或测量实时延迟。

- 抓取快照：2,819 stars、277 forks、11 open issues。
- 热度信号：GitHub JavaScript Trending 抓取时约 +15 当日 stars。
- 版本与许可：Apache-2.0；latest Release、tag 与 npm 说明均为 `v2.0.1` / `2.0.1`。

## 定位

qwen-audio-agent 是把实时语音前台与长时程后台 Agent 连接起来的 runtime。用户可以持续对话，把文件、代码、搜索或工具任务异步交给 OpenClaw、Claude Code、Codex、DeepSeek Harness 等 backend，并从桌面面板追踪多任务；它不是单一语音模型，也不等于全部处理都在本地。

## 用法

可用 `npm install -g qwen-audio-agent` 安装。默认示例使用阿里云 Bailian / Qwen Audio Realtime key，`AGENT_PROTOCOL` 选择后台 Agent；也可换成本地或兼容 voice frontend、ACP / A2A backend。桌面版支持本地唤醒、Gateway 和远程客户端；Gateway 默认仅监听本机，启用 `--lan` 后应只在可信局域网使用，跨网优先通过私有 Tailnet 或自建 HTTPS 反向代理。

## 原理

三层架构把实时 voice frontend、conversation / task coordinator 与后台 Agent 解耦：轻量对话留在前台，需要工具或持续处理的任务交给后台。backend 复用自身模型、MCP、skills、认证与工作目录；Gateway 保存 profile、长期记忆、任务状态和日志。前台 MCP、memory / knowledge provider 与视觉输入又形成独立数据流。

## 价值

它解决语音 Agent 常见的“执行任务时沉默”问题，让对话、状态播报和后台工作并行，并允许替换 voice provider 与 Agent backend。对无障碍交互、桌面生产力、客服或车载原型，统一 task card、实时打断和异步状态比简单的 STT → LLM → TTS 串行链更实用。

## 风险边界

- 默认麦克风音频、转写上下文和回复请求会发送至阿里云 Qwen Audio Realtime；改用其他 provider 时数据边界随之改变，“自部署 Gateway”不等于零外发。
- 后台 Agent 可继承模型、工具、MCP、文件和 shell 权限；语音确认容易被误听、打断或伪造，真实副作用仍需视觉回读和独立审批。
- 启用实时视觉时 JPEG 帧会送给当前 provider；memory、knowledge、搜索与远程 MCP 也可能接收对话、文档或音频片段。
- `--lan` 的 HTTP / WebSocket 不加密，不应转发公网；配对 token、Tailnet 与客户端连接都需单独撤销和审计。
- 本地 `~/.config/qwaudio/`、日志和 Electron 客户端目录卸载后不会自动删除；诊断日志虽做常见 secret 脱敏，仍可能含路径、session ID 和模型信息。
- Apache-2.0 只覆盖代码；模型、声音、输入内容、输出、provider 服务和示例资产可能有额外条款。

## 补充建议

先在无敏感文件的专用账户中，用授权音频、固定噪声 / 打断集和 mock tools 测试 VAD、延迟、取消、重试与误操作。为删除、发送、付款、代码写入等动作增加屏幕确认和二次验证；绘制 voice、backend、MCP、memory、knowledge 与 remote client 的数据流，设置最短保留期，并实测设备丢失后的凭据撤销。

## 参考资料

- [GitHub 仓库](https://github.com/QwenAudio/qwen-audio-agent)
- [GitHub REST API](https://api.github.com/repos/QwenAudio/qwen-audio-agent)
- [v2.0.1 Release](https://github.com/QwenAudio/qwen-audio-agent/releases/tag/v2.0.1)
- [Architecture Deep Dive](https://github.com/QwenAudio/qwen-audio-agent/blob/main/docs/architecture/deep-dive.md)
- [Backend Agents](https://github.com/QwenAudio/qwen-audio-agent/blob/main/docs/backends/overview.md)
- [Privacy](https://github.com/QwenAudio/qwen-audio-agent/blob/main/PRIVACY.md)
- [Security Policy](https://github.com/QwenAudio/qwen-audio-agent/blob/main/SECURITY.md)
- [LICENSE](https://github.com/QwenAudio/qwen-audio-agent/blob/main/LICENSE)
