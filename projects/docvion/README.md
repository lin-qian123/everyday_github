# Docvion

## 定位

`Docvion` 是面向 RAG 与 LLM 文档摄取的 schema-first Python 库：它试图把 Docling、Tesseract、PaddleOCR 等解析器的异构输出适配为统一的 `DocvionDocument`。截至 2026-07-26，仓库创建于 2026-07-25，约 2 stars、1 fork，MIT 许可；其“中立标准”定位仍需真实多引擎数据验证。

## 用法

安装 PyPI 包后，先从已有解析器输出开始，调用 `convert` 得到统一对象，再导出结构化 Markdown 供 LLM 上下文使用，或导出保留 bbox、置信度与表格单元的 JSON。试点时应使用同一批扫描件、表格 PDF 和多语言文档，在切换引擎前后比较下游 chunk、检索与引用结果。

## 原理

库将具体解析器输出映射到规范化文档模型，下游代码只依赖 `DocvionDocument`。它还提供结构感知 chunking，并尝试处理引擎间置信度口径不同的问题；因此 OCR/layout engine 可以替换，而无需重写每个消费端。

## 价值

- 降低 RAG pipeline 对单一 OCR/解析器 JSON 结构的锁定。
- 将解析、分块和下游检索的接口分离，便于 A/B 评估和逐步迁移。
- MIT 许可使其适合原型中作为适配层候选。

## 风险边界

- 统一 schema 不能抹平不同 OCR、表格、阅读顺序和语言模型的真实精度差异。
- 置信度跨引擎未必可直接比较；低质量扫描件仍须保留页图和原始输出以便追溯。
- 早期项目的 adapter 覆盖、版本兼容与性能尚未被独立验证。

## 补充建议

把 canonical JSON 与原始引擎输出并存，建立字段丢失、表格保真、页码引用和 chunk 召回的回归集。生产采用前给每个 adapter 设版本 pin 和失败回退，避免 schema 变化静默污染索引。

## 参考资料

- GitHub：<https://github.com/prolixis/docvion>
- PyPI：<https://pypi.org/project/docvion/>
- Docling：<https://github.com/docling-project/docling>
