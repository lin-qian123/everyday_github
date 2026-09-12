<!-- markdownlint-disable MD013 -->

# DeskcommCRM（melgarafael/DeskcommCRM）中文解读

> 证据快照：2026-09-13（Asia/Shanghai）。GitHub REST API 显示 1,780 stars、548 forks、120 open issues，最新 release 为 `v1.19.0`，MIT。本文未安装、运行或连接真实 WhatsApp、CRM 客户数据与模型账号。

## 定位

DeskcommCRM 是面向 WhatsApp 销售与客服的自托管 CRM，把会话收件箱、客户与漏斗、自动化、按租户 RAG、AI agent、人工接管和审计放到同一套系统。它可以经 WAHA 的扫码通道或 Meta Cloud API 接入 WhatsApp，并用 OpenRouter、Anthropic、OpenAI 等 provider 驱动 agent。

它的“open-source AI sales OS”定位比普通聊天机器人更重：agent 可分配为客服、移动线索阶段、触发 follow-up、调用 skills，并通过内部 MCP 接触 CRM 能力；这也意味着错误操作、越权与个人数据风险比只读问答更高。

## 用法

上游主路径是准备带 Docker 的 VPS、域名、Supabase、模型 key 与 WhatsApp 号码，再运行安装器：

```bash
git clone https://github.com/melgarafael/DeskcommCRM.git
cd DeskcommCRM
bash hostgator-setup-kit/install.sh
```

开发环境则使用 `pnpm`、Supabase/Postgres 与可选 WAHA。上游特别说明新数据库应应用 `supabase/baseline.sql`，而不是把历史 stub migrations 当成完整建库链；生产前还应单独演练 `backup.sh` 与升级回滚。

## 原理

- Next.js 16 / TypeScript 提供 Web 应用和 API，Supabase 负责 Postgres、Auth、Storage、Realtime、RLS 与 pgvector。
- WAHA 或 Meta Cloud API 接收 WhatsApp 消息；媒体进入私有 Storage bucket，发送侧提供节流、抖动、时间窗与 STOP 检测。
- agent engine 使用按租户知识、组织记忆、意图路由、情绪分析、skills 与 AI→人工交接；组织级预算上限限制模型支出。
- CRM 事件先写 `event_log`，再由每分钟执行的 drain 任务触发 webhook 和自动化，避免数据库 trigger 直接访问外网。
- RBAC、RLS、assignment/transfer 与 append-only audit log 形成治理面；内部 MCP 与未来公共 MCP 会把这些业务动作暴露给外部 agent。

## 价值

- 将“聊天、客户记录、漏斗、自动化与 agent”置于同一事务和审计上下文，减少跨 SaaS 拼接造成的身份与状态漂移。
- 自托管让团队可选择数据库、模型 provider、遥测和备份策略，适合需要数据驻留与定制流程的组织。
- 人工接管、agent assignee、支出上限和提案审批提供了比完全自动回复更清晰的运营闸门。
- 上游公开 schema、架构、runbook 和数据库 invariants，可作为审查多租户 AI 应用的工程样本。

## 风险边界

- “自托管”不等于数据只在一台机器：Supabase、模型 provider、WAHA/Meta、Sentry、邮件和电商连接器都会形成独立数据路径。
- WhatsApp 非官方扫码通道存在账号限制与条款风险；节流与 anti-ban 不能保证账号安全或合规。
- RLS、RBAC 和审计是设计与测试证据，不是对所有部署、升级、插件和自定义 SQL 的持续隔离证明。
- agent 可修改真实客户状态并发送消息；RAG、情绪判断和“自我改进”提案会产生误分流、错误承诺与提示注入风险。
- LGPD 标签不等于自动满足适用法律。实例运营者仍需处理告知、同意、保留、删除、跨境传输和数据主体请求。
- 上游安装器会触碰 VPS、Docker、cron、数据库与 secret；执行远程脚本或无交互安装前必须固定 revision 并审阅内容。

## 补充建议

1. 先用合成客户、测试号码和低权限 provider key 建立 staging；禁止向真实联系人自动发送消息。
2. 为每个 tenant 做 RLS 越权、webhook 重放、prompt injection、人工交接和预算耗尽测试，并保存审计证据。
3. 明确列出 WhatsApp、模型、Supabase、Sentry 与第三方连接器的数据字段、保留期和删除路径。
4. 生产升级前验证数据库备份、旧镜像回滚、cron 健康和一条端到端收发链；不要把 CI 绿色等同于实例可恢复。

## 参考资料

- GitHub：<https://github.com/melgarafael/DeskcommCRM>
- GitHub REST API：<https://api.github.com/repos/melgarafael/DeskcommCRM>
- Releases：<https://github.com/melgarafael/DeskcommCRM/releases>
- English README：<https://github.com/melgarafael/DeskcommCRM/blob/main/README.en.md>
- 架构：<https://github.com/melgarafael/DeskcommCRM/blob/main/ARCHITECTURE.md>
- 安全说明：<https://github.com/melgarafael/DeskcommCRM/blob/main/SECURITY.md>
- LICENSE：<https://github.com/melgarafael/DeskcommCRM/blob/main/LICENSE>
