<!-- markdownlint-disable MD013 -->

# Comp AI CRM

> 更新：2026-10-20（Asia/Shanghai）。分类：办公、商业与行业应用。上游 `trycompai/crm`；快照 `6d4793dd6d7a`（release）。本文基于官方榜单、认证 API 与上游文件静态研究；热度、版本时间与跨平台证据见[当日日报](../../daily/2026-10-20/ai-hotspots.md)。

## 定位

面向 AI Agent 的单租户 CRM：联系人、公司、交易和沟通记录是 Agent 的工作底座，研究 Agent 有自己的任务队列、预算和后续检查。默认分支为 `release`，`main` 是尚未发版的开发线；本文按 release 快照阅读。[README.md](https://github.com/trycompai/crm/blob/6d4793dd6d7aeea91aa6a034e00b17d7408a2d08/README.md)

## 用法

需要 Bun、Docker 和可用身份提供方。上游本地流程为：[README.md](https://github.com/trycompai/crm/blob/6d4793dd6d7aeea91aa6a034e00b17d7408a2d08/README.md)

```bash
git clone https://github.com/trycompai/crm.git
cd crm
cp .env.example .env
bun install
docker compose up -d
bun run db:deploy
bun run dev
```

启动前设置 `BETTER_AUTH_SECRET`、`ALLOWED_SIGN_IN`，并成对配置 Google 或 Microsoft OAuth；app / API 默认入口为 3000 / 3001。`AGENT_BRIDGE_SECRET` 需在相关进程一致，开启聊天桥接；外部研究源按需增加，不能把“无研究 API key 仍可读自有记录”理解为模型推理无费用。[README.md](https://github.com/trycompai/crm/blob/6d4793dd6d7aeea91aa6a034e00b17d7408a2d08/README.md)[docs/environment.md](https://github.com/trycompai/crm/blob/6d4793dd6d7aeea91aa6a034e00b17d7408a2d08/docs/environment.md)

## 原理

Next.js、NestJS、Postgres 与 eve Agent 分工；dispatcher 用带租约的队列领取到期任务，Agent 通过 authored tools 读 CRM、获取证据、记录事实、安排复查。证据分档由代码规则而非模型自评分决定；沙箱用于文件 / shell 处理，文档规定 deny-all 出站且不向其注入 `DATABASE_URL`。[README.md](https://github.com/trycompai/crm/blob/6d4793dd6d7aeea91aa6a034e00b17d7408a2d08/README.md)[docs/agent.md](https://github.com/trycompai/crm/blob/6d4793dd6d7aeea91aa6a034e00b17d7408a2d08/docs/agent.md)

## 价值

可研究如何将来源、身份匹配、人工字段保护、预算和后台接续接进业务系统；相较只返回一段“销售洞察”，事实记录与待定建议更便于追责。是否能减少重复维护、避免错配，需要用有标准答案的脱敏联系人集评估。

## 风险边界

- README 的“强证据写入、弱证据人工决定”是概括。详细文档还规定：空白字段可由达到保留门槛的较弱证据填入，`PROBABLE` 在已有值的字段才仍需人工决定。因此不能声称每项未验证事实都必经审批，也不能把“不让模型自评分”当作事实正确保证。[docs/agent.md](https://github.com/trycompai/crm/blob/6d4793dd6d7aeea91aa6a034e00b17d7408a2d08/docs/agent.md)
- Agent 可读完整邮件正文；deny-all 只覆盖沙箱，`web_fetch` 在 app runtime、`web_search` 在 provider。邮件授权、模型上下文、外部查询与可信工具执行需要分别审查；提示中的数据边界规则不等于网络抓包验证。[docs/agent.md](https://github.com/trycompai/crm/blob/6d4793dd6d7aeea91aa6a034e00b17d7408a2d08/docs/agent.md)
- 自托管安装包含服务端遥测：每日汇总、设置里程碑和失败事件；文档称不用客户正文 / 邮箱值，并采用属性 allowlist。可用 `CRM_TELEMETRY_DISABLED=1` 或 `DO_NOT_TRACK=1` 后重启关闭；官网营销页分析与安装实例是不同范围。[docs/telemetry.md](https://github.com/trycompai/crm/blob/6d4793dd6d7aeea91aa6a034e00b17d7408a2d08/docs/telemetry.md)
- 持久会话和后台任务会持续消耗资源；取消运行不回滚已完成副作用。单租户结构不能直接外推为多租户隔离方案。代码 MIT；最新 Release `v1.15.3` 的发行时间为 2026-08-21，不是当日发布。[docs/agent.md](https://github.com/trycompai/crm/blob/6d4793dd6d7aeea91aa6a034e00b17d7408a2d08/docs/agent.md)[LICENSE](https://github.com/trycompai/crm/blob/6d4793dd6d7aeea91aa6a034e00b17d7408a2d08/LICENSE)

## 补充建议

先用合成公司与邮件验证身份歧义、空白字段 / 人工已有值、拒绝建议、预算用尽及取消后的写入；对照任务行、事实来源和最终 CRM 值。邮箱 / 日历只读授权与后续业务写动作分开验收，并确认关闭遥测后的实际网络行为。本轮未部署、接邮箱或运行 Agent。

## 参考资料

- [README.md](https://github.com/trycompai/crm/blob/6d4793dd6d7aeea91aa6a034e00b17d7408a2d08/README.md)
- [LICENSE](https://github.com/trycompai/crm/blob/6d4793dd6d7aeea91aa6a034e00b17d7408a2d08/LICENSE)
- [docs/agent.md](https://github.com/trycompai/crm/blob/6d4793dd6d7aeea91aa6a034e00b17d7408a2d08/docs/agent.md)
- [docs/telemetry.md](https://github.com/trycompai/crm/blob/6d4793dd6d7aeea91aa6a034e00b17d7408a2d08/docs/telemetry.md)
- [docs/environment.md](https://github.com/trycompai/crm/blob/6d4793dd6d7aeea91aa6a034e00b17d7408a2d08/docs/environment.md)
- [仓库 API](https://api.github.com/repos/trycompai/crm)
- [v1.15.3 Release](https://github.com/trycompai/crm/releases/tag/v1.15.3)
