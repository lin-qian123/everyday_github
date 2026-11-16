<!-- markdownlint-disable MD013 -->

# Whisper（openai/whisper）

- GitHub：<https://github.com/openai/whisper>
- 核查：2026-11-17（Asia/Shanghai）07 时段；112,852 stars / 13,668 forks / 185 open issues（含 PR）；仓库 ID `537603333`。
- 热度：官方 Python daily +123；成熟项目补录，不是新模型首发。
- 固定 main：`86098128c0b4f24f0e2aa2994de830614b474227`；源码 / PyPI `20250625`，最新 Release [v20250625](https://github.com/openai/whisper/releases/tag/v20250625) 发布于 UTC 2025-06-26。
- 许可与证据：README 声明代码和模型权重 MIT。静态核读相关材料，未下载权重、处理录音、试听或测准确率。

## 定位

OpenAI 的多语言语音识别模型与 Python 推理参考实现，支持原语言转写、语言识别和向英语的语音翻译。它是 ASR 基础组件，完整的实时流、说话人分离与业务复核通常还需上层系统。官方首发是 [2022-09-21](https://openai.com/index/whisper/)，本轮日榜不能解释为新的发布事件。[固定 README](https://github.com/openai/whisper/blob/86098128c0b4f24f0e2aa2994de830614b474227/README.md)

## 用法

包名为 `openai-whisper`，导入名为 `whisper`，还需系统 `ffmpeg`。当前 PyPI latest 与源码版本均为 `20250625`。包清单要求 Python `>=3.8`，分类列到 3.13，而 README 仍写预期兼容 3.8–3.11；分类声明不能充当所有组合的运行验收。[包清单](https://github.com/openai/whisper/blob/86098128c0b4f24f0e2aa2994de830614b474227/pyproject.toml)、[PyPI 元数据](https://pypi.org/pypi/openai-whisper/json)

在独立环境安装固定包并准备已授权录音后，可按下面方式转写；以下命令未执行：

```bash
pip install openai-whisper==20250625
whisper sample.wav --model turbo --language Chinese --task transcribe
```

翻译任务的目标是英语，须改用支持翻译的多语言模型，例如 `medium`；`turbo` 未训练翻译任务，README 明确提示即使指定 translate 仍可能返回原语言。模型大小、精度和内存按实际机器选，不能把名称当能力承诺。

## 原理

encoder-decoder Transformer 把 log-Mel 音频特征映射为文本及语言 / 任务 / 时间戳 token。高层 `transcribe()` 按滑动的约 30 秒窗口自回归处理；这是批量接口的处理策略，不等于开箱即用的低延迟流式识别。音频加载调用 FFmpeg 解码为单声道、16 kHz 浮点数组。[音频预处理](https://github.com/openai/whisper/blob/86098128c0b4f24f0e2aa2994de830614b474227/whisper/audio.py)

`load_model()` 按模型名取权重，默认缓存目录为 XDG cache 或 `~/.cache/whisper`，并校验下载文件 SHA-256；权重缺失或校验不符时会联网下载。提供本地模型文件和依赖后才可设计离线路径，不能把首次启动称为天然无网络。[加载与下载](https://github.com/openai/whisper/blob/86098128c0b4f24f0e2aa2994de830614b474227/whisper/__init__.py)

## 价值

可为字幕、录音检索与研究访谈整理提供本地转写基线，便于固定模型并保留原音频与文本对照。README 的速度比较来自英语 / A100 条件，不能套用到中文、长音频或 Apple Silicon；没有本轮性能结果。

## 风险边界

- 模型卡明确指出可能输出音频中没有的文本、重复文字，且不同语言、口音表现不均。无声段、噪声、术语和姓名要回听；语言流畅不是内容正确的证据。[模型卡](https://github.com/openai/whisper/blob/86098128c0b4f24f0e2aa2994de830614b474227/model-card.md)
- 转写、翻译、时间戳和说话人分离是不同任务；模型卡未对 speaker diarization 等扩展作充分评估。不能把单份 transcript 当已核对的逐人记录。
- 文档存在数值口径漂移：README 的 turbo 参数表为 809 M，模型卡写 798 M；本轮不自行消除差异，也不据此反推实际显存 / 速度。
- 参考实现可以本地运行，但权重下载、包装服务、同步、遥测与用户自己接入的云服务须另核；代码及权重许可不替代录音授权和数据处理规则。
- MIT、模型完整性校验与安装成功不证明识别质量、部署安全或高风险用途适用。没有做录音处理、断网验证、平台兼容或端到端听评。

## 补充建议

用有人工参考文本的代表样本，分开统计中文 CER / 英文 WER、无声段幻觉、时间对齐、时延与峰值内存。保留音频时间段到文本的映射，对专名、数字和结论逐项回听；输出摘要时明确哪些来自 ASR、哪些是人工确认。部署前固定包、权重哈希、FFmpeg 与运行配置。

## 参考资料

- [仓库 API](https://api.github.com/repos/openai/whisper)、[v20250625](https://github.com/openai/whisper/releases/tag/v20250625)、[PyPI](https://pypi.org/pypi/openai-whisper/json)。
- [版本文件](https://github.com/openai/whisper/blob/86098128c0b4f24f0e2aa2994de830614b474227/whisper/version.py)、[MIT](https://github.com/openai/whisper/blob/86098128c0b4f24f0e2aa2994de830614b474227/LICENSE)，以及正文固定 SHA 文档 / 实现；未执行模型推理。
