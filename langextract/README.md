# LangExtract

LangExtract 是 Google 开源的“基于大模型的结构化信息抽取”库，主打高精度的**来源定位（grounding）**与**结构化输出**。它适合把长文档、报告、网页等非结构化文本转成结构化数据，并能把抽取结果**精确对应回原文位置**，降低“抽错、编造”的风险。

## 核心能力
- **可追溯抽取（grounded extraction）**：抽取结果与原文位置绑定，可生成高亮可视化 HTML，便于审阅与校验。
- **结构化输出**：用 schema + few-shot 例子约束输出结构，减少随意发挥。
- **长文档处理**：支持 chunking、并行处理与合并逻辑，适配长文本与多页文档。
- **多模型支持**：支持 Gemini 以及基于 Ollama 的本地模型；也支持 OpenAI 等云端模型接口。

## 原理概述（非实现细节）
1. **任务定义**：用 prompt + 示例定义“要抽什么、怎么抽”。
2. **结构约束**：schema + 控制式生成降低格式漂移。
3. **分块抽取**：对长文本分块并行抽取，之后合并去重。
4. **来源定位**：输出中带有与原文对应的证据/位置，支持生成可视化 HTML。

## 快速开始
### 安装
```bash
pip install langextract
```

### 最小示例
```python
import langextract as lx

# 1) 定义抽取任务
prompt = "Extract all person names and their titles from the text."
examples = [
    lx.Example(
        text="CEO Alice Smith joined Acme.",
        extractions=[{"name": "Alice Smith", "title": "CEO"}],
    )
]

# 2) 运行抽取
extractor = lx.LangExtract(prompt=prompt, examples=examples)
result = extractor.extract("CFO Bob Lee announced the new plan.")

# 3) 可视化（高亮证据）
result.save_html("extractions.html")
```

## 常见使用场景
- 合同/报告/网页中的实体、条款、数值抽取
- 研究报告与企业公告的结构化信息整理
- 构建可审计的“可追溯”抽取流水线

## 注意事项
- 云端模型需要配置 API Key（具体环境变量以官方文档为准）。
- 对中文场景效果与可追溯性高度依赖提示词与示例质量。
- 若追求完全离线运行，可选用 Ollama 本地模型（性能取决于模型与硬件）。

## 资源链接
- GitHub: https://github.com/google/langextract
- 文档与示例（README 内）: https://github.com/google/langextract/blob/main/README.md
- 可视化示例说明: https://github.com/google/langextract#interactive-visualization
