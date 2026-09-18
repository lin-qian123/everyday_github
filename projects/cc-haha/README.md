<!-- markdownlint-disable MD013 MD034 -->

# cc-haha：跨平台 Claude Code / Agent 桌面工作台

> 上游仓库：https://github.com/NanmiCoder/cc-haha · 归类：Coding Agents 与终端助手 · 本页基于 2026-09-19 的中英文 README、隐私与架构文档、release、LICENSE 与 REST API 静态整理；未安装桌面包、连接账号或执行 Computer Use。

## 定位

`cc-haha`（Claude Code Haha）把多会话、Worktree、Diff、浏览器预览、权限审批、多模型、MCP、SubAgent、Agent Teams、Computer Use、技能市场、H5 远程入口和多种 IM 渠道收进一个 Electron 桌面应用。它既是 Claude Code 的图形前端，也试图成为多个 Agent、provider 与远程入口的本地控制面。

2026-09-19 的 GitHub 官方 TypeScript Trending 抓取显示约 `+38 stars today`；REST API 快照为 `14,626 stars / 8,567 forks / 192 open issues`，MIT。最新 release 为 `v0.6.4`（9 月 17 日）。

## 用法

普通用户可从 Releases 下载 macOS、Windows 或 Linux 安装包，首次启动后选择模型 provider、API Key 和默认模型。源码开发使用 Bun：

```sh
bun install
cp .env.example .env
./bin/claude-haha
```

官方文档提醒 macOS 正式版应检查签名与公证；Windows 未签名包可能触发 SmartScreen。正式使用前应核对 release 资产、校验值、代码签名与上游发布说明，不应把“仍要运行”当作安全验证。

## 原理

- Electron + React / Vite 提供桌面 shell，Bun 驱动本地 CLI 与服务；Anthropic SDK、MCP 与 LSP 连接模型和工具。
- 每条会话可绑定当前 working tree 或新 Worktree，并在右侧显示文件 diff、活动、SubAgent 和模型请求 trace。
- 五档权限模式把工具调用和危险命令放到 GUI 审批，但也提供跳过权限模式；权限策略最终仍落到所启动 Agent 与本机用户权限。
- H5 与 Telegram、飞书、微信、钉钉、WhatsApp、企业微信、QQ、Slack 等渠道把远程消息路由到本机会话。
- Computer Use 通过截图、点击和键盘控制桌面；内置浏览器使用真实登录态与 Cookie。
- 隐私文档称项目本身不运营接收会话内容的后端，但模型、OAuth、MCP、IM、远程访问、网页、更新和上游运行时会按配置产生网络流量。

## 价值

- 用单一界面管理多会话、diff、审批和 Agent Teams，适合需要持续监督而不想只看终端日志的用户。
- Worktree 与分支入口降低并行任务相互覆盖的概率；本地 trace 便于排查卡死、失败和 provider 延迟。
- 同时支持官方账号、第三方 OpenAI-compatible endpoint、LM Studio 和 Ollama，便于比较不同模型与成本。
- IM、H5 与定时任务让长任务可远程观察和审批，适合个人工作站场景。

## 风险边界

- Worktree 只隔离 Git 文件视图，不隔离进程、网络、凭据、系统 keychain 或用户目录；Computer Use 与真实浏览器登录态进一步放大副作用。
- 选择“跳过权限”或远程批准命令会让 Agent 继承本机用户权限；必须防范 prompt injection、错误项目、误点和非幂等外部操作。
- 隐私文档明确提示词、附件、代码上下文、工具结果、认证信息和 IM 消息会发给所选第三方；“本地优先”不等于离线或零外发。
- API Key、OAuth token、会话、日志和记忆保存在本机；卸载不会自动删除 `~/.claude` 与系统应用数据目录。
- 技能市场、MCP、动态编排脚本和第三方 provider 构成多条供应链，界面显示“安全状态”不能替代源码、权限和网络审计。
- 本页未验证 release 签名、远程入口认证、IM 数据路径、Computer Use stop condition、模型 trace 脱敏或跨平台稳定性。

## 补充建议

1. 使用专用测试账号、浏览器 profile、低额度 provider key 与无敏感代码仓库，先从“询问权限”模式完成端到端试用。
2. 为 Worktree、H5、IM 和定时任务分别建立 allowlist；外部写入、上传、付款、发消息与删除必须人工确认并做写后回读。
3. 安装前验证 release 签名与 hash；禁用未使用的 MCP、技能、IM 渠道和非必要 telemetry 流量。
4. 定期导出并检查本地日志、会话和 token 存储位置，制定删除、备份和设备丢失后的凭据撤销流程。

## 参考资料

- 上游 README：https://github.com/NanmiCoder/cc-haha
- `v0.6.4` release：https://github.com/NanmiCoder/cc-haha/releases/tag/v0.6.4
- 隐私与联网说明：https://github.com/NanmiCoder/cc-haha/blob/main/docs/start/privacy.md
- 桌面架构：https://github.com/NanmiCoder/cc-haha/blob/main/docs/internals/desktop.md
- GitHub REST API：https://api.github.com/repos/NanmiCoder/cc-haha
- LICENSE：https://github.com/NanmiCoder/cc-haha/blob/main/LICENSE
