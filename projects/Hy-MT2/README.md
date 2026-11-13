<!-- markdownlint-disable MD013 -->

# Hy-MT2：面向术语、格式与风格约束的翻译模型

- 上游：[`Tencent-Hunyuan/Hy-MT2`](https://github.com/Tencent-Hunyuan/Hy-MT2)；仓库 ID：`1242193963`。
- 核读：2026-11-14（Asia/Shanghai）；主线固定于 [`ff1903ecaa72`](https://github.com/Tencent-Hunyuan/Hy-MT2/tree/ff1903ecaa724e10951a23c16817a2413c752b35)。
- 热度快照：1,749 stars / 185 forks / 14 open issues（含 PR）；来自 [GitHub API](https://api.github.com/repos/Tencent-Hunyuan/Hy-MT2)，不代表采用量或质量。

## 定位

腾讯 Hy 的多语言翻译模型家族，提供 1.8B、7B 与 30B-A3B MoE，以及 FP8 / GGUF 量化版本；上游称支持 33 种语言。重点是术语、风格、背景消歧和结构保留，随仓库发布 IFMTBench 与训练入口。官方 Python daily +49；是 2026-05-21 发布模型的首次建档，非今日新模型，GitHub release 列表为空。

## 用法

先选模型、精度与后端，固定权重 revision 和依赖。上游 Transformers 示例要求 `transformers>=5.6.0`，用 `AutoModelForCausalLM`、`device_map="auto"` 与 `trust_remote_code=True`；需先审阅远程代码，再决定是否授权执行。本轮未下载权重或推理。

输入采用 user 消息，例如“将以下文本翻译成英语，只输出译文”，按需加入术语表与结构约束。README 声明上下文 8,192、建议最大生成 4,096；dense 与 MoE 的采样建议不同。示例 `generate` 只显式设置长度，复现时还须核生成配置，不能假定它已落实参数表。

CPU GGUF 路径使用 llama.cpp；**1.25-bit STQ 内核所指 [PR #22836](https://github.com/ggml-org/llama.cpp/pull/22836) 当前仍 open、未合并**。README 的 clone / build 不代表通用主线已支持，需核指定实现和模型格式。仓库还提供 vLLM / SGLang 与 full / LoRA 训练路线。

## 原理

生成式模型将原文、指令与约束一起编码，自回归输出译文。30B-A3B 的激活参数量不等于全部权重存储；AngelSlim 低比特量化降低权重体积。上游约 440 MB 和 1.5 倍速度属于特定条件，不能替代 RAM、KV cache 或目标设备实测。

IFMTBench 把术语、布局、结构化数据、代码标签设为 gate，风格 / 背景由 LLM judge 评分；多约束总分为 gate 乘连续分均值。术语规则不通过也会调用 judge，并非全部评测都能离线确定。

## 价值

把“翻译好”拆成占位符不变、JSON 键保留、术语一致和风格匹配等可检查要求。训练与评测入口有助于建立域内回归集，而不是只看一句演示。

## 风险边界

- “超过商业 API / 大模型”是上游评测结论，受语言、数据域、prompt、量化和 judge 影响，本轮未复现。
- 默认 judge 模型名为 `gpt-4o`，endpoint / key 由环境变量配置；远程评分会外发文本与响应。`--skip-llm` 是规则调试模式，不能当作完整评测的等价成绩。
- 源码将缺失输出记为 `None`，平均只用已评分项；多约束组合略过缺失维度。需同时报告 total / scored、失败与逐维明细，不能只报平均分。
- API SPDX 为 NOASSERTION，但根 `LICENSE.txt` 明确为 Apache-2.0；[官方基础权重](https://huggingface.co/tencent/Hy-MT2-1.8B)与[官方 1.25-bit 权重](https://huggingface.co/tencent/Hy-MT2-1.8B-1.25Bit-GGUF)元数据也标 Apache-2.0。IFMTBench 数据集另用 CC-BY-4.0。
- 低温、量化或格式 gate 不保证无漏译、数字错误或语义反转，仍需独立结构检查与双语复核。

## 补充建议

用非敏感样本覆盖长句、单位、否定、占位符和歧义，记录语义质量、格式、峰值内存、首 token 与总延迟。固定后端 SHA、模型 revision、prompt、采样和 judge，使用同一批完整输出比较量化前后。

本页为静态源码、文档和模型元数据核读；未训练、量化、评测、下载模型或调用 judge。

## 参考资料

- [模型、推理与参数](https://github.com/Tencent-Hunyuan/Hy-MT2/blob/ff1903ecaa724e10951a23c16817a2413c752b35/README.md)。
- [训练与 LoRA](https://github.com/Tencent-Hunyuan/Hy-MT2/blob/ff1903ecaa724e10951a23c16817a2413c752b35/train/README.md)。
- [评测方法](https://github.com/Tencent-Hunyuan/Hy-MT2/blob/ff1903ecaa724e10951a23c16817a2413c752b35/IFMTBench/README.md)。
- [Judge 配置](https://github.com/Tencent-Hunyuan/Hy-MT2/blob/ff1903ecaa724e10951a23c16817a2413c752b35/IFMTBench/config.py)。
- [分母和缺失分数](https://github.com/Tencent-Hunyuan/Hy-MT2/blob/ff1903ecaa724e10951a23c16817a2413c752b35/IFMTBench/eval/scoring.py)。
- [模型许可](https://github.com/Tencent-Hunyuan/Hy-MT2/blob/ff1903ecaa724e10951a23c16817a2413c752b35/LICENSE.txt)。
- [数据集许可](https://github.com/Tencent-Hunyuan/Hy-MT2/blob/ff1903ecaa724e10951a23c16817a2413c752b35/LICENSE-IFMTBench.txt)。
