<!-- markdownlint-disable MD013 -->

# AudioCraft：研究音频生成与可控音乐生成的 PyTorch 工具箱

- 上游：[facebookresearch/audiocraft](https://github.com/facebookresearch/audiocraft)，仓库 ID `650945129`；本页新增于 2026-11-25。
- 快照：23,956 stars / 2,721 forks / 401 open issues（API 累计，含 PR）；Jupyter Notebook daily +9 stars。
- 版本：PyPI 最新字段为 `1.3.0`，制品上传于 2024-06-03；固定主线 `896ec7c47f5e5d1e5aa1e4b260c4405328bf009d` 的 `__version__` 为 `1.4.0a2`，提交日期 2025-03-13。API `pushed_at` 为 2026-03-03，不能当成默认分支提交日期或新发行日期。
- 证据范围：固定文档、模型卡、依赖、loader 局部源码及 PyPI / Hugging Face 元数据；未安装、下载权重、推理、训练、听评或完整观看视频。

## 定位

AudioCraft 是 Meta FAIR 的音频生成研究框架，集成 MusicGen、AudioGen、EnCodec、Multi Band Diffusion、MAGNeT、AudioSeal、MusicGen Style 与 JASCO 的相关代码 / 文档。不同组件支持的训练、推理、输入条件和模型许可要逐项查阅，不能把总目录等同于每项功能已在同一安装包中可用。

本页重点解释 MusicGen：通过文字或旋律条件生成音乐，适合研究可控生成、条件遵循与音频 token 建模。它没有因本轮上榜就成为 2026 年新发布模型。

## 用法

先选择稳定包还是固定源码，建立独立环境。README 要求 Python 3.9 / PyTorch 2.1.0；PyPI 的 `Requires-Python >=3.8.0` 是包元数据下限，不能证明所有相应解释器都能装好依赖。当前源码还固定 `av==11.0.0`、`numpy<2`、`torchvision==0.16.0`、`torchtext==0.16.0` 等旧组合，需匹配平台与 CUDA。

已核环境、许可及模型来源后，可从 small 模型做短音频试验。以下按上游 API 编写，**本轮未执行**；首次 `get_pretrained` 会通过模型仓库取得权重，不是离线空操作。

```python
from audiocraft.models import MusicGen
from audiocraft.data.audio import audio_write

model = MusicGen.get_pretrained('facebook/musicgen-small', device='cuda')
model.set_generation_params(duration=4)
wav = model.generate(['A short instrumental guitar melody'])
audio_write('demo', wav[0].cpu(), model.sample_rate,
            strategy='loudness', loudness_compressor=True)
```

示例需要可用 CUDA 环境与足够显存。MusicGen 文档建议约 1.5B 的 medium 模型至少 16 GB GPU 内存；small 300M 与短片段需求不同。源码自动选择逻辑也包含 CPU fallback，但这不证明 CPU / Apple MPS 的性能与所有依赖兼容，本轮未测试。

文字生成用 small / medium 等模型；旋律引导须选择 melody 变体与 `generate_with_chroma`。原生示例中 `--share` 会启用 Gradio 分享路径，展示本地 demo 前应按实际用途确认访问范围，不直接照抄为默认部署方式。

## 原理

MusicGen 先用 EnCodec 把 32 kHz 音频转成离散 token，再由单阶段自回归 Transformer 预测。它使用四个 codebook、50 Hz token 帧率，通过 codebook 间延迟模式让多路 token 交错预测；**50 个自回归步骤 / 音频秒是建模结构，不是实测生成速度或实时播放保证**。

文字条件控制风格与描述，melody 变体额外使用旋律条件；条件相似不等于逐音、和声、乐段或整首结构严格一致。立体声模型对两路 token 流采用交错处理，仍继承基础模型的能力与数据限制。

AudioCraft 还提供训练配置与不同任务的 solver；“代码可训练”不等于训练数据、算力和最终模型都能完整重现。

## 价值

它把音频 tokenizer、语言模型、条件控制、训练配置与评估接口放在可读的研究代码中，适合建立短音频基线、分析旋律条件和比较生成策略。对于音乐项目，可以先研究节奏、乐器音色和条件响应，再判断是否值得进一步投入人工整理。

模型卡分别列 FAD、KLD、CLAP 文本一致性和旋律相关指标，并说明人工评价。公开权重经过器乐分离，客观分数与论文模型有所不同；不能把论文表格、模型卡数值与本轮生成效果合并成一个验收结论。

## 风险边界

| 议题 | 已核事实与使用边界 |
| --- | --- |
| 代码与权重许可 | 代码 MIT；仓库 `LICENSE_weights`、MusicGen 模型卡及所查 small 模型卡均为 CC-BY-NC 4.0。安装开源代码不自动取得预训练权重的商业使用权。 |
| 版本与维护 | PyPI 1.3.0、源码 1.4.0a2 和仓库 `pushed_at` 是不同对象；本轮 GitHub Releases 列表为空不等于没有包或历史 tag。 |
| 模型下载与加载 | loader 接受本地路径、HTTPS 和 Hugging Face ID，并调用 `torch.load`；来源与序列化加载需单独信任，不能把任意下载 checkpoint 当普通媒体文件。 |
| 数据与旋律 | 作者称使用 20K 小时授权音乐；原始训练集未因发布代码自动开放。使用自己的旋律、录音和生成结果仍需核相应权利与用途。 |
| 质量与语言 | 模型卡说明以英语描述训练，其他语言和音乐文化覆盖不均，真实人声能力有限，可能出现突然收尾或静音。 |
| 评价范围 | 客观音频指标不能替代完整试听、结构 / 噪声检查与艺术接受；本轮没有生成或听过样本。 |

## 补充建议

1. 为目标机器固定 Python / torch / CUDA / AudioCraft SHA / 模型 revision，先核安装与短片段输出，再扩到长音频或训练。
2. 固定种子、prompt、片段时长与模型，分别记显存、墙钟时间、文本条件、旋律遵循和失败样本；不要把 token 帧率当生成吞吐。
3. 评价音乐时完整试听，单列节奏漂移、断句、尾部静音与声像问题；需要乐谱时另行转录和逐音复核。
4. 公布或商用前按实际权重与输入素材核许可；若只做研究，仍保留引用、版本和处理记录。

## 参考资料

- [仓库 API](https://api.github.com/repos/facebookresearch/audiocraft)、[PyPI 当前元数据](https://pypi.org/pypi/audiocraft/json)。
- [固定 README](https://github.com/facebookresearch/audiocraft/blob/896ec7c47f5e5d1e5aa1e4b260c4405328bf009d/README.md)、[CHANGELOG](https://github.com/facebookresearch/audiocraft/blob/896ec7c47f5e5d1e5aa1e4b260c4405328bf009d/CHANGELOG.md)、[源码版本](https://github.com/facebookresearch/audiocraft/blob/896ec7c47f5e5d1e5aa1e4b260c4405328bf009d/audiocraft/__init__.py)、[requirements](https://github.com/facebookresearch/audiocraft/blob/896ec7c47f5e5d1e5aa1e4b260c4405328bf009d/requirements.txt)。
- [固定 MusicGen 文档](https://github.com/facebookresearch/audiocraft/blob/896ec7c47f5e5d1e5aa1e4b260c4405328bf009d/docs/MUSICGEN.md)、[MusicGen 模型卡](https://github.com/facebookresearch/audiocraft/blob/896ec7c47f5e5d1e5aa1e4b260c4405328bf009d/model_cards/MUSICGEN_MODEL_CARD.md)、[small 权重模型卡](https://huggingface.co/facebook/musicgen-small/blob/main/README.md)。
- [模型加载路径](https://github.com/facebookresearch/audiocraft/blob/896ec7c47f5e5d1e5aa1e4b260c4405328bf009d/audiocraft/models/loaders.py)、[MusicGen API 与设备选择](https://github.com/facebookresearch/audiocraft/blob/896ec7c47f5e5d1e5aa1e4b260c4405328bf009d/audiocraft/models/musicgen.py)、[权重许可原文](https://github.com/facebookresearch/audiocraft/blob/896ec7c47f5e5d1e5aa1e4b260c4405328bf009d/LICENSE_weights)。
