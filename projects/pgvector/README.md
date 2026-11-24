<!-- markdownlint-disable MD013 -->

# pgvector：把向量相似度检索放进 PostgreSQL

- 上游：[pgvector/pgvector](https://github.com/pgvector/pgvector)，仓库 ID `359952601`；本页新增于 2026-11-25。
- 快照：23,803 stars / 1,405 forks / 19 open issues（API 累计，含 PR）；C daily +12 stars。
- 版本：README 安装示例固定 `v0.8.7`，tag 对应 `f37c13f68b57d2c3472b2214fbcff699d6d34876`；本轮主线 `e8f84dcc55dd2cace82dfadcdd7929781c3f708c`，CHANGELOG 已列 `0.9.0 (unreleased)`。
- 证据范围：固定 README / CHANGELOG、控制文件与索引参数的局部静态核读；未安装扩展、连接数据库、建索引或测性能。

## 定位

pgvector 是 PostgreSQL 扩展，提供向量类型、距离算子、精确近邻检索以及 HNSW / IVFFlat 近似索引。业务字段与向量可保存在同一数据库，结合 SQL、JOIN 和既有数据库运维能力，适合已有 Postgres 的 RAG、相似项目推荐和检索实验。

它负责存储与检索；embedding 的生成、模型与维度选择、文档分块、重排、引用质量和回答生成需由上层实现。高向量召回率也不能直接解释为答案正确率。

## 用法

先按目标 Postgres 的版本与发行渠道安装扩展。稳定 tag 的 README 声明支持 Postgres 13+；主线未发行 0.9.0 的 CHANGELOG 已声明移除 13 / 14 支持，不能混用两者的环境要求。

下面是在**测试数据库**中的最小精确检索例子；假设已有启用扩展的权限。整个示例放在事务中，最后回滚。本轮未执行。

```sql
BEGIN;
CREATE EXTENSION IF NOT EXISTS vector;
CREATE TEMP TABLE demo_vectors (id integer, embedding vector(3));
INSERT INTO demo_vectors VALUES (1, '[1,2,3]'), (2, '[4,5,6]');
SELECT id, embedding <-> '[3,1,2]' AS l2_distance
FROM demo_vectors
ORDER BY embedding <-> '[3,1,2]'
LIMIT 2;
ROLLBACK;
```

`<->` 是 L2 距离，`<=>` 是余弦距离，`<#>` 返回**负内积**，以适配升序索引扫描。业务维度必须与 embedding 模型对应；三个数只是演示数据，不是文本 embedding。

需要近似索引时，可在自己的测试表执行 `CREATE INDEX ON items USING hnsw (embedding vector_l2_ops);`。索引的 operator class 要与查询距离一致，保留原始距离算子升序 `ORDER BY ... LIMIT ...`，并用 `EXPLAIN (ANALYZE, BUFFERS)` 检查实际计划；有索引不保证优化器一定选它。

## 原理

- **精确检索**：默认进行精确近邻搜索，可作为同一数据 / 距离定义下的召回基线；这里的“精确”针对向量距离，不评价语义或事实。
- **HNSW**：构建多层近邻图，不需要先训练聚类中心；用更多构建内存与时间换取查询的速度 / 召回折衷。`hnsw.ef_search` 默认 40。
- **IVFFlat**：先划分向量集合，再探测部分列表，需要有代表性的数据建立索引；`lists` 与查询 `probes` 共同影响速度 / 召回，默认 probes 为 1。
- **过滤与迭代扫描**：近似索引先取候选，再应用过滤条件；可能返回少于 `LIMIT` 的结果。0.8.0 起可开启 iterative scan，直到得到足够候选或碰到扫描 / 内存上限。
- **排序与召回分开**：HNSW `strict_order` 保证返回结果按距离排序，不保证已找全真实 top-k；`relaxed_order` 允许局部次序放宽。主线 HNSW 与 IVFFlat 的 iterative scan 默认均为 off。

## 价值

对已有 Postgres 的团队，向量与业务行同库可减少独立同步链路，复用 SQL、事务、备份和观察工具；这是否优于专用向量库仍取决于数据量、更新率、过滤选择率、内存和延迟目标。

工程上可先保留精确检索，再比较 HNSW / IVFFlat。应同时报告 recall@k、过滤后返回数量、P95 延迟、索引体积、构建 / 更新和恢复成本，避免只给单次吞吐数字。

## 风险边界

| 议题 | 已核事实与验证条件 |
| --- | --- |
| 版本漂移 | 主线 `vector.control` 仍写 0.8.7，但 CHANGELOG 含未发行 0.9.0；文件里的版本字符串不能证明当前源码等于稳定 tag。 |
| 已发布修复 | 0.8.7（2026-10-01）记录修复 IVFFlat 建索引 buffer overflow；这是上游修复记录，未核实际部署二进制或利用条件。 |
| 过滤结果不足 | 上游举例：命中 10% 的过滤条件与默认 ef_search=40，平均只剩约 4 个结果；这是说明性估算，不是本轮测量。 |
| 迭代扫描 | HNSW `max_scan_tuples` 默认 20,000，近似上限且不约束初始扫描；提高上限仍可能受 `work_mem` 等约束，不保证满召回。 |
| 数据权限 | 租户条件、数据库权限与应用鉴权需另行配置；近似索引的候选过滤过程不能替代访问控制。 |
| 模型变化 | 更换 embedding 模型 / 维度 / 归一化方式可能需要重算与重建索引；不同模型向量不能仅凭维度相同就直接比较。 |
| 许可 | API 返回 `NOASSERTION`；实际 LICENSE 为 PostgreSQL 风格的宽松条款，允许在保留指定声明的条件下使用、修改与分发，不能记成“无许可证”或 MIT。 |

## 补充建议

1. 先记录 Postgres、扩展 tag / SHA、embedding 模型和距离定义，再固定一组含真实过滤条件的保留查询。
2. 对相同快照运行精确 top-k 作基线，逐项扫描 ef_search / probes / iterative scan，另记过滤不足与超时。
3. 用代表性增量数据验证 VACUUM、并行建索引、更新和恢复；小静态表的表现不外推到生产负载。
4. RAG 再单独评价文档覆盖、重排与引用支持度，向量召回与最终回答质量分别记账。

## 参考资料

- [仓库 API](https://api.github.com/repos/pgvector/pgvector)、[v0.8.7 tag 引用](https://api.github.com/repos/pgvector/pgvector/git/ref/tags/v0.8.7)。
- [稳定 0.8.7 README，固定 tag commit](https://github.com/pgvector/pgvector/blob/f37c13f68b57d2c3472b2214fbcff699d6d34876/README.md)。
- [主线固定 README：检索、过滤、迭代、调优](https://github.com/pgvector/pgvector/blob/e8f84dcc55dd2cace82dfadcdd7929781c3f708c/README.md)、[CHANGELOG：已发布修复与未发行变更](https://github.com/pgvector/pgvector/blob/e8f84dcc55dd2cace82dfadcdd7929781c3f708c/CHANGELOG.md)。
- [vector.control](https://github.com/pgvector/pgvector/blob/e8f84dcc55dd2cace82dfadcdd7929781c3f708c/vector.control)、[HNSW 参数注册](https://github.com/pgvector/pgvector/blob/e8f84dcc55dd2cace82dfadcdd7929781c3f708c/src/hnsw.c)、[IVFFlat 参数注册](https://github.com/pgvector/pgvector/blob/e8f84dcc55dd2cace82dfadcdd7929781c3f708c/src/ivfflat.c)、[LICENSE 原文](https://github.com/pgvector/pgvector/blob/e8f84dcc55dd2cace82dfadcdd7929781c3f708c/LICENSE)。
