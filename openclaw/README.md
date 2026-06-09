# OpenClaw (openclaw/openclaw)

概览
OpenClaw 是一个开源、本地优先的个人 AI 助手与代理平台，运行在你的电脑或自建服务器上，并通过你常用的聊天应用（如 WhatsApp/Telegram/Slack/Discord/Teams/iMessage 等）触发真实任务。它强调“本地控制 + 可扩展工具”，让你的数据和操作尽量停留在本地环境。

核心能力
- 本地优先与自托管：运行在你的设备或自建环境，数据尽量留在本地。
- 多渠道聊天接入：支持多种聊天平台接入，随时通过聊天发起任务。
- 持久化记忆：跨会话保存上下文与偏好。
- 浏览器控制：可自动化网页任务。
- 插件/技能扩展：支持自定义技能与社区插件。
- 安全隔离：强调通过沙箱（如 Docker）降低风险。

原理与架构（基于公开说明的归纳）
OpenClaw 采用“聊天入口 + 本地控制平面 + 工具/技能”的架构：用户在聊天应用里发出指令，本地控制平面编排模型与工具执行任务，完成后回写结果。通过限制工具权限与可控接入点，减少数据外泄与误操作风险。

快速上手
1. 环境准备：安装 Node.js 22+。
2. 运行安装脚本：
   - macOS/Linux/WSL：`curl -fsSL https://openclaw.bot/install.sh | bash`
   - Windows PowerShell：`iwr -useb https://openclaw.ai/install.ps1 | iex`
3. 启动引导向导：`openclaw onboard --install-daemon`。
4. 连接通道并验证：`openclaw status`。

典型使用场景
- 个人效率：清理收件箱、管理日程、信息检索。
- 自动化与集成：通过插件把聊天入口变成跨工具的自动化入口。

安全与注意事项
- 权限即能力：只打开你真正需要的通道和工具权限。
- 不要直接暴露网关到公网，建议通过反向代理 + TLS 做访问控制。
- 定期更新与审计技能配置，避免插件滥用。

今日动态（信息源）
- OpenClaw 在 GitHub 今日趋势榜靠前，属于“本地优先 + 多渠道接入”的代表工具。
- 多家媒体关注其爆火与安全风险讨论，强调对权限与数据的谨慎配置。

参考链接
- https://www.openclawagent.ai/
- https://openclawbot.site/
- https://www.openclawdbot.org/
- https://openclawagent.net/
