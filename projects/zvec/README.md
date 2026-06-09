# zvec

## 为什么是今天的热门
GitHub 今日趋势榜单中，`alibaba/zvec` 位列靠前位置，并显示“stars today”级别增长，说明关注度快速上升。citeturn6search1

## 这是什么
Zvec 是一个开源、**嵌入式（in-process）**向量数据库，定位为轻量、低延迟、可直接嵌入应用。它基于阿里巴巴的 Proxima 向量检索引擎，提供生产级的相似度检索能力，并强调“无需额外服务”的使用体验。citeturn7view0

## 能做什么（关键能力）
- **快速相似度检索**：面向大规模向量检索场景，强调低延迟与高吞吐。citeturn7view0
- **Dense + Sparse + 多向量查询**：同时支持密集/稀疏向量，并允许一次请求做多向量查询。citeturn7view0
- **混合检索**：支持语义相似度与结构化过滤结合。citeturn7view0
- **可嵌入运行**：作为库运行在你的进程内，可用于 Notebook、服务端、CLI 或边缘设备。citeturn7view0

## 工作原理（简述）
Zvec 以“嵌入式向量库”为设计核心，应用程序直接链接/加载库并在同一进程中完成索引与检索流程，从而减少跨服务通信开销，提升延迟表现。其底层构建于 Proxima 引擎，以提供可扩展的向量相似度检索能力。citeturn7view0

## 快速上手

### Python
**安装**：
```bash
pip install zvec
```
citeturn7view0

**最小示例（简化版）**：
```python
import zvec

schema = zvec.CollectionSchema(
    name="example",
    vectors=zvec.VectorSchema("embedding", zvec.DataType.VECTOR_FP32, 4),
)

collection = zvec.create_and_open(path="./zvec_example", schema=schema)
collection.insert([
    zvec.Doc(id="doc_1", vectors={"embedding": [0.1, 0.2, 0.3, 0.4]}),
])

results = collection.query(
    zvec.VectorQuery("embedding", vector=[0.4, 0.3, 0.3, 0.1]),
    topk=5,
)
print(results)
```
citeturn7view0

### Node.js
**安装**：
```bash
npm install @zvec/zvec
```
citeturn7view0

### 环境要求与平台
- Python 3.10 - 3.12。citeturn7view0
- 支持 Linux（x86_64/ARM64）与 macOS（ARM64）。citeturn7view0

## 适用场景（建议）
- 需要**低延迟**且不想维护独立向量数据库服务的应用。
- 边缘/本地场景：希望将向量检索能力“嵌入式”打包到应用中。
- 语义检索 + 结构化过滤的混合检索需求。citeturn7view0

## 参考链接

```text
https://github.com/alibaba/zvec
https://github.com/trending
```
