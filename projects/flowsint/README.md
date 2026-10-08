<!-- markdownlint-disable MD013 -->

# Flowsint（reconurge/flowsint）

> 上游仓库：<https://github.com/reconurge/flowsint> · 归类：RAG、检索与知识处理 · 本页基于 2026-10-09 的 GitHub API、README、ETHICS、DISCLAIMER、部署配置与模块说明静态整理，未用真实个人标识符、泄露数据或目标资产运行 enrichers。

- 抓取快照：9,558 stars、1,173 forks、65 open issues。
- 热度信号：GitHub TypeScript Trending 抓取时约 +85 当日 stars；最后 push 为 2026-10-03。
- 版本与许可：最新 Release / tag `v1.2.13`，Apache-2.0；本页固定审计 commit `4c05849bc6ca`。

## 定位

Flowsint 是面向合规 OSINT 调查的可视化图谱平台，把 domain、IP、ASN、个人、组织、邮箱、电话、网站和加密钱包等实体连接到统一调查图中。它不是通用知识图谱数据库，也不自动证明实体关系真实；核心用途是把查询、enricher 结果、人工判断和来源组织成可复查的调查工作区。

## 用法

官方生产路径以 Docker Compose 启动 PostgreSQL、Redis、Neo4j、API、worker 与前端。单机默认从 `http://localhost:5173/register` 创建首个账户；部署到局域网或服务器前必须更换 `AUTH_SECRET`、`MASTER_VAULT_KEY_V1`、`NEO4J_PASSWORD`，补 host allowlist，并让 5173 只经带 TLS 的反向代理开放。调查时先建实体，再按明确范围运行 DNS、WHOIS、breach、social、wallet 或 crawler enrichers。

## 原理

前端通过 FastAPI 访问图谱与调查状态；core 负责数据库、认证、vault、Celery task 和 orchestrator，独立 enrichers 将外部数据转换成 Pydantic 实体 / 关系，Neo4j 承载图结构，PostgreSQL / Redis 支撑业务状态与队列。模块边界有助于扩展来源，但每个 enricher 仍继承第三方 API、抓取规则、命中歧义和时间漂移。

## 价值

它把零散 OSINT 工具输出转成可交互图，并提供本地部署、版本固定、vault 与多人入口，比手工复制搜索结果更适合持续调查和证据复盘。对安全团队而言，统一实体 schema 与任务队列也便于分离“发现线索”和“人工确认”。

## 风险边界

- Email / phone breach、username、social、wallet 与组织关系会形成高敏感个人数据集；合法来源不自动等于合法处理、保留或再分发。
- enrichers 返回的是候选关系，不是身份确认；同名、共享基础设施、历史 DNS 与聚合数据会产生误关联。
- “数据在本机”只描述部署位置；外部 API、DNS、WHOIS、crawler、Maigret / Sherlock 与 n8n connector 仍会产生网络访问和第三方日志。
- 默认 secrets 仅适合本机首次启动；公网部署若未配置 HTTPS、host allowlist、强密钥、备份加密与最小端口，会暴露调查图和 API key。
- README 明确测试仍不完整；Release 存在不等于所有 enrichers、升级和恢复路径达到生产质量。
- ETHICS 与 DISCLAIMER 是使用约束和提醒，不是技术强制范围控制，也不能替代书面授权、平台条款和当地法律审查。

## 补充建议

先用虚构域名、保留测试网段和合成身份建立小调查，逐个记录 enricher 的数据出口、误报和 TTL。生产部署使用独立主机、TLS、最小出站 allowlist、短期 API key、加密备份和字段级保留期；任何个人身份关联至少要求两个独立来源与人工复核，并保留撤回和删除流程。

## 参考资料

- [GitHub 仓库](https://github.com/reconurge/flowsint)
- [GitHub REST API](https://api.github.com/repos/reconurge/flowsint)
- [README 与部署边界](https://github.com/reconurge/flowsint/blob/main/README.md)
- [ETHICS](https://github.com/reconurge/flowsint/blob/main/ETHICS.md)
- [DISCLAIMER](https://github.com/reconurge/flowsint/blob/main/DISCLAIMER.md)
- [生产 Compose](https://github.com/reconurge/flowsint/blob/main/docker-compose.prod.yml)
- [v1.2.13 Release](https://github.com/reconurge/flowsint/releases/tag/v1.2.13)
