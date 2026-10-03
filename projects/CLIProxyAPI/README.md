<!-- markdownlint-disable MD013 -->

# CLIProxyAPI（router-for-me/CLIProxyAPI）

> 上游仓库：<https://github.com/router-for-me/CLIProxyAPI> · 归类：模型、训练与推理基础设施 · 本页基于 2026-10-04 的 GitHub API、README、v8 配置模板、SDK / management 文档、Release 与 LICENSE 静态整理，未登录任何模型账户、导入 OAuth 凭据、启动代理或发送请求。

- 抓取快照：54,034 stars、8,186 forks、666 open issues。
- 热度信号：GitHub Go Trending 抓取时约 +168 当日 stars。
- 版本与许可：MIT；latest Release / tag 为 `v8.0.13`，配置模板 schema 为 `8`。

## 定位

CLIProxyAPI 是把 Codex、Claude Code、Gemini / Antigravity、Grok Build、Kimi、Muse、Devin 与其他 OpenAI-compatible provider 统一成 OpenAI / Responses、Gemini / Interactions 和 Claude-compatible API 的 Go 代理。它支持多个 CLI / OAuth 账号、轮询、session affinity、failover、协议翻译和嵌入式 SDK。

## 用法

用户按官方指南启动 server，完成各 provider 的 OAuth / API-key 登录，再给下游客户端配置本代理 URL 与 client API key。v8 配置可控制 listener、TLS、管理 API、credential 并发、路由、session affinity、重试、cooldown、proxy、header passthrough 和 payload rewrite；Management API / TUI 可管理配置与账号池。

## 原理

代理加载多个 provider credential，把下游 OpenAI / Gemini / Claude 请求翻译成对应上游协议，再按轮询、权重、会话绑定、账号可用性和 cooldown 选择凭据。流式 / 非流式 / WebSocket、tool call 与多模态在 translator 层转换；失败时可跨凭据重试，子 Agent 可继承父 session 绑定以复用 prompt cache。

## 价值

对需要在多种客户端与多个 provider 之间复用协议的团队，它减少每个工具分别维护 OAuth、格式转换、failover 和账号池的成本；Go SDK 也允许把认证、路由和 translator 嵌入自有服务，而非只能部署独立 proxy。

## 风险边界

- 这是高价值凭据集中层：OAuth token、API key、prompt、tool payload、响应和 quota 状态可能通过同一进程；应假设代理主机失陷会扩大到全部已导入账号。
- v8 模板的 `server.host` 默认空字符串，会绑定全部 IPv4 / IPv6 interface，TLS 默认关闭；若沿用默认并暴露端口，client API 与模型流量可能进入局域网或公网攻击面。
- remote management 默认关闭且 management key 必填，但错误反代、弱 key、控制面资产自动下载或误开远程管理仍可能暴露账号池和配置。
- OAuth 登录可运行不等于 provider 条款允许把个人订阅转换为通用、多用户或商业 API；多账号轮询、代理、配额绕行和账号共享必须回到每家当前条款确认。
- 协议翻译、payload override、自动重试与跨账号 failover可能改变 tool schema、stream、error、usage、conversation state 和模型语义；兼容 endpoint 不证明行为等价。
- README 包含大量赞助 relay 与第三方面板；项目列出不等于安全、隐私、账单或官方渠道背书。

## 补充建议

固定 `v8.0.13`，只在独立低权限主机上绑定 `127.0.0.1`，为每个客户端发独立 key；远程使用应置于 mTLS / VPN 后并保持 management 关闭。先用无敏感数据的单账号验证协议、tool、stream、重试和账单，再逐 provider 增加；把 credential 文件、日志和备份纳入 secret 管理，并书面核对订阅 / OAuth 的允许用途。

## 参考资料

- [GitHub 仓库](https://github.com/router-for-me/CLIProxyAPI)
- [GitHub REST API](https://api.github.com/repos/router-for-me/CLIProxyAPI)
- [README 与功能概览](https://github.com/router-for-me/CLIProxyAPI/blob/main/README.md)
- [中文 README](https://github.com/router-for-me/CLIProxyAPI/blob/main/README_CN.md)
- [v8 配置模板](https://github.com/router-for-me/CLIProxyAPI/blob/main/config.example.yaml)
- [Management API 文档](https://help.router-for.me/management/api)
- [SDK 用法](https://github.com/router-for-me/CLIProxyAPI/blob/main/docs/sdk-usage.md)
- [v8.0.13 Release](https://github.com/router-for-me/CLIProxyAPI/releases/tag/v8.0.13)
- [LICENSE](https://github.com/router-for-me/CLIProxyAPI/blob/main/LICENSE)
