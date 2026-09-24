<!-- markdownlint-disable MD013 -->

# Laya（aayushch/laya）

- GitHub：<https://github.com/aayushch/laya>
- 抓取快照：2026-09-25，280 stars、45 forks、7 open issues
- 热度信号：GitHub Python Trending 抓取时约 +79 当日 stars
- 版本与许可：Apache-2.0；latest GitHub Release 为 `v1.6.0`，tags 已到 `v1.7.0`，UI manifest 为 `0.0.1`

## 定位

Laya 是 local-first AI notification command center，把 Gmail、Slack、GitHub、Bitbucket、Jira、Linear、Notion、Outlook 与 Calendar 的事件统一为可研究、可归类、可关联和待批准的 Action Cards。它不是单纯通知收件箱，而是把跨工具上下文、coding-agent workspace、规则学习和 outbound action staging 放进同一桌面应用。

## 用法

可下载 macOS、Windows、Linux 构建，或从源码启动 Python / FastAPI engine、Svelte / Tauri UI 和本地 n8n；用户连接工作平台后选择 Ollama / LM Studio、本地兼容端点、云模型或已安装的 Claude Code、Codex、Gemini、Pi CLI 作为推理后端。默认先生成 Action Card，用户预览 / 批准后才通过 n8n 执行回复、评论或其他外发动作。

## 原理

连接器事件先由 n8n 归一化，再进入 Python pipeline 完成 ingest、route、stage、trace、learn、context learning 与 summary；SQLite / FTS5 保存结构化事件，ChromaDB 提供向量召回，并用 Reciprocal Rank Fusion 合并语义与精确关键词结果。Tauri UI 展示 cards、coherence、analytics、workspace 与 audit，OS keychain 保存 provider 和 connector 凭据。

## 价值

它试图解决消息、issue、PR、日历和文档上下文分散的问题，并把研究 / 生成与真正外发拆成可审阅的卡片。对多平台团队而言，统一 audit、失败重试、预算和跨系统 entity resolution 有助于减少遗漏，也给自动化规则提供了可见的 firing log。

## 风险边界

- “no cloud sync”只描述 Laya 自身存储；Gmail、Slack、Jira、Notion、云模型和 coding-agent CLI 仍各自有网络、账户和数据处理边界。
- 单机聚合会集中邮件、聊天、代码、日历、客户与员工信息；SQLite、ChromaDB、日志、导出和备份需要磁盘加密、访问控制与保留期。
- Action Card 的预览降低误发风险，但 processing rule 可自动 run agent / send egress；权限、收件人、幂等、速率限制与撤回能力必须逐连接器验证。
- n8n 的自托管配置被上游安全策略列为用户责任；本地 webhook、凭据、workflow import 与开放端口不能交给默认值。
- Release `v1.6.0`、tag `v1.7.0` 与 UI manifest `0.0.1` 不一致；升级、迁移和桌面构建必须固定具体 commit / artifact。

## 补充建议

从一个测试平台、只读 scope 与本地模型开始，使用虚构通知验证分类、关联、card approval、dead-event recovery 和 audit export。外发能力应逐个 connector 开启，并加入 recipient allowlist、二次确认、幂等 key 和小额度预算；再以脱敏数据测试跨平台 memory 的误关联、删除传播和规则学习回滚。

## 参考资料

- [GitHub 仓库](https://github.com/aayushch/laya)
- [GitHub REST API](https://api.github.com/repos/aayushch/laya)
- [v1.6.0 Release](https://github.com/aayushch/laya/releases/tag/v1.6.0)
- [v1.7.0 tag](https://github.com/aayushch/laya/tree/v1.7.0)
- [安全策略](https://github.com/aayushch/laya/blob/main/SECURITY.md)
- [NOTICE](https://github.com/aayushch/laya/blob/main/NOTICE)
- [LICENSE](https://github.com/aayushch/laya/blob/main/LICENSE)
