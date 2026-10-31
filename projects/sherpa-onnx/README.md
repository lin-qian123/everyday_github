<!-- markdownlint-disable MD013 -->

# sherpa-onnx

- 上游：[k2-fsa/sherpa-onnx](https://github.com/k2-fsa/sherpa-onnx)；分类：语音、视频与多模态。
- 核读：2026-11-01（Asia/Shanghai）；固定主线 `935e5ded3d949a8b557ac44ef4dad03a7d2038e7`。
- [仓库 API](https://api.github.com/repos/k2-fsa/sherpa-onnx) 快照：15,649 stars / 1,835 forks / 639 open issues（含 PR）；发行首项 [v2.0.1](https://github.com/k2-fsa/sherpa-onnx/releases/tag/v2.0.1)，2026-10-26 UTC。发行与主线分别看。
- 证据：上游文档及指定文件静态核读；本轮未安装运行、调用模型或复现作者实验。

## 定位

以 ONNX Runtime 为核心的跨平台语音推理工具集，涵盖流式 / 非流式识别、TTS、VAD、说话人分离、增强与分离等能力，并提供多种语言绑定。不是单一识别模型，也不是所有平台功能完全一致的成品应用。官方 C++ daily 榜本轮显示 +26 stars；v2.0.1 发行记录含 VoxLock 目标说话人隔离及多种绑定更新。

## 用法

先选一个明确模型与 CPU 文件解码路径，不从全平台编译开始：

```bash
python -m pip install 'sherpa-onnx==2.0.1' soundfile
git clone https://github.com/k2-fsa/sherpa-onnx.git
cd sherpa-onnx
git checkout 935e5ded3d949a8b557ac44ef4dad03a7d2038e7
python python-api-examples/offline-sense-voice-ctc-decode-files.py
```

运行前必须按该示例头部说明下载并解压 SenseVoice int8 模型包，放在当前目录；模型在 `asr-models` 资源发行中单独提供，wheel 不包含全部模型。示例读取包内 `test_wavs/zh.wav`，验证成功后再换成自己的授权音频。上面的安装与解码本轮均未执行。

示例选择 `model.int8.onnx` / `tokens.txt`，调用 `OfflineRecognizer.from_sense_voice`，读取 float32 音频并取第一声道，再 accept waveform、decode、读取结果；原例说明采样率不必固定 16 kHz，仍需遵循所选模型的输入约束。

## 原理

框架把特征处理、模型格式、解码策略和绑定接口组织起来；ONNX 模型及 token 文件承载识别能力，stream 对象管理输入和输出。流式 / 离线、CTC / transducer 等模型路径有不同状态、延迟和上下文需求，不能只替换一个文件名。

本地推理可在预先取得模型后离线运行；仓库也提供 websocket client / server 和在线 demo。选择服务模式后，音频跨网络传输与服务访问控制属于应用架构的一部分。

## 价值

为桌面、移动、嵌入式及多语言应用提供一致的语音集成入口，适合构建不依赖 hosted STT 的语音界面。模型选择、量化和硬件适配是实际成本所在，框架可用不代表识别率或实时性达标。

## 风险边界

- 项目代码 Apache-2.0，所下载模型、声音和训练数据可能有独立许可；不能把代码许可自动套给所有模型资源。
- “无需联网”只适用于已下载依赖 / 模型的本地路径；在线 demo、模型下载与 websocket 部署有各自出口。
- 识别、VAD、diarization、语音增强是不同任务，模型支持和硬件后端需逐项确认。口音、噪声、重叠说话和低精度量化可能改变结果。
- 示例第一声道处理会丢掉其他声道信息；涉及会议双通道或分离效果时，应先定义声道、采样率和参考标签。
- 本轮未下载模型、测延迟 / WER、部署服务或复现 VoxLock 效果，发行说明不是本轮实验结果。

## 补充建议

固定 wheel、源码 SHA、模型文件 SHA256 与实际后端；先做数十条有人工稿的短音频，统计 WER / CER、数字实体错误、实时因子、首字延迟与峰值内存。增加噪声 / 口音 / 重叠样本后再决定端侧模型，并分别验离线与服务路线。

## 参考资料

- [固定 README / 平台与任务范围](https://github.com/k2-fsa/sherpa-onnx/blob/935e5ded3d949a8b557ac44ef4dad03a7d2038e7/README.md)。
- [SenseVoice 文件解码示例](https://github.com/k2-fsa/sherpa-onnx/blob/935e5ded3d949a8b557ac44ef4dad03a7d2038e7/python-api-examples/offline-sense-voice-ctc-decode-files.py)。
- [Python 包安装定义](https://github.com/k2-fsa/sherpa-onnx/blob/935e5ded3d949a8b557ac44ef4dad03a7d2038e7/setup.py)。
- [离线 websocket 服务入口](https://github.com/k2-fsa/sherpa-onnx/blob/935e5ded3d949a8b557ac44ef4dad03a7d2038e7/sherpa-onnx/csrc/offline-websocket-server.cc)。
- [Apache-2.0 代码许可](https://github.com/k2-fsa/sherpa-onnx/blob/935e5ded3d949a8b557ac44ef4dad03a7d2038e7/LICENSE)。
