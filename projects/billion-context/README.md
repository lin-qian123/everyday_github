<!-- markdownlint-disable MD013 -->

# billion-context（ranxianglei/billion-context）中文解读

> 上游仓库：<https://github.com/ranxianglei/billion-context> · 归类：Coding Agents 与终端助手 · 本页基于 2026-10-13 的 README、配置、session identity、Release、许可证与 GitHub REST API 静态整理；未让它代理任何真实模型凭据、会话或并行 Agent 流量。

## 定位

billion-context 是面向多类 coding-agent 客户端的上下文压缩代理 / 原生插件 / launcher。它在模型请求链路中注入 `compress`、`decompress`、`search_context` 和 `acp_status`，把已消费对话折叠成可恢复的分层摘要，以延长单会话并改善 prefix cache 利用。

## 用法

可安装 npm 包后使用 `bili plugin install <client>`、`bili <client>` 或在 base URL 前添加 `/bili/` 代理前缀。默认监听 `127.0.0.1`；launcher 会根据客户端采用 base-URL rewrite 或证书 MITM。应先用测试 API key 和可丢弃会话验证协议、流式响应、缓存、恢复及日志，再考虑接入正式客户端。

## 原理

- 代理解析 Anthropic / OpenAI 等请求形状，识别 conversation id，执行 `acp-kernel` 增量压缩后再转发上游。
- 摘要按消息范围持久化，可按需解压或搜索；显式 session id 优先，缺失时用历史前缀关联。
- native plugin、launcher 和 URL rewrite 覆盖不同客户端；部分封闭客户端依赖 TLS MITM 和本地 CA。
- session state、运行日志、版本检查与 advisory 包分别落在本机状态目录和 npm 更新链路。

## 价值

- 为长 coding session 提供独立于宿主内建 compact 的可观察压缩层，可查看 token、cache hit 和被折叠范围。
- 同一工具支持 Codex、Claude Code、OpenCode、pi、Gemini 等多个宿主，便于统一实验压缩策略。
- session identity、衍生会话与并发边界有专门设计文档，至少把关键假设暴露给审计者。

## 风险边界

- 代理位于模型请求中间，能看到 prompt、tool schema、响应和凭据相关流量；证书 MITM 进一步扩大本机 CA 与供应链权限。
- README 自述仍属 Early，真实模型集成测试是后续里程碑；“省 5 倍 token”“数十亿 token 单会话”不能视为通用质量或成本结论。
- 绑定 `0.0.0.0` 时没有认证，只允许可信 LAN / 防火墙后使用；debug 与持久 session 文件也可能保留敏感上下文。
- API 返回 `NOASSERTION`，根 LICENSE 是 MIT 文本加额外产品表面署名条款，不应简写成标准 MIT；package manifest 的 `MIT` 字段不能覆盖附加条款。
- 自动更新和独立 advisory 轮询会修改已安装包；即使有回滚与节流，也需纳入组织的软件更新策略。

## 补充建议

- 用固定 prompt 集比较原始客户端与压缩链路的任务成功率、事实丢失、TTFT、输入 token、cache hit 和总成本。
- 保持 loopback，禁用不需要的 debug / session 持久化 / auto-update；正式使用前检查 CA、代理白名单和日志保留期。
- 每次版本变更固定 npm 版本与客户端版本，并保存可解压的原始会话副本，避免摘要成为唯一证据。

## 参考资料

- GitHub 仓库：<https://github.com/ranxianglei/billion-context>
- GitHub REST API：<https://api.github.com/repos/ranxianglei/billion-context>
- `v0.1.195` Release：<https://github.com/ranxianglei/billion-context/releases/tag/v0.1.195>
- 配置说明：<https://github.com/ranxianglei/billion-context/blob/master/CONFIGURATION.md>
- Session identity：<https://github.com/ranxianglei/billion-context/blob/master/SESSION-IDENTITY.md>
- LICENSE 与附加条款：<https://github.com/ranxianglei/billion-context/blob/master/LICENSE>
