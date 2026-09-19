<!-- markdownlint-disable MD013 MD034 -->

# docling：把复杂文档转换为 Agent / RAG 可用结构的解析平台

> 上游仓库：https://github.com/docling-project/docling · 归类：RAG、检索与知识处理 · 本页基于 2026-09-20 的 README、官方文档、技术报告、release、LICENSE 与 REST API 静态整理；未在本机转换文档或复核 OCR / 表格准确率。

## 定位

`Docling` 面向 PDF、Office、HTML、图片、音频、视频、邮件和多种专业 XML，把版面、阅读顺序、表格、公式、代码、图像与转写结果统一到 `DoclingDocument`，再导出 Markdown、HTML、WebVTT、DocTags 或 lossless JSON。它是 RAG / Agent 的文档入口层，不是事实核验器或万能 OCR。

2026-09-20 的 GitHub 官方综合 / Python Trending 抓取显示约 `+94 stars today`；REST API 快照为 `67,012 stars / 4,833 forks / 935 open issues`，MIT。最新 release 为 `v2.129.0`（9 月 18 日）。

## 用法

项目要求 Python 3.10+：

```sh
pip install docling
docling https://arxiv.org/pdf/2206.01062
```

Python 入口保持简洁：

```python
from docling.document_converter import DocumentConverter

result = DocumentConverter().convert("document.pdf")
print(result.document.export_to_markdown())
```

需要视觉语言模型时可选择 VLM pipeline；还可通过 `docling-serve` 提供 API，或用 MCP server 暴露给 Agent。

## 原理

- format backend 读取 PDF、DOCX、PPTX、XLSX、HTML、EPUB、图片、音视频、邮件和专业 XML。
- PDF pipeline 组合页面布局、阅读顺序、表格结构、公式 / 代码识别、图像分类和 OCR。
- 各解析器映射到统一 `DoclingDocument`，保留层级、位置与结构，再按目标格式导出。
- VLM、ASR、OCR 与 chart understanding 可补充难解析内容；不同模型有独立权重、运行资源和许可证。
- LangChain、LlamaIndex、CrewAI、Haystack、API server 与 MCP 将解析结果接入下游检索和 Agent 工作流。

## 价值

- 用一套结构表达跨格式资料，降低每个 RAG 项目单独拼 OCR、表格和导出脚本的成本。
- 支持本地和 air-gapped 运行，适合对敏感文档建立可控解析链。
- 同时提供 CLI、Python、服务端和 MCP，多种接入方式便于从批处理逐步走向在线系统。
- 技术报告、示例、测试与高频 release 为格式覆盖和版本追踪提供较完整入口。

## 风险边界

- 结构化输出仍可能发生阅读顺序、表格单元格、公式、脚注、页眉页脚和 OCR 字符错误；关键结论必须回到原页坐标或渲染图。
- “local execution”取决于所选 pipeline、模型下载、远程 URL 和集成配置；首次权重下载与外部输入抓取可能产生网络访问。
- Docling 代码为 MIT，但 README 明确要求单独核对每个模型的许可证，不能把代码许可延伸到模型权重。
- MCP / API server 会扩大文档读取与解析表面，需要认证、路径 allowlist、文件大小、格式炸弹、超时和并发限制。
- 音视频、邮件、专利和财报可能含高敏感数据；缓存、临时文件、模型输入和导出物都需治理。
- 本页未验证 `v2.129.0` 的转换准确率、资源峰值、恶意文件处理、air-gap 完整性或下游检索质量。

## 补充建议

1. 为目标语种和格式建立带页码 / bounding box 的金标集，分别评估正文、表格、公式、图片和阅读顺序。
2. 固定 Docling、OCR / VLM / ASR 模型版本和硬件，记录冷启动、峰值内存、wall time 与失败类型。
3. 对外服务只允许受控目录和 MIME / 大小范围，隔离解析进程并禁用不必要网络。
4. 在 RAG 中保存原文件哈希、页码和坐标，让每个引用可回到原始视觉证据。

## 参考资料

- 上游 README：https://github.com/docling-project/docling
- 官方文档：https://docling-project.github.io/docling/
- 技术报告：https://arxiv.org/abs/2408.09869
- `v2.129.0` release：https://github.com/docling-project/docling/releases/tag/v2.129.0
- GitHub REST API：https://api.github.com/repos/docling-project/docling
- LICENSE：https://github.com/docling-project/docling/blob/main/LICENSE
