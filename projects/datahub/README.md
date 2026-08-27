<!-- markdownlint-disable MD013 -->

# DataHub

> 上游仓库：[datahub-project/datahub](https://github.com/datahub-project/datahub) · 归类：RAG、检索与知识处理 · 本页基于 2026-08-28 的上游 README、官方快速开始与 GitHub API 快照整理。

## 定位

DataHub 是面向数据发现、治理和可观测性的开源 metadata platform，也把自己定位为 AI data catalog。它从数据仓库、湖、BI、ML 系统、编排器和 agent 连接器摄取元数据，建立包含 schema、血缘、使用情况、质量指标、owner 和治理标签的可查询图。GitHub Python Trending 当日页面显示约 12 个当日 stars；API 快照为 12,597 stars、3,676 forks、1,261 个开放 issue，2026-08-27 有推送，许可证为 Apache-2.0。仓库还提供基于目录的 Analytics Agent 和 MCP 接入，但这些上层能力不等于数据事实自动正确。

## 用法

本地探索可使用 Docker quickstart：

~~~sh
pip install --upgrade acryl-datahub
datahub docker quickstart
~~~

也可以使用 Homebrew 安装 CLI，或直接打开官方 demo。快速开始默认需要 Docker Desktop，并建议分配至少 8 GB RAM；完整栈包含 GMS、React UI、Elasticsearch、MySQL 和 Kafka。接入 Snowflake、BigQuery、dbt 等数据源时，按官方 ingestion recipe 配置连接信息，并先使用无敏感测试数据。

AI agent 接入可以通过仓库 README 指向的 Analytics Agent 或 acryldata/mcp-server-datahub，但应把查询权限限制为只读，并对 agent 返回的 SQL、字段和数据范围做人工或确定性校验。

## 原理

- ingestion connector 从数据源读取 schema、owner、profile、usage、quality 和 lineage 等 metadata，通过 batch 或 streaming 方式写入 DataHub。
- GMS、存储层、搜索索引和 Kafka 共同维护可查询的 metadata graph；前端与 API 根据实体、字段、标签、关系和权限提供搜索与浏览。
- lineage 把上游数据集、转换任务和下游消费连接起来，帮助追踪数据流向与影响面；它依赖连接器覆盖和源系统的实际信息。
- MCP/Analytics Agent 以 catalog 元数据、治理规则和可发现的数据资产作为模型上下文，再生成查询、解释或图表；模型生成的 SQL 和结论仍需回到权限、schema 和原始数据验证。
- RBAC、认证、授权和审计记录构成治理层，但部署者仍需正确配置租户、服务账号、数据脱敏、保留期和网络出口。

## 价值

- 把分散在仓库、湖、BI、ML 和编排系统里的数据资产组织成统一发现入口。
- 用字段级 schema、血缘、owner、质量和使用信息提升 RAG/agent 选择数据源时的上下文质量。
- 为数据团队提供搜索、影响分析、治理和可观测性基础，而不仅是一个向量检索接口。
- 开源连接器、CLI、API、MCP 和本地 quickstart 便于先做小规模试验，再按组织数据栈扩展。

## 风险边界

- metadata 新鲜度、血缘完整性和质量指标取决于 connector、调度、权限和源系统；目录存在不等于源数据仍可访问或正确。
- Analytics Agent 可能生成错误 SQL、越权查询、错误字段解释或把 metadata 当成业务事实；必须限制只读权限并进行结果校验。
- DataHub 的存储、搜索、Kafka、数据库、缓存和导出可能包含内部 schema、业务名称、个人信息和安全标签；不可直接暴露到公网。
- Docker quickstart 适合开发探索，不代表生产 HA、备份、升级、灾备、隔离和性能配置。
- Apache-2.0 覆盖仓库代码；被接入的数据、连接器、模型、插件和下游服务仍有独立许可与合规责任。

## 补充建议

1. 先用公开/合成数据验证 ingestion、schema、lineage、搜索、删除和权限；保留一份可重建的 recipe 与版本记录。
2. 对 agent 提供最小只读 catalog 和数据访问范围，要求生成 SQL 先解释数据来源、时间范围、过滤条件和预期输出。
3. 建立 metadata freshness、connector failure、lineage coverage、权限拒绝和查询审计指标，避免把目录命中率当作数据质量。
4. 生产部署前单独评估 Elasticsearch/MySQL/Kafka 的备份、密钥、网络、租户隔离、PII 脱敏和升级回滚。

## 参考资料

- [上游 README / AI data catalog 与 quickstart](https://github.com/datahub-project/datahub)
- [DataHub Quick Start](https://docs.datahub.com/docs/quickstart)
- [Metadata ingestion 文档](https://docs.datahub.com/docs/metadata-ingestion)
- [Analytics Agent 文档](https://docs.datahub.com/docs/features/feature-guides/analytics-agent)
- [MCP Server for DataHub](https://github.com/acryldata/mcp-server-datahub)
- [仓库许可证](https://github.com/datahub-project/datahub/blob/master/LICENSE)
- [GitHub API 元数据](https://api.github.com/repos/datahub-project/datahub)
