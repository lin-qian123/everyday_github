<!-- markdownlint-disable MD013 -->

# OpenDataLoader PDF（opendataloader-project/opendataloader-pdf）

> 上游仓库：<https://github.com/opendataloader-project/opendataloader-pdf> · 归类：RAG、检索与知识处理 · 本页基于 2026-10-02 的 GitHub API、README、benchmark 链接、package manifest、Release 与 LICENSE 静态整理，未处理真实 PDF、复跑准确率 / 速度或验证 PDF/UA 合规。

- 抓取快照：29,454 stars、2,807 forks、90 open issues。
- 热度信号：GitHub Java Trending 抓取时约 +16 当日 stars。
- 版本与许可：当前核心为 Apache-2.0，latest Release / tag 为 `v2.5.12`；上游注明 2.0 以前版本为 MPL-2.0。

## 定位

OpenDataLoader PDF 是面向 RAG / LLM 数据和可访问性修复的 PDF parser，提供 Python、Node.js、Java 与 CLI 接口，把数字 PDF、扫描件或 tagged PDF 转成 Markdown、带 bounding box 的 JSON、HTML 或 Tagged PDF。默认路径是确定性的本地 Java 解析，复杂页可交给本机 hybrid AI backend。

## 用法

基础安装为 `pip install -U opendataloader-pdf`，需要 Java 11+ 与 Python 3.10+；Python 用 `opendataloader_pdf.convert()` 批处理，Node 包为 `@opendataloader/pdf`，Java 有 Maven artifact。复杂表格、OCR、公式或图表说明需安装 `[hybrid]` extra，先启动本地 `opendataloader-pdf-hybrid` 服务，再由 CLI / SDK 指向它。

## 原理

本地模式结合 PDF text / geometry、border 与 clustering 分析、XY-Cut++ reading order、heading / list / image 检测和坐标保留；hybrid 模式对复杂页面使用 Docling / OCR / 公式或图片 enrichment。输出前还提供 watermark / header filtering 和针对文档 prompt injection 的规则过滤；可访问性路径根据版面结构生成 tag tree，再用 veraPDF 等工具做后续验证。

## 价值

同一管线同时保留文字、结构与页内坐标，便于 RAG chunk、来源回跳和逐元素审计；数字 PDF 可低成本批量本地处理，复杂页再选择性使用 AI。Tagged PDF 输出也为可访问性修复提供了可自动化的起点，而不只导出纯文本。

## 风险边界

- README 的 0.907 overall、0.928 table、0.015 / 0.463 秒每页与“第一”来自项目方 benchmark 和特定 Apple M4 / 200-document 设置，本轮未复跑。
- layout、表格、公式、OCR、标题层级和 bounding box 都可能错；结构化 JSON 与坐标不等于语义正确或引用完整。
- prompt-injection filter 是有限规则，不能保证恶意 PDF 不影响下游 LLM；不可信 PDF 解析本身还应放进资源受限隔离环境。
- hybrid backend 虽可本地运行，仍会下载并执行模型 / OCR 依赖；“no cloud required”不等于零网络、零供应链或零敏感缓存。
- 自动生成 Tagged PDF 是 PDF/UA 工作流基础，不等于法律或完整无障碍合规；上游把 PDF/UA export 和 visual studio 列为 enterprise 功能。
- 版本 2.0 前后许可证不同；代码许可也不覆盖输入文档、字体、模型权重、OCR engine、生成描述或企业 add-on。

## 补充建议

在隔离 worker 固定 `v2.5.12`、Java、Python / Node、OCR engine 与模型 revision；用自有 PDF 金标分别测数字页、扫描件、多栏、复杂表格、公式、图表和恶意指令。将 page / bbox 证据回链到原 PDF，人工抽样 Markdown、JSON 与 Tagged PDF；可访问性项目再用 veraPDF、screen reader 与人工检查，不把 parser score 当作合规证明。

## 参考资料

- [GitHub 仓库](https://github.com/opendataloader-project/opendataloader-pdf)
- [GitHub REST API](https://api.github.com/repos/opendataloader-project/opendataloader-pdf)
- [README 与 Quick Start](https://github.com/opendataloader-project/opendataloader-pdf/blob/main/README.md)
- [Benchmark 仓库](https://github.com/opendataloader-project/opendataloader-bench)
- [Hybrid Mode 文档](https://opendataloader.org/docs/hybrid-mode)
- [Python Quick Start](https://opendataloader.org/docs/quick-start-python)
- [v2.5.12 Release](https://github.com/opendataloader-project/opendataloader-pdf/releases/tag/v2.5.12)
- [LICENSE](https://github.com/opendataloader-project/opendataloader-pdf/blob/main/LICENSE)
