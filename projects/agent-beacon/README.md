<!-- markdownlint-disable MD013 -->

# agent-beacon（Asymptote-Labs/agent-beacon）

- GitHub：<https://github.com/Asymptote-Labs/agent-beacon>
- 抓取快照：2026-09-24，1,297 stars、99 forks、5 open issues
- 热度信号：GitHub Go Trending 抓取时约 +186 当日 stars
- 版本与许可：MIT；latest GitHub Release 为 `v1.3.22`

## 定位

Beacon 是跨 Claude Code、Cursor、Codex、OpenCode 等 Agent harness 的 session telemetry 与记忆层。它把 prompt、response、tool、command、file、approval、MCP 和 token 归一为 OpenTelemetry-based event，再落到本地 JSONL、可审阅记忆或组织自有日志系统。

## 用法

macOS 可通过 Homebrew、Linux 通过 deb / rpm、Windows 通过 MSI 安装 endpoint；本地查看用 `beacon traces` 或 `beacon endpoint dashboard`。交互式安装会预选 Beacon Managed，但确认页允许改为 Local；后者只保留本机 JSONL。团队可再按需配置 Splunk、Datadog、Elastic、Sentinel、S3 / GCS 等转发。

## 原理

Beacon 从 Agent 的 OTLP、hooks、插件、poller、browser extension、CI 或 SDK 收集事件，统一成稳定 endpoint schema，经 sanitization、secret redaction、truncation 和 event-size limits 后写入轮转 JSONL。记忆流程从完整 session 中抽取工作流 / 修正 / 约定，经 review 后通过 MCP 或 Agent Skills 复用。

## 价值

它把分散在不同 Agent 工具里的执行历史放到统一、可查询、可迁移的数据面，适合调试、审计、成本分析和跨 harness 复用经验。默认 JSONL 及多种客户自管输出也便于接入已有安全与 observability 流程。

## 风险边界

- 完整 telemetry 可能含 prompt、response、命令输出、diff、文件路径、审批与 MCP 参数；本地保存也仍是高敏感数据集中点。
- secret redaction 是降低暴露而非保密证明；应以注入测试验证 token、连接串、业务字段和二进制 / 超长内容的覆盖。
- 交互式 setup 预选 Managed，确认后会开启转发；必须明确选择 Local 或核对 Standard / Metadata-only 模式、组织和 retention。
- browser extension 的 full retention 可保留完整 ChatGPT / Claude 对话；站点权限、用户知情、企业政策和卸载 / 删除必须单独治理。
- “支持 20+ harness”表示上游适配面，不保证各字段完整度一致；README 表格中 `–` / `~` 项需要按目标版本复核。

## 补充建议

先在无敏感仓库选 Local 模式，注入假 secret、超长输出、工具参数和失败 session，核对 JSONL、轮转、redaction、卸载及 harness 字段完整度。若转发到 SIEM / cloud storage，应把 endpoint key、TLS、IAM、retention、删除请求与跨境要求纳入同一数据治理方案。

## 参考资料

- [GitHub 仓库](https://github.com/Asymptote-Labs/agent-beacon)
- [GitHub REST API](https://api.github.com/repos/Asymptote-Labs/agent-beacon)
- [v1.3.22 Release](https://github.com/Asymptote-Labs/agent-beacon/releases/tag/v1.3.22)
- [架构与支持矩阵](https://github.com/Asymptote-Labs/agent-beacon#architecture)
- [SECURITY 与数据流](https://github.com/Asymptote-Labs/agent-beacon/blob/main/SECURITY.md)
- [官方文档](https://docs.beacon.sh)
- [LICENSE](https://github.com/Asymptote-Labs/agent-beacon/blob/main/LICENSE)
