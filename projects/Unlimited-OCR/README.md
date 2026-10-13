<!-- markdownlint-disable MD013 -->

# Unlimited OCR（baidu/Unlimited-OCR）中文解读

> 上游仓库：<https://github.com/baidu/Unlimited-OCR> · 归类：RAG、检索与知识处理 · 本页基于 2026-10-14 的 README、论文、推理脚本、模型卡、许可证与 GitHub REST API 静态整理；未下载权重、运行 GPU 推理或复测作者 benchmark。

## 定位

Unlimited OCR 是百度开源的长文档 OCR / 文档解析模型。它以 DeepSeek-OCR 为基线，用 Reference Sliding Window Attention（R-SWA）替换 decoder 的全注意力，目标是在输出序列变长时保持近似恒定的 KV cache，并在 32K 最大长度内一次处理多页文档。

## 用法

上游提供 Transformers、vLLM 与 SGLang 三条推理路径。Transformers 示例要求 Python 3.12、CUDA 12.9、BF16 并开启 `trust_remote_code=True`；单图可选 `gundam` / `base`，多页与 PDF 使用 `base`。生产前应先固定模型 revision、容器或 wheel、CUDA 与后处理版本，并只对可公开样本做复现。

## 原理

- 视觉 encoder 压缩页面，LLM decoder 生成含文本、版面类别和坐标标记的长序列。
- R-SWA 只保留滑动参考窗口，限制长序列注意力和 KV cache 增长；论文将其描述为可推广到 ASR、翻译等解析任务的机制。
- 多页 / PDF 先转为图像，再通过单次长上下文或并发请求生成结果；仓库给出 OmniDocBench 后处理示例。

## 价值

- 把“逐页 OCR + 外部拼接”推进到可研究的一次性长文档解析路径，适合比较跨页连续性、显存和吞吐。
- 同时给出 Transformers、vLLM、SGLang 与公开论文，便于定位算法贡献和 serving 差异。
- 代码与 Hugging Face 模型卡均标为 MIT，权重公开下载入口清晰。

## 风险边界

- `trust_remote_code=True` 会执行模型仓库代码；固定 revision、离线审计与隔离环境不能省略。
- “dozens of pages / constant KV cache”来自作者论文与演示，不等于任意版式、语言、扫描质量或页数下准确率不下降。
- OCR 输出可能遗漏、幻觉或错误关联表格 / 坐标；合同、病历、财务、档案和无障碍转换都需逐页核对。
- README 的 SGLang 路径包含仓库内自带开发 wheel，且服务器示例绑定 `0.0.0.0`；不得无认证暴露到不可信网络。

## 补充建议

- 以相同 PDF、DPI、模型 revision 和后处理比较逐页模式与多页模式，记录字符错误率、结构错误、跨页一致性、峰值显存和 wall time。
- 对扫描件、双栏、表格、公式、手写、中文和超长页分别建失败集，不用单一总分掩盖版式差异。
- 保存原 PDF、页面图、raw token / bbox、清洗后文本与人工修订，避免只留下不可追溯的最终 Markdown。

## 参考资料

- GitHub 仓库：<https://github.com/baidu/Unlimited-OCR>
- GitHub REST API：<https://api.github.com/repos/baidu/Unlimited-OCR>
- 论文：<https://arxiv.org/abs/2606.23050>
- Hugging Face 模型：<https://huggingface.co/baidu/Unlimited-OCR>
- vLLM recipe：<https://recipes.vllm.ai/baidu/Unlimited-OCR>
- LICENSE：<https://github.com/baidu/Unlimited-OCR/blob/main/LICENSE>
