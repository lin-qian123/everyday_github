<!-- markdownlint-disable MD013 -->

# speech-to-speech

> Hugging Face 的开源本地语音 agent 组合工具：将语音活动检测（VAD）、语音识别（STT）、LLM 与语音合成（TTS）拼成可替换的实时链路。

- 上游仓库：[huggingface/speech-to-speech](https://github.com/huggingface/speech-to-speech)
- 许可证：Apache-2.0
- 本轮快照：2026-08-13，GitHub REST API 约 `12.4k` stars、`1.5k` forks；GitHub Trending 页面当时显示当天约 `627` stars。以上计数会随时间变化。
- 分类：语音、视频与多模态

## 定位

`speech-to-speech` 不是单一端到端语音模型，而是面向实时语音 agent 的可替换流水线。它提供 OpenAI Realtime 兼容的 WebSocket 服务、命令行客户端和本地/远端 LLM 后端选择；上游默认组合本地 Parakeet TDT STT、OpenAI 兼容 LLM 和 Qwen3-TTS。适合希望控制语音链路、在不同模型间试验，或优先在本机运行的开发者。

## 用法

最小路径需要 Python 环境和一个可用的 OpenAI 兼容 LLM：

```bash
pip install speech-to-speech
export OPENAI_API_KEY=...
speech-to-speech serve

# 另一个终端：连接默认的 Realtime 兼容服务
speech-to-speech talk --url ws://127.0.0.1:8765/v1/realtime
```

`speech-to-speech local` 可一并启动服务与打包的麦克风/扬声器客户端。若需完全本地，README 给出了先用 `llama.cpp` 启动兼容服务、再通过 `--responses_api_base_url` 指向该服务的路线。项目还以 pip extras 提供 Whisper、MLX、Kokoro、Pocket TTS 等可选后端；安装前应按操作系统、CUDA runtime 与目标语言逐项核对兼容性。

## 原理

1. VAD / endpointing 判断何时开始、结束一轮说话；
2. STT 将音频转成文本，交给选定的 LLM 或兼容 API；
3. LLM 可调用工具并流式生成回复；
4. TTS 将回复转回语音，通过 Realtime 协议交给客户端。

模块替换使延迟、语言覆盖、成本和本地化程度能够分别调节，但端到端体验仍由最慢模块和停顿判定共同决定。

## 价值

- 以可观察、可替换模块取代黑箱式语音 agent 服务，利于做延迟和效果对照。
- 支持本地模型服务与离线运行路径，可减少部分语音/文本外发依赖。
- 兼容 Realtime 客户端，有利于把既有界面或设备接到不同语音后端。

## 风险边界

- 语音输入可能包含身份、位置和敏感业务信息；连接云端 LLM、下载模型或开启日志前，必须明确数据流、留存和访问权限。
- TTS/声音相关能力不等于可复制、模仿或发布任何人的声音；应获得声音主体授权，并在面向他人时披露自动生成属性。
- VAD 的端点阈值会影响打断、漏听和延迟；默认配置不是跨语言、噪声环境或辅助无障碍场景的质量保证。
- CUDA wheel、模型权重和额外后端各有自己的平台/许可证约束；不能只依据本仓库的 Apache-2.0 许可证判断整个部署的合规性。

## 补充建议

- 先用录制的、已获授权的短音频做离线回放，分别记录首音频延迟、打断恢复、转写错误和总成本。
- 将 STT、LLM、TTS 的模型版本和参数写入部署清单；遇到体验下降才有可复现的回归依据。
- 生产接入前为工具调用设置最小权限和人工确认，且将音频、文本 transcript、密钥与调试日志分别做脱敏和保留期控制。

## 参考资料

- [项目 README：安装、Realtime API 与后端选择](https://github.com/huggingface/speech-to-speech#readme)
- [GitHub 仓库元数据](https://api.github.com/repos/huggingface/speech-to-speech)
- [GitHub Trending 观察入口](https://github.com/trending)
