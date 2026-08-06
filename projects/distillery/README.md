<!-- markdownlint-disable MD013 -->

# Distillery

- 仓库：[TonicAI/distillery](https://github.com/TonicAI/distillery)
- 快照：2026-08-07 抓取；GitHub API 显示其创建于 2026-08-06，约 11 stars、0 forks，MIT。数字会随时间变化。
- 分类：模型、训练与推理基础设施

## 定位

开源、多 provider 的 LLM API 网关。它在客户端与 OpenAI、Anthropic、Gemini、Azure OpenAI、Vertex AI、Bedrock 等上游之间提供统一入口、密钥映射、路由、配额、用量记录与可选文本脱敏。

## 用法

项目要求 `uv` 和 Python 3.12+。在仓库根目录执行 `uv sync`，再以 `DISTILLER_HOST=127.0.0.1 uv run distillery` 启动本机代理；OpenAI SDK 仅需把 `base_url` 改为代理地址。原始请求捕获默认关闭；若显式设为磁盘捕获，记录会写入本地 `captures/`，配置前应先审阅保留策略。

## 原理

代理按接入协议适配上游 URL 和认证，把代理 key 映射到租户与厂商凭据，并在请求/响应旁路生成统一 `InteractionRecord`。流式响应持续转发，采集经有界队列送往 JSONL 或 HTTP sink；失败投递进入持久 spool。其脱敏仅在显式开启且受支持的协议路径上生效，不支持的脱敏路径默认拒绝继续处理。

## 价值

适合把多家模型的凭据、观察、配额和审计入口收敛到应用外部，降低每个客户端分别实现 provider 差异的成本。OpenAI-compatible 接入降低迁移门槛，本地 SQLite 指标与可回放的 spool 也有利于排障。

## 风险边界

网关会经过 API key、提示词、工具参数和模型输出；即使开启脱敏，也不能假定所有敏感字段或所有协议均被覆盖。捕获的数据、管理员界面、代理 key、下游 sink、日志留存和出站访问都需要单独做访问控制与合规审查。它不是通用模型负载均衡、响应缓存或数据治理系统。

## 补充建议

生产先绑定回环地址或受认证的内网入口，使用独立最小权限 provider 凭据，并关闭原始采集；再用合成敏感文本和流式/tool-call 请求验证实际脱敏覆盖。为 JSONL、spool 与 SQLite 设加密、保留期和删除演练，并把网关可用性故障纳入应用降级设计。

## 参考资料

- [项目 README](https://github.com/TonicAI/distillery)
- [配置与安全说明](https://github.com/TonicAI/distillery/blob/main/README.md#capture-safety)
- [GitHub API 元数据快照](https://api.github.com/repos/TonicAI/distillery)
