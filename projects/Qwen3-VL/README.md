<!-- markdownlint-disable MD013 -->

# Qwen3-VL

> 更新：2026-10-21（Asia/Shanghai）。分类：语音、视频与多模态。上游 `QwenLM/Qwen3-VL`；快照 `96588727e44c`（main）。本文为官方资料与源码静态研究；热度、发行时间及社媒限制见[当日日报](../../daily/2026-10-21/ai-hotspots.md)。

## 定位

Qwen 视觉语言模型系列，提供 Dense / MoE、Instruct / Thinking 等变体，面向图像问答、OCR、视频理解与视觉 Agent。可用权重本地推理，也有另外的托管 API 路径。[README.md](https://github.com/QwenLM/Qwen3-VL/blob/96588727e44c78b25ba03ea03b8e12f7e64fd0da/README.md)

## 用法

当前 GitHub quickstart 指定 `transformers>=4.57.0`，用 processor 构建包含图片 / 视频与文本的消息，再由模型生成。先从较小的 2B / 4B 权重及一张自有图片开始；具体设备、精度和依赖按目标权重核。[README.md](https://github.com/QwenLM/Qwen3-VL/blob/96588727e44c78b25ba03ea03b8e12f7e64fd0da/README.md) [2B Instruct 官方模型卡](https://huggingface.co/Qwen/Qwen3-VL-2B-Instruct)

视频 / 多图工具文档包含 `qwen-vl-utils` 的输入与处理方式；设置视觉 token / 像素预算、fps 或帧数，并保存实际采样。模型卡仍有“4.57.0 尚未发布”的旧安装注释，与当前 GitHub 指南不一致，应固定依赖后验证。[qwen-vl-utils/README.md](https://github.com/QwenLM/Qwen3-VL/blob/96588727e44c78b25ba03ea03b8e12f7e64fd0da/qwen-vl-utils/README.md) [2B Instruct 官方模型卡](https://huggingface.co/Qwen/Qwen3-VL-2B-Instruct)

## 原理

官方材料描述 Interleaved-MRoPE 在时间与空间维度组织位置，DeepStack 融合多层视觉特征，并通过文本与时间戳对齐处理视频事件；语言模型在视觉 token 和文本联合上下文上生成回答。这些机制不保证每一帧或细小对象都被正确识别。[README.md](https://github.com/QwenLM/Qwen3-VL/blob/96588727e44c78b25ba03ea03b8e12f7e64fd0da/README.md)

## 价值

工程判断：适合对比本地视觉问答、文档解析与视频检索的能力 / 成本。应按 OCR 字段准确率、时序定位、拒答和错误操作分别验收，不能把 benchmark 总分当成 GUI 自动操作可靠性。

## 风险边界

- README 的 256K / 扩展至 1M 等是系列能力声明，不代表任意设备、权重与默认配置可达到；MoE 激活参数也不等于全部常驻权重。视觉 token、分辨率、帧数和 KV cache 共同影响内存。[README.md](https://github.com/QwenLM/Qwen3-VL/blob/96588727e44c78b25ba03ea03b8e12f7e64fd0da/README.md)
- URL 媒体会触发下载，托管 API 会发送输入；本地推理、远程素材与云端模型需分开记录。GUI 行动要由外部 harness 限定权限与审批，模型输出不是授权。[README.md](https://github.com/QwenLM/Qwen3-VL/blob/96588727e44c78b25ba03ea03b8e12f7e64fd0da/README.md) [qwen-vl-utils/README.md](https://github.com/QwenLM/Qwen3-VL/blob/96588727e44c78b25ba03ea03b8e12f7e64fd0da/qwen-vl-utils/README.md)
- 仓库 Apache-2.0；本轮额外核 2B Instruct 模型卡同标 Apache-2.0，不外推全部第三方量化或衍生数据条款。README 的 2B / 32B 发布日期是 **2025-10-21**，不是今天；没有 GitHub Release 记录不等于没有权重发行。[LICENSE](https://github.com/QwenLM/Qwen3-VL/blob/96588727e44c78b25ba03ea03b8e12f7e64fd0da/LICENSE) [2B Instruct 官方模型卡](https://huggingface.co/Qwen/Qwen3-VL-2B-Instruct) [README.md](https://github.com/QwenLM/Qwen3-VL/blob/96588727e44c78b25ba03ea03b8e12f7e64fd0da/README.md)

## 补充建议

保存具体权重 revision、依赖、精度、图片缩放和视频帧时间戳；以含密集文字、遮挡、跨帧事件的自有样本做人工真值。复跑 benchmark 时采用对应 evaluation 配置，独立报告资源和失败例。本轮未下载权重、调用 API 或复现评测。[evaluation/mmmu/README.md](https://github.com/QwenLM/Qwen3-VL/blob/96588727e44c78b25ba03ea03b8e12f7e64fd0da/evaluation/mmmu/README.md)

## 参考资料

- [README.md](https://github.com/QwenLM/Qwen3-VL/blob/96588727e44c78b25ba03ea03b8e12f7e64fd0da/README.md)
- [evaluation/mmmu/README.md](https://github.com/QwenLM/Qwen3-VL/blob/96588727e44c78b25ba03ea03b8e12f7e64fd0da/evaluation/mmmu/README.md)
- [LICENSE](https://github.com/QwenLM/Qwen3-VL/blob/96588727e44c78b25ba03ea03b8e12f7e64fd0da/LICENSE)
- [qwen-vl-utils/README.md](https://github.com/QwenLM/Qwen3-VL/blob/96588727e44c78b25ba03ea03b8e12f7e64fd0da/qwen-vl-utils/README.md)
- [仓库 API](https://api.github.com/repos/QwenLM/Qwen3-VL)
