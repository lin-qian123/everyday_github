# qdrant

## 项目定位
`qdrant` 是一套面向下一代 AI 检索场景的高性能向量数据库与向量搜索引擎，重点不是“能不能存 embedding”，而是“能不能把过滤、混合检索、多向量与重排稳定放进生产查询路径”。

- GitHub：https://github.com/qdrant/qdrant
- 官网：https://qdrant.tech/
- 记录日期：2026-06-11（Asia/Shanghai）

## 为什么值得关注

- GitHub 仓库页显示约 `23.8k stars`、`1.7k forks`。
- 仓库 About 将其定义为 “High-performance, massive-scale Vector Database and Vector Search Engine for the next generation of AI”。
- 官网把核心卖点直接放在 `metadata filters`、`native hybrid search`、`multivector`、`one-stage filtering` 和 `reranking` 上，明显偏生产检索能力而不是单点 demo。

如果说 `milvus` 更像“大规模向量底座”的代表，`qdrant` 的热点则更像“现代 AI 检索查询能力”的代表。

## 用法

常见接入路径通常是：

1. 先用本地实例或 Qdrant Cloud 起一个最小集合。
2. 写入向量、payload metadata 和业务主键。
3. 在查询端组合 dense / sparse / hybrid search，再叠加过滤或 reranking。
4. 将其接入 RAG、agent memory、推荐或多模态搜索工作流。

对已经在做复杂检索策略的团队，`qdrant` 的吸引力往往不在“第一次跑通”，而在“把业务约束一并写进检索层”。

## 原理

`qdrant` 的公开路线很清晰：

1. 向量检索  
   提供高性能相似度搜索，支撑 AI 搜索主链路。

2. 混合检索  
   官方首页明确支持 dense + sparse 混合查询，并提到 BM25、SPLADE++、miniCOIL。

3. 查询表达能力  
   通过 JSON metadata、复杂过滤和 multivector，把“检索规则”拉近真实业务。

4. 结果优化  
   官网强调 reranking、MMR 等能力，说明它已经不满足于只返回近邻结果。

## 价值

- 适合检索逻辑比较复杂、过滤条件比较多的 AI 搜索系统。
- 对 agent / RAG 产品，能更自然地承接“语义 + 关键词 + 规则”的组合查询。
- 从产品化角度看，它更接近可直接落地的 AI 检索引擎，而不是研究型组件。

## 风险边界

- 更强的查询表达能力也意味着 schema、payload 与检索策略设计更容易失控。
- 向量库能力再强，也不能替代上游 embedding 选择、数据清洗和评测闭环。
- 如果团队暂时没有复杂过滤或 hybrid retrieval 需求，选它的收益未必会立刻体现。

## 补充建议

- 如果你的检索逻辑已经需要 metadata 过滤、关键词补偿或多向量表达，`qdrant` 值得优先评估。
- 真正要测的不是 benchmark 宣传，而是你自己的业务查询集在延迟、召回和成本之间的平衡。
- 不要把“支持很多高级特性”误判为“默认配置就最优”，生产前仍需要自己压测和调参。

## 参考资料

- https://github.com/qdrant/qdrant
- https://qdrant.tech/
- https://ossinsight.io/trending/ai
