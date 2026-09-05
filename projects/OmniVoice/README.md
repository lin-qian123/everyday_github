<!-- markdownlint-disable MD013 -->

# OmniVoice（k2-fsa/OmniVoice）

> 记录日期：2026-09-06（Asia/Shanghai）。本页依据上游 README、模型卡、论文、release、LICENSE 与 GitHub REST API 做静态整理；本轮未下载模型、未合成音频，也未复现上游速度或质量指标。

## 定位

`OmniVoice` 是 k2-fsa 发布的多语种 zero-shot text-to-speech（TTS）项目，面向语音克隆、文字描述驱动的 voice design、自动选声和批量合成。上游称其覆盖 600 多种语言，并采用 diffusion language model 风格架构。

2026-09-06 的 GitHub 官方 Python Trending 抓取显示约 `+83 stars today`；REST API 快照为 `9,910 stars / 1,609 forks / 58 open issues`，最新 release 为 `0.2.1`。仓库代码为 Apache-2.0，但 Hugging Face 模型卡明确写明预训练模型受训练数据约束采用 `CC-BY-NC`，代码许可不能直接外推到权重和生成内容用途。

## 用法

上游将 PyPI 作为稳定安装入口，并要求先按硬件安装匹配的 PyTorch：

```bash
pip install omnivoice
```

最小 voice-cloning 调用形态如下；正式使用前应先取得说话人明确授权，并保留授权范围与撤回方式：

```python
from omnivoice import OmniVoice
import soundfile as sf
import torch

model = OmniVoice.from_pretrained(
    "k2-fsa/OmniVoice",
    device_map="cuda:0",
    dtype=torch.float16,
)
audio = model.generate(
    text="This is a test.",
    ref_audio="authorized-reference.wav",
    ref_text="Transcription of the reference audio.",
)
sf.write("output.wav", audio[0], 24000)
```

项目还提供 `omnivoice-demo`、`omnivoice-infer` 与 `omnivoice-infer-batch`。README 提示参考音频宜为 3–10 秒；Apple Silicon 可选择 `mps`，Intel GPU 可选择 `xpu`，具体依赖和性能仍须按平台验证。

## 原理

- **多语种 zero-shot TTS**：用参考语音与目标文本生成新语音，不要求为每位说话人单独训练模型。
- **Diffusion language model 路线**：论文与 README 将生成过程描述为 diffusion language model 风格的语音建模架构。
- **三种生成模式**：voice cloning 使用参考音频；voice design 使用文字声线描述；auto voice 不提供参考声线。
- **辅助转写**：省略 `ref_text` 时可借助 Whisper 自动转写参考音频，这会额外引入 ASR 错误与资源消耗。
- **批处理与加速**：CLI 支持多 GPU batch inference；上游还提供 FlashInfer/CUDA graph 加速路径。
- **训练与评测入口**：`examples/` 覆盖数据准备、训练、评测和微调，论文与模型卡提供模型背景。

## 价值

- 将多语言、跨语言克隆、voice design、CLI、Python API 与批处理放进同一套公开代码接口。
- 对语音研究、无障碍朗读、授权配音和低资源语言实验提供统一起点。
- 同时开放论文、代码、模型卡与训练/评测入口，便于追踪声明来自何处。
- CUDA、XPU 和 MPS 路径扩大硬件覆盖，但不能据此推定所有后端具有相同质量和吞吐。

## 风险边界

- 上游的“600+ languages”“state of the art”“2–2.9x”等是项目声明或固定 H100 benchmark，不是本仓库复现实测；低资源语言、口音、韵律和长文本须分层评测。
- Voice cloning 可被用于冒充、欺诈和未授权生物特征处理；免责声明不能替代同意、身份核验、内容标记与滥用响应。
- 代码 Apache-2.0，预训练模型则为 CC-BY-NC；商业使用、再分发、微调权重和数据来源须分别审查。
- 参考音频、自动转写文本、生成文件和缓存都可能含敏感个人信息；本地运行也不自动等于已满足删除、访问控制和审计要求。
- Cross-lingual cloning 可能保留来源语言口音；voice design 主要以中英文数据训练，上游也提示其他语言可能不稳定。
- 合成音频可出现错读、数字归一化、停顿、情绪或说话人相似度偏差，不能用于未经复核的医疗、法律、金融或紧急通知。

## 补充建议

- 建立已授权说话人清单、用途/期限/渠道范围和一键撤回流程，不使用网络抓取的陌生人语音做参考。
- 按语言、方言、性别/年龄、噪声、参考长度、跨语言和长文本建立人工听测与 ASR/WER 辅助评测集。
- 将代码、权重、训练数据与输出资产分别登记许可证；商业项目在法务确认前不要采用 CC-BY-NC 权重。
- 在可丢弃环境固定 commit、模型 revision、PyTorch/CUDA、seed、步数和硬件，再复现 RTF、显存与质量。
- 对外发布时加入“合成语音”披露、可验证 provenance 或水印，并测试转码、剪辑和噪声后的可检测性。

## 参考资料

- [GitHub 仓库](https://github.com/k2-fsa/OmniVoice)
- [GitHub REST API](https://api.github.com/repos/k2-fsa/OmniVoice)
- [0.2.1 Release](https://github.com/k2-fsa/OmniVoice/releases/tag/0.2.1)
- [Hugging Face 模型卡](https://huggingface.co/k2-fsa/OmniVoice)
- [OmniVoice 论文](https://arxiv.org/abs/2604.00688)
- [语言列表](https://github.com/k2-fsa/OmniVoice/blob/master/docs/languages.md)
- [训练与评测示例](https://github.com/k2-fsa/OmniVoice/tree/master/examples)
