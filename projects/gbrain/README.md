<!-- markdownlint-disable MD013 -->

# GBrain（garrytan/gbrain）

> 上游仓库：<https://github.com/garrytan/gbrain> · 归类：记忆层与个人 AI 基础设施 · 本页基于 2026-10-08 的 GitHub API、README、设计 / 安全文档与 manifest 静态整理，未导入邮件、会议、语音或真实个人记忆，也未运行后台 enrichment。

- 抓取快照：30,653 stars、4,596 forks、228 open issues。
- 热度信号：GitHub TypeScript Trending 抓取时约 +40 当日 stars；最后 push 为 2026-10-07。
- 版本与许可：最新 Release `v0.60.104.0`，MIT；本页固定审计 commit `8e11aa1f34ab`。

## 定位

GBrain 是让多个 Agent 共用显式、可纠正、可撤回且带来源记忆的本地 / 自托管知识层。它支持 keyless 关键词检索，也可选语义检索、图关系、综合回答、后台采集与“梦境”式维护；既能作为 coding-agent 的 MCP memory，也能扩展成持续运行的个人或公司知识系统。

## 用法

轻量本地路径要求 Bun 1.4+：从 GitHub 安装后运行 `gbrain init --pglite --no-embedding`，再以 `gbrain serve --surface verbs` 接入 Codex、Claude Code 或其他 MCP client。先用唯一的 remember / recall / correction / withdrawal fixture 验证，再决定是否启用远端 HTTP、Tailscale Funnel、Postgres、embedding、synthesis、hook 或后台 ingest。

## 原理

核心把 page、source、事实 / take、关系、visibility 与操作审计落到 PGlite / PostgreSQL；关键词和可选 embedding 提供检索，typed graph 提供关系查询，synthesis 将多页内容整理为带引用回答。远端 caller 通过 profile、operation grant、source grant 与 visibility filter 限权；本地文件和共享数据库凭据属于另一信任边界。

## 价值

相较把对话摘要直接塞回 prompt，GBrain 强调来源、纠正、撤回、空缺提示和跨 Agent 一致记录；keyless 起步把“持久记忆”与“付费模型 enrichment”分离。公开文档也主动区分 facts、takes、当前未知项和检索 benchmark 范围，便于审计记忆为什么被召回。

## 风险边界

- 会议、邮件、联系人、语音、代码和 Agent transcript 汇聚后是高价值个人 / 企业数据；本地运行不等于低敏感或自动合规。
- keyless 只表示 GBrain 自身不调用付费模型；宿主模型仍会看到召回内容，启用 cloud embedding、rerank、extraction 或 synthesis 后文本可发送给外部 provider。
- 远端 grant 和 visibility filter 只覆盖特定访问路径；共享数据库凭据、同机文件、管理员账号或错误 source 配置可绕开租户隔离预期。
- 默认 brain-wide 可见性会让同一 brain 的其他 Agent 召回记忆；私有事实必须显式标记并做跨 profile 对抗测试。
- 自动采集、cron、enrichment、consolidation 与 citation repair 会持续改写知识；来源存在不等于事实仍然正确，take 也不能冒充 fact。
- Markdown export 不是完整数据库备份；版本迁移、PGlite / Postgres、embedding index 与后台队列需要独立备份和恢复演练。

## 补充建议

从无隐私 fixture、单用户 PGlite 与七个 memory verbs 开始，关闭 tunnel、hook、provider 和后台任务。为 source / profile / visibility 建立矩阵测试，分别验证越权读、越权写、纠正、撤回和删除；只有在可恢复备份、密钥轮换和数据保留规则就绪后，再接入真实渠道。

## 参考资料

- [GitHub 仓库](https://github.com/garrytan/gbrain)
- [GitHub REST API](https://api.github.com/repos/garrytan/gbrain)
- [设计说明](https://github.com/garrytan/gbrain/blob/master/DESIGN.md)
- [安全策略](https://github.com/garrytan/gbrain/blob/master/SECURITY.md)
- [Memory boundaries](https://github.com/garrytan/gbrain/blob/master/docs/guides/memory-boundaries.md)
- [Brains and sources](https://github.com/garrytan/gbrain/blob/master/docs/architecture/brains-and-sources.md)
- [Facts 与 takes](https://github.com/garrytan/gbrain/blob/master/docs/takes-vs-facts.md)
- [v0.60.104.0 Release](https://github.com/garrytan/gbrain/releases/tag/v0.60.104.0)
