<!-- markdownlint-disable MD013 -->

# FalkorDB（FalkorDB/FalkorDB）

> 上游仓库：<https://github.com/FalkorDB/FalkorDB> · 归类：RAG、检索与知识处理 · 本页基于 2026-10-07 的 GitHub API、README、Rust manifest、构建文档与 LICENSE 静态整理，未启动数据库、导入知识图谱或复测查询 benchmark 与故障恢复。

- 抓取快照：7,701 stars、516 forks、913 open issues。
- 热度信号：GitHub Rust Trending 抓取时约 +348 当日 stars；最后 push 为 2026-10-06。
- 版本与许可：latest Release / tag 为 `v6.0.1`；API 返回 `NOASSERTION`，README、`Cargo.toml` 与根 LICENSE 明确为 SSPLv1；manifest 使用 `99.99.99` 占位值；本页固定审计 commit `d2c42e0328ed`。

## 定位

FalkorDB 是以 property graph、OpenCypher 与稀疏矩阵为核心的图数据库，面向知识图谱、GraphRAG、Agent memory、云安全和欺诈检测。当前主仓库是 Rust 实现，作为 Redis module 暴露图查询能力；它不是完整的 RAG pipeline 或自动事实校验层。

## 用法

上游快速路径是启动 `falkordb/falkordb` 容器并映射数据库 6379 与浏览器 UI 3000 端口，再用 Python、TypeScript、Rust、Go、Java、C# 等客户端发送查询。试用时应固定 `v6.0.1` 镜像 digest、只绑定 loopback / 私网、启用认证与持久卷备份，并先以合成图验证 schema、查询、租户隔离和恢复。

## 原理

项目用稀疏邻接矩阵表示图，以 GraphBLAS / LAGraph 的线性代数执行遍历和部分查询，节点 / 边属性遵循 property graph 模型，查询语言以 OpenCypher 为主并含自有扩展。Rust module 嵌入 Redis-compatible server，外部 client 通过 `GRAPH.QUERY` 等命令读写；构建还依赖 GraphBLAS、LAGraph 与 RediSearch submodule。

## 价值

把图遍历转成稀疏矩阵运算为高连接度知识图提供了清晰的性能路线，OpenCypher 与多语言 client 也降低应用接入成本。对 GraphRAG，它能把实体、关系和路径查询放在专门存储层，而不是全部压进向量检索或 prompt。

## 风险边界

- SSPLv1 不是宽松许可证，向第三方提供数据库服务时可能触发广泛源代码义务；采用前必须由法务结合部署模式审查，不能据“source available”默认等同 OSI 开源。
- README 示例直接映射 6379 / 3000；数据库、UI、认证和备份若暴露不当，会泄露完整知识图与管理面，生产环境不得照搬公开端口示例。
- 图谱中的错误关系、过期事实、敏感属性和 prompt injection 不会因换成图数据库自动消失；GraphRAG 输出仍需 provenance、权限过滤和最终回答评测。
- 上游的“ultra-fast”与 benchmark 站点是作者证据，本轮未在固定数据集、并发、缓存、查询分布和竞品版本下复测。
- OpenCypher 支持包含自有扩展，Redis client 兼容也不保证事务、一致性、运维与故障语义完全相同；迁移前需差分测试。
- `Cargo.toml` 的 `99.99.99` 是源码占位，不是产品发行版本；应以 Release、镜像 digest、submodule SHA 和 schema / backup 版本共同固定。

## 补充建议

以一份带真实查询分布但已脱敏的小图建立 golden set，验收查询正确率、p50 / p95、并发写、重启、备份恢复与租户越权；对 GraphRAG 同时测路径召回、引用准确性和错误关系传播。发布前记录 SSPL 评审结论、镜像 digest、client 版本、submodule 与恢复演练证据。

## 参考资料

- [GitHub 仓库](https://github.com/FalkorDB/FalkorDB)
- [GitHub REST API](https://api.github.com/repos/FalkorDB/FalkorDB)
- [README 与快速开始](https://github.com/FalkorDB/FalkorDB/blob/main/README.md)
- [官方文档](https://docs.falkordb.com/)
- [命令参考](https://docs.falkordb.com/commands/)
- [v6.0.1 Release](https://github.com/FalkorDB/FalkorDB/releases/tag/v6.0.1)
- [Rust manifest](https://github.com/FalkorDB/FalkorDB/blob/main/Cargo.toml)
- [SSPLv1 License](https://github.com/FalkorDB/FalkorDB/blob/main/LICENSE)
- [上游 benchmark](https://benchmark.falkordb.com/)
