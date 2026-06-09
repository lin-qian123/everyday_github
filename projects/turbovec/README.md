# turbovec

## 项目定位
`turbovec` 是一个基于 `TurboQuant` 的向量检索库，用 Rust 实现核心索引，并提供 Python 绑定。它瞄准的不是“更大的向量数据库平台”，而是本地、低内存、低延迟、可嵌入的 ANN 检索层，适合给 RAG、语义搜索和 agent 检索管线做轻量底座。

- GitHub：https://github.com/RyanCodrai/turbovec
- PyPI：https://pypi.org/project/turbovec/
- 适用人群：需要在本地或私有环境里做高密度向量检索的 AI 工程师、RAG 系统开发者、强调隐私和成本控制的团队。

## 用法

官方 README 给出的最短路径非常直接：

1. 安装 Python 包：
   `pip install turbovec`
2. 创建索引：
   `from turbovec import TurboQuantIndex`
3. 指定向量维度和量化位宽，例如：
   `index = TurboQuantIndex(dim=1536, bit_width=4)`
4. 写入向量并检索：
   `index.add(vectors)`，再执行 `index.search(query, k=10)`。
5. 如需持久化，可用 `index.write("my_index.tq")` 保存，再用 `TurboQuantIndex.load(...)` 加载。

官方还单独提供了 `IdMapIndex`，适合需要稳定外部 ID、删除操作和 allowlist 过滤的场景。这说明它并不只是做 demo，而是在认真补“真实检索系统里最常见的工程要求”。

## 原理

`turbovec` 的核心思路是用 `TurboQuant` 做在线向量量化，把向量压缩到更低比特表示，再配合手写 SIMD 内核做快速搜索。

- 无训练量化：README 明确强调没有单独的 train phase，也不需要先训练 codebook。
- 在线增量写入：向量加入后即可进入索引，不必每次扩容都重建全库。
- 高压缩比：仓库主页直接给出例子，`1000 万` 文档的 `float32` 语料约需 `31 GB` RAM，而 `turbovec` 可压到约 `4 GB`。
- SIMD 加速：在 ARM 上用 NEON，在 x86 上用 AVX-512BW，目标是直接和 FAISS 的 PQ/FastScan 路线竞争。
- 检索时过滤：支持在 `search()` 阶段传 allowlist，把 ACL、租户、时间窗或 BM25 候选集约束直接下沉到检索核内部。

这让它和“托管型向量数据库”路线不同。它更像一块能被你嵌进现有 Python/Rust 检索栈里的高性能本地引擎。

## 价值

- 对本地 RAG 或私有部署团队，最大的价值是“低内存 + 本地可控”，而不是再接一个外部服务。
- 对需要混合检索的系统，allowlist 过滤能力很实用，因为它让“先粗筛再 dense rerank”的架构更顺手。
- 对强调工程可验证性的团队，README 给了较完整的 recall、compression、speed 对比口径，便于自行复核。

## 风险边界

- 它解决的是向量索引层问题，不会自动帮你解决 embedding 质量、召回策略、rerank 和业务正确性。
- 公开 benchmark 很亮眼，但真实收益仍取决于维度、数据分布、CPU 指令集和查询模式。
- 如果团队已经深度绑定云向量数据库，本地嵌入式索引的运维优势未必能覆盖迁移成本。

## 补充建议

- 真正值得优先验证的是你自己的 embedding 维度、过滤模式和硬件条件，而不是只看 README 里的统一 benchmark。
- 如果场景里租户隔离、时间窗或权限过滤很多，`allowlist` 路线比单纯比拼裸 ANN QPS 更值得关注。
- 从 GitHub 热度来看，`turbovec` 代表的不是“大而全 AI 应用”，而是 AI 基础设施继续向更底层的检索与压缩层下沉。

## 参考资料

- 仓库主页：https://github.com/RyanCodrai/turbovec
- PyPI：https://pypi.org/project/turbovec/
- GitHub Trending：https://github.com/trending
- 仓库 README 中的 Python / Rust / Benchmark / How it works 段落
