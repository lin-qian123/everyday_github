# cocoindex

- GitHub: <https://github.com/cocoindex-io/cocoindex>
- 官网: <https://cocoindex.io/>
- 观察时间: 2026-05-05

## 这是什么

`cocoindex` 是一个面向 AI 工作负载的数据转换与增量索引框架：
- 用声明式 Dataflow 定义“从原始数据到可检索索引”的流水线；
- 核心引擎（Rust）负责增量更新、最小重算与数据血缘；
- 适合 RAG、语义搜索、知识图谱、长期运行 agent 的上下文构建。

它的核心价值不是“再做一个向量库”，而是把“索引构建 + 持续刷新 + 可解释处理链”统一起来。

## 快速用法

### 1) 安装

```bash
pip install -U cocoindex
```

### 2) 定义一个最小数据流（示意）

```python
import cocoindex

@cocoindex.flow_def(name="TextEmbedding")
def text_embedding_flow(flow_builder: cocoindex.FlowBuilder, data_scope: cocoindex.DataScope):
    data_scope["documents"] = flow_builder.add_source(cocoindex.sources.LocalFile(path="markdown_files"))
    collector = data_scope.add_collector()

    with data_scope["documents"].row() as doc:
        doc["chunks"] = doc["content"].transform(
            cocoindex.functions.SplitRecursively(),
            language="markdown", chunk_size=2000, chunk_overlap=500
        )

        with doc["chunks"].row() as chunk:
            chunk["embedding"] = chunk["text"].transform(
                cocoindex.functions.SentenceTransformerEmbed(
                    model="sentence-transformers/all-MiniLM-L6-v2"
                )
            )
            collector.collect(text=chunk["text"], embedding=chunk["embedding"])

    collector.export("doc_embeddings", cocoindex.targets.Postgres())
```

### 3) 典型落地场景

- 文档/代码库语义检索（RAG）；
- 会议纪要、知识库、PDF 等异构数据统一索引；
- 长流程 agent 的“持续新鲜上下文”维护。

## 原理拆解（为什么它快）

1. 声明式 Dataflow：每个字段由输入字段纯函数生成，避免隐式状态。
2. 增量计算：源数据或规则变化时，仅重算受影响子图。
3. 数据血缘：可追踪某条索引结果来自哪些输入与变换步骤。
4. 标准化 Source/Transform/Target：可插拔切换数据源、模型、存储目标。

这套机制让它在“持续更新的数据索引”上比一次性批处理更适合生产。

## 我认为有价值的补充

- 对 agent 工程的实际意义：
  - 许多 agent 失败不是模型弱，而是上下文脏、旧、不可追溯；
  - `cocoindex` 的增量与血缘能力，正好对应“长期运行可靠性”的短板。
- 引入建议：
  - 先从单一来源（例如 `docs/`）做 POC；
  - 再扩展到代码、工单、会议记录，统一进入同一检索层。
- 选型对比关注点：
  - 是否必须实时刷新；
  - 是否需要字段级可追溯；
  - 是否要跨多数据源保持一致处理语义。

## 参考资料

- 仓库 README（功能、示例、安装）: <https://github.com/cocoindex-io/cocoindex>
- 官方站点（增量索引与场景）: <https://cocoindex.io/>
- GitHub Trending（今日趋势参考）: <https://github.com/trending?since=daily>
