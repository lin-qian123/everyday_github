<!-- markdownlint-disable MD013 -->

# helix-db（HelixDB/helix-db）

- GitHub：<https://github.com/HelixDB/helix-db>
- 抓取快照：2026-09-23，6,079 stars、368 forks、18 open issues
- 热度信号：GitHub Rust Trending 抓取时约 +88 当日 stars
- 版本与许可：Apache-2.0；最新 GitHub Release 为 `v3.3.0`

## 定位

HelixDB 是面向知识图谱、RAG 和 Agent memory 的 Rust graph-vector database。它把 graph、vector、KV、document、relational 等访问面放入同一产品，并提供 Rust、TypeScript、Python、Go SDK、本地 CLI 和托管 HelixDB Cloud。

## 用法

本地可先安装 `helix` CLI，再用 `helix chef` 安装 query skills / docs MCP、生成工程、启动实例、写入示例数据并把任务交给检测到的 coding agent；也可按官方 quickstart 手动配置。应用通过各语言 DSL 生成同一 JSON AST，并调用本地默认 `http://localhost:6969` 的 `POST /v2/query`。

## 原理

HelixDB 以 graph + vector 为主数据模型，同时提供其他数据抽象。各 SDK 把 typed DSL 编译成统一查询 AST，由运行实例执行图遍历、向量 / 全文检索和事务。Cloud 路径用 object storage、单 writer 和可扩展 reader，并通过 WorkOS session 与 gateway key 管理控制面 / 数据面访问。

## 价值

Agent memory 和企业知识应用常同时需要关系、语义相似度、全文与业务实体查询；单一查询层可减少多数据库同步和拼接代码。多语言 SDK 与本地 / Cloud 两种路径也利于从原型逐步迁移。

## 风险边界

- “一个平台替代多类数据库”是产品定位，不是对每种 OLTP、向量、图或全文 workload 的独立性能证明。
- `curl | bash`、PowerShell installer 和 `helix chef` 会下载工具并写入 skills / MCP / 工程；应先读脚本、固定版本并用可丢弃配置试装。
- Agent memory / company data 往往高度敏感；本地与 Cloud 的认证、备份、租户隔离、删除和密钥流需要分别审计。
- README 的 SDK 版本各自发布，并不与数据库 / CLI tag 一一相同；要锁定完整兼容矩阵而非只记 `v3.3.0`。

## 补充建议

用公开或合成图建立可重复 benchmark，对比冷 / 热启动的写入、图遍历、vector + filter、并发事务、备份恢复和错误结果率。若使用 `helix chef`，记录它新增的 skill、MCP、文件与网络请求；Cloud 试验只使用最小权限 tenant 和可撤销 application key。

## 参考资料

- [GitHub 仓库](https://github.com/HelixDB/helix-db)
- [GitHub REST API](https://api.github.com/repos/HelixDB/helix-db)
- [官方文档](https://docs.helix-db.com)
- [查询指南](https://docs.helix-db.com/database/querying-guide/overview)
- [v3.3.0 Release](https://github.com/HelixDB/helix-db/releases/tag/v3.3.0)
- [LICENSE](https://github.com/HelixDB/helix-db/blob/main/LICENSE)
