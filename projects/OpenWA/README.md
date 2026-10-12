<!-- markdownlint-disable MD013 -->

# OpenWA（rmyndharis/OpenWA）中文解读

> 上游仓库：<https://github.com/rmyndharis/OpenWA> · 归类：办公、商业与行业应用 · 本页基于 2026-10-13 的 README、架构 / 安全文档、MCP 集成、Release、许可证与 GitHub REST API 静态整理；未扫码登录 WhatsApp、读取联系人或发送任何消息。

## 定位

OpenWA 是自托管 WhatsApp API gateway，将多 session、消息 / 媒体 / 联系人 / 群组、webhook、dashboard、API key、queue 和可选 MCP server 放在 NestJS 服务中，并可选择 SQLite / PostgreSQL、local / S3、disabled / Redis 等存储适配器。

## 用法

上游推荐 Docker 启动后从 `localhost:2785` 访问 dashboard / API / Swagger，创建 session、扫码登录并生成 API key。给 Agent 使用时可启用 MCP，并优先创建限制到特定 session 与 chat 的 viewer / operator token；发送、批量操作和群组管理应继续由外部审批层控制。

## 原理

- 每个 WhatsApp session 由隔离容器 / runtime 管理，核心服务负责 session lifecycle、API、webhook、audit 和 dashboard。
- operator / viewer key 可限制到指定 session 和 chat；admin key 保留全局管理能力。
- Docker socket proxy 缩小主服务直接访问 daemon 的面，但仍是高权限容器控制路径。
- MCP 将消息读取和发送能力映射成 Agent tools；plugin fabric 另行承载 Chatwoot、Typebot 等扩展。

## 价值

- 相比简单 bridge，提供多 session、细粒度 key、队列、存储后端、审计和生产部署文档。
- session / chat scope 能把共享账号中的 Agent 可见面压缩到有限联系人和群组。
- v0.24.0 有连续 Release、CI、Security Policy 和明确的非官方平台风险说明。

## 风险边界

- OpenWA 不是 Meta / WhatsApp 官方产品，README 明确警告账号限制、封禁和平台行为风险；合规与用户同意由部署者负责。
- viewer 仍可读取私聊和媒体，operator 可外发、转发、编辑、删除和批量发送；接入 LLM 后形成典型 prompt-injection / data-exfiltration 高风险组合。
- Docker socket proxy、session token、webhook、S3 / Redis / Postgres 和 plugin 都扩大凭据与供应链面；“沙箱插件”需要按实际容器权限验证。
- session / chat scope 不是意图验证，admin 未受限；默认全 session 语义和将来新 session 继承也需谨慎配置。
- 本报未验证客户端协议兼容、端到端加密边界、媒体保留、吞吐、恢复或封禁概率。

## 补充建议

- 只用专门测试号码起步，viewer 默认、单 session / chat allowlist，外发 tool 关闭；发送前要求用户即时确认并做写后回读。
- 不把未可信消息原文直接送入有外发 / 管理权限的 Agent；对 URL、附件、联系人和 tool output 做分区与注入测试。
- 生产环境隔离 Docker 控制面，轮换 API / webhook secrets，设置速率 / 批量上限、保留期、备份与异常发送熔断。

## 参考资料

- GitHub 仓库：<https://github.com/rmyndharis/OpenWA>
- GitHub REST API：<https://api.github.com/repos/rmyndharis/OpenWA>
- `v0.24.0` Release：<https://github.com/rmyndharis/OpenWA/releases/tag/v0.24.0>
- 安全设计：<https://github.com/rmyndharis/OpenWA/blob/main/docs/04-security-design.md>
- MCP 集成：<https://github.com/rmyndharis/OpenWA/blob/main/docs/24-mcp-integration.md>
- Plugin sandbox：<https://github.com/rmyndharis/OpenWA/blob/main/docs/30-plugin-sandboxing.md>
- LICENSE：<https://github.com/rmyndharis/OpenWA/blob/main/LICENSE>
