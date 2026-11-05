<!-- markdownlint-disable MD013 -->

# VibeVoice（microsoft/VibeVoice）

- 更新：2026-11-06（Asia/Shanghai）；官方 综合 daily +214，为读取快照，不是自然日结算。
- GitHub API：55,857 stars / 6,280 forks / 205 open issues（含 PR）；仓库 ID `1044296738`。
- 核读基线：`16fb2cb1217c9934a886e1948ffb06120caa2df5`；文档与抽样实现核验，不是安装运行、安全或性能认证。

## 定位

Microsoft 的语音模型家族，需按任务区分：长音频 ASR、增量 ASR-Streaming、单说话人 Realtime TTS，以及另外仓库中的 CPU BitNet 路径。2026-09-03 的增量 ASR 是已有历史发布，今日综合榜关注增长不等于新模型发布。

**旧页纠正**：上游说明因不当使用，已于 2025-09-05 从本仓库撤下原 VibeVoice-TTS 代码；模型表也标 Disabled。README 仍保留 90 分钟 / 四说话人介绍，不能把它当当前已提供的完整可运行路径。

## 用法

Python 要求 >=3.10。先按所选模型文档准备匹配的 CUDA / PyTorch 环境与权重，固定本页 commit 后安装：

```bash
pip install -e .
python demo/vibevoice_asr_inference_from_file.py --model_path /path/to/asr-checkpoint --audio_files /path/to/audio.wav
python demo/vibevoice_asr_streaming_inference_from_file.py --model_path /path/to/streaming-checkpoint --audio_files /path/to/audio.wav
```

两条推理命令是不同 checkpoint 路径的示例，不能混用。流式模型的 chunk / lookahead 来自权重的 `preprocessor_config.json`。需要网页演示时，先核 host / 端口 / 认证；Gradio 实现默认 host 为 `0.0.0.0`，`--share` 会创建公开链接，旧页不应把它作为默认本地上手方式。

Realtime TTS 按独立文档与依赖安装；`streamingtts` extra 固定 Transformers 4.51.3，根依赖范围则为 >=4.51.3、<5.0.0。本轮未下载权重、转写、合成、录音或启动服务。

## 原理

长音频 ASR 将识别、说话人和时间戳一起建模，上游标称可在 64K 上下文处理最长约 60 分钟；增量 ASR 按音频 chunk 输出。Realtime TTS 使用交错窗口与扩散声学生成，文档明确移除了完整多说话人版本的 semantic tokenizer，仅用 7.5 Hz acoustic tokenizer。不能把家族总览中的双 tokenizer / diffusion 描述无差别套到每个模型。

## 价值

ASR 的 Who / When / What 结构适合会议、访谈与长录音后处理；流式路径降低等整段结束的等待。实时 TTS 则面向逐段输入文字的发声。应分别量化识别错误、说话人归属、时间戳、首包延迟和整段吞吐，不以单个“实时”标签替代全部指标。

## 风险边界

- **模型范围不相同**：README 对离线 ASR 标 50+ 语言、流式新闻标 10 语言；Realtime 主要面向英语、单说话人，额外九种语言属未充分测试的探索。不能相互借用语言 / 多人能力。
- **上游延迟措辞不一致**：README 写约 300 ms，Realtime 专页写约 200 ms 且依赖硬件；本轮均未复测，应固定硬件、音频长度、batch 与计时定义。
- **CPU / 量化是另一条路径**：BitNet 的 1.58 GB 和 RTF<1 来自另仓库 / 特定条件，不能作为本仓库所有 7B 模型的内存与速度保证。
- **网络与内容**：权重下载、云 Playground、Colab、公开分享链接与本地推理数据流不同。语音授权、个人信息和合成标记需按真实用途处理。
- 根代码为 MIT；单独权重及第三方组件条件须看相应 model card / LICENSE。转写可能漏词、错分人或幻觉，热词提示也不保证正确；关键记录必须对照原音频。

## 补充建议

用授权的多说话人短音频和真实术语集建立金标，再分开测试离线 / 流式 ASR。记录 WER / CER、说话人错误、时间戳误差、chunk 等待、首包和峰值显存；TTS 还需完整试听可懂度、稳定性和音色。部署前核默认监听地址与分享选项，避免把演示服务器直接视为生产服务。

## 参考资料

- [README.md](https://github.com/microsoft/VibeVoice/blob/16fb2cb1217c9934a886e1948ffb06120caa2df5/README.md)
- [pyproject.toml](https://github.com/microsoft/VibeVoice/blob/16fb2cb1217c9934a886e1948ffb06120caa2df5/pyproject.toml)
- [docs/vibevoice-asr.md](https://github.com/microsoft/VibeVoice/blob/16fb2cb1217c9934a886e1948ffb06120caa2df5/docs/vibevoice-asr.md)
- [docs/vibevoice-asr-streaming.md](https://github.com/microsoft/VibeVoice/blob/16fb2cb1217c9934a886e1948ffb06120caa2df5/docs/vibevoice-asr-streaming.md)
- [docs/vibevoice-realtime-0.5b.md](https://github.com/microsoft/VibeVoice/blob/16fb2cb1217c9934a886e1948ffb06120caa2df5/docs/vibevoice-realtime-0.5b.md)
- [demo/vibevoice_asr_gradio_demo.py](https://github.com/microsoft/VibeVoice/blob/16fb2cb1217c9934a886e1948ffb06120caa2df5/demo/vibevoice_asr_gradio_demo.py)
- [仓库与 API 快照](https://api.github.com/repos/microsoft/VibeVoice)；[发行列表](https://github.com/microsoft/VibeVoice/releases)。
