<!-- markdownlint-disable MD013 MD034 -->

# pdf-inspector：先分类、再抽取或选择性 OCR 的 PDF 入口层

## 项目概览

- 上游仓库：https://github.com/firecrawl/pdf-inspector
- GitHub API 快照（2026-09-01）：17,335 stars、1,198 forks、195 个开放 issue
- 当前 release：`v1.15.0`
- 接口：Rust、CLI、Python、Node.js、Browser WebAssembly
- 许可证：MIT

## 定位

pdf-inspector 是面向 PDF ingest pipeline 的 Rust 库。它先判断文档是文本型、扫描型、图像型还是混合型，再做位置感知文本抽取、Markdown 转换、表格/多栏布局处理，并把真正需要 OCR 的页面单独路由出去。

## 用法

Python 入口示例：

```bash
pip install pdf-inspector
```

```python
import pdf_inspector

result = pdf_inspector.process_pdf("document.pdf")
print(result.pdf_type)
print(result.markdown)
```

CLI 可用 `detect-pdf` 只分类，也可用 `pdf2md` 输出 Markdown、JSON、页码标记或指定页。浏览器 Wasm 版本允许在客户端完成同一套基础解析。

## 原理

解析器共享一次文档加载：detector 抽样内容流判断 PDF 类型，extractor 遍历字体、内容流、XObject、链接和表单字段，layout 层重建行、列与阅读顺序，table 层结合矩形绘制和文本对齐识别表格，最后转换为 Markdown。

选择性 OCR 路径只渲染被分类为需要 OCR 的页面，并保留页面级 provenance。这能减少对大型 OCR runtime 的无条件加载，但分类错误仍可能让内容被漏掉或不必要地进入 OCR。

## 价值

- 给 RAG、知识库和 agent 文档入口增加明确的预检与路由层。
- 同时覆盖服务器、CLI、Python/Node 和浏览器，便于统一管线。
- 位置、字体和页级信息有利于追踪抽取错误，而不只返回一段纯文本。
- 上游提供公开 benchmark 表，可作为候选比较入口。

## 风险边界

- PDF 是复杂且可能恶意的容器；解析库必须放在资源受限、无敏感凭据的沙箱中。
- 多栏、公式、脚注、跨页表格、嵌入字体和扫描质量仍可能导致阅读顺序或字符错误。
- 上游 benchmark 为特定 200 份语料、关闭 OCR 的结果，不能直接外推到中文论文、专利或业务票据。
- Markdown 视觉上“像对了”不代表数字、单位、上下标、表头和引用关系正确。
- 本页未运行该库，也未复现其速度或质量分数。

## 补充建议

1. 建立包含中文、公式、多栏、扫描件、表格和损坏字体的内部 golden set。
2. 对分类置信度设人工复核区间，并记录进入 OCR 的页码与原因。
3. 对关键数字、单位、表格和引用做版面渲染对照，不只检查 Markdown 是否非空。
4. 对超大页、压缩炸弹、深层对象和异常字体设置时间、内存、页数与文件大小上限。
5. 比较固定版本的 pdf-inspector、OCR 和下游 chunker，避免把版本漂移误判为内容变化。

## 参考资料

- 仓库与 README：https://github.com/firecrawl/pdf-inspector
- 官方文档：https://firecrawl.github.io/pdf-inspector/
- Python API：https://github.com/firecrawl/pdf-inspector/blob/main/docs/python.md
- Rust API：https://github.com/firecrawl/pdf-inspector/blob/main/docs/rust-api.md
- Benchmark 语料：https://github.com/opendataloader-project/opendataloader-bench
