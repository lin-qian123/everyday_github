<!-- markdownlint-disable MD013 -->

# RAG_Techniques

## 定位

RAG Techniques 是 RAG 方法的 notebook / 脚本教材，包含基础检索、查询改写、结构分块、重排、Graph RAG 和评估等。它是用于学习与受控比较的公开材料集合，不能因代码可见就视为宽松许可的生产框架。

2026-10-31 采样：Jupyter Notebook daily +73 stars；API 累计 30,146 stars / 3,691 forks / 8 open issues（含 PR）。核读 main `4eacd2fae8cf`；发行 API 首项 [ai-agents-book-v1.0](https://github.com/NirDiamant/RAG_Techniques/releases/tag/ai-agents-book-v1.0)，2026-10-26 UTC。以下区分作者文档与有限源码核读，未做上游运行验收。

## 用法

先读根 LICENSE，再选择单个 notebook 的依赖、数据和模型。最小基线可从 `simple_rag.ipynb` 或同名脚本入手；脚本依赖根目录 helper 与 evaluation，运行目录会影响相对路径。以下仅演示准备好依赖与 provider 凭证后的调用：

```bash
cd all_rag_techniques_runnable_scripts
python simple_rag.py --path ../data/Understanding_Climate_Change.pdf   --chunk_size 1000 --chunk_overlap 200 --n_retrieved 2
```

脚本基础 `run` 返回并显示检索片段，不能把这个输出当作端到端答案已验证。即使不传 `--evaluate`，顶部仍导入 evaluation / deepeval 依赖。缺 key、依赖版本与模型不可用应记失败，不用随机数据补齐。本轮未运行 notebooks、模型或评测。

## 原理

基线用 PyPDFLoader 抽取 PDF、按 1000 字符 / 200 重叠切块、OpenAI embedding 与 FAISS 建索引，再检索 top-k。查询改写、HyDE、重排与结构分块分别改变不同环节，比较时需固定其余变量。

本轮新读的 Mistral OCR notebook 以一份带表格的论文对照 PyPDF、OCR 加相同字符分块、OCR 加结构分块，再做相同重排；作者展示数值脱离表头 / caption 后仍可能被错误使用。这里核的是作者 notebook / 已存结果，未复跑，也不将单文档结论推广到全部 PDF。

## 价值

适合建立“原文 → 抽取 → chunk → 候选 → 重排 → 答案”的可追踪诊断流程。先打印进入索引的文本，再判断是解析、分块还是检索失败，通常比只追加复杂 Agent 更容易定位问题；实际收益由自有数据和标注验证。

## 风险边界

- 根 LICENSE 明文限制非商业使用，商业使用需事先书面授权，并约定贡献授权；不能标为 MIT / Apache 或默认可商用。API 许可字段为 NOASSERTION，正文以实际文本为准。
- 新 OCR notebook 披露 Mistral 赞助、预计算 OCR 缓存与小样本边界。无 Mistral key 可读缓存，不代表 embedding、答案模型和 LLM 重排均无需 key / 联网 / 成本。
- README / notebook 标 OCR 4，而 2026-10-30 X 帖文写 OCR 4.1；本页不将两者视为同版本实测，复跑需记录解析模型标识与 live / cache 路径。
- 主线 README 的 42+ 与 notebook 自述 41 是各自文档口径，不能拿作本轮逐一运行通过数量。
- 示例数据、提示、外部模型与裁判可能使结论偏向特定方案；看到了正确片段、裁判打高分和答案事实正确须分别验证。赞助与图书推广不构成效果证明。
- README 部分视频 / 推广链接经 click tracker；本库用固定视频直链供复核，不由点击量推出方法质量。发行首项是图书标签，不是统一 notebook 软件版本。

## 补充建议

建立含表格、跨页表、双栏与扫描页的脱敏小数据集，保留原页 / 抽取文本 / chunk / 检索排名 / 答案引用。分别比较解析和分块，再加重排；报告拒答、数字 / 单位错误、来源准确率及每问成本，用独立标注集复核裁判。

## 参考资料

- [上游仓库](https://github.com/NirDiamant/RAG_Techniques)、[仓库 API](https://api.github.com/repos/NirDiamant/RAG_Techniques)。
- [README.md](https://github.com/NirDiamant/RAG_Techniques/blob/4eacd2fae8cfe91a067e642de29ccba0190f902f/README.md)。
- [LICENSE](https://github.com/NirDiamant/RAG_Techniques/blob/4eacd2fae8cfe91a067e642de29ccba0190f902f/LICENSE)。
- [all_rag_techniques_runnable_scripts/simple_rag.py](https://github.com/NirDiamant/RAG_Techniques/blob/4eacd2fae8cfe91a067e642de29ccba0190f902f/all_rag_techniques_runnable_scripts/simple_rag.py)。
- [helper_functions.py](https://github.com/NirDiamant/RAG_Techniques/blob/4eacd2fae8cfe91a067e642de29ccba0190f902f/helper_functions.py)。
- [evaluation/evalute_rag.py](https://github.com/NirDiamant/RAG_Techniques/blob/4eacd2fae8cfe91a067e642de29ccba0190f902f/evaluation/evalute_rag.py)。
- [all_rag_techniques/document_parsing_with_mistral_ocr.ipynb](https://github.com/NirDiamant/RAG_Techniques/blob/4eacd2fae8cfe91a067e642de29ccba0190f902f/all_rag_techniques/document_parsing_with_mistral_ocr.ipynb)。
