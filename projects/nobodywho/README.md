<!-- markdownlint-disable MD013 -->

# NobodyWho（nobodywho-ooo/nobodywho）

> 上游仓库：<https://github.com/nobodywho-ooo/nobodywho> · 归类：模型、训练与推理基础设施 · 本页基于 2026-09-26 的 GitHub API、README、Changelog、Security Policy、Release 与 LICENSE 静态整理，未下载模型或在任何设备运行推理。

- 抓取快照：1,414 stars、87 forks、20 open issues。
- 热度信号：GitHub Rust Trending 抓取时约 +30 当日 stars。
- 版本与许可：EUPL-1.2；latest GitHub Release 为 Swift binding `nobodywho-swift-v4.0.0`，bindings 独立发布，tags 已出现 `v5.3.1`。

## 定位

NobodyWho 是跨桌面、移动端与游戏引擎的本地 AI 推理 SDK，用一套 Rust core 向 Python、Kotlin、Swift、React Native、Flutter 和 Godot 暴露 chat、tool calling、视觉 / 音频输入、TTS、STT、VAD、embedding 与 reranking 能力。

## 用法

用户可通过 PyPI、Maven、Swift Package Manager、npm、pub.dev 或 Godot AssetLib 选择对应 binding；模型既可使用本地路径，也可用 `hf:owner/repo:QUANT` 或 URL 在首次调用时下载缓存。桌面建议从小型 Qwen GGUF 验证内存与 backend；实验性 local server 在 `127.0.0.1:8888` 提供部分 OpenAI Chat Completions 接口。

## 原理

多语言 binding 通过 PyO3、UniFFI、flutter_rust_bridge 或 gdext 连接 Rust core。文本、vision、embedding 和 reranking 主要走 llama.cpp，语音相关路径使用 ONNX Runtime；Vulkan、Metal、CUDA 或 CPU 承担计算。schema / grammar 可约束 tool calling，本地模型和媒体文件由应用侧加载到同一 Chat / speech surface。

## 价值

它解决了端侧应用在多语言、多平台重复封装推理引擎的问题，并把 chat、工具、图像、音频和语音接口合并到一致的 SDK 心智模型。无需云 API key 可减少默认外发，移动端 / Godot / Flutter / React Native binding 对交互应用尤其有复用价值。

## 风险边界

- “本地离线”只描述推理路径；使用 Hugging Face / URL 会联网下载并缓存模型，模型来源、hash、恶意格式与供应链仍需验证。
- 代码采用 EUPL-1.2，修改并分发仓库代码有互惠义务；模型权重、应用商店包和 llama.cpp / ONNX 依赖仍有各自许可。
- output 与 tool call 必须视为不可信输入；grammar 保证结构不保证语义、权限或安全，真实工具仍须独立授权与参数校验。
- 各 binding 独立发布，GitHub latest Release、tags、package 版本并非一个全局版本；文档示例必须与实际 binding / artifact 对齐。
- 上游内存下限、backend 支持和移动设备建议不是本轮实测；不同模型、量化、温控、设备散热和 OS 内存策略会显著改变性能与稳定性。

## 补充建议

先固定 binding、commit、GGUF revision 与 SHA-256，在离线设备上以小模型做冷 / 热启动、峰值 RAM / VRAM、TTFT、tok/s、崩溃恢复和 battery / thermal 测试。为 tool calling 准备 schema 与恶意参数金标，服务模式只绑定 loopback 并加认证；发布应用前逐项核对模型卡、数据权利和 EUPL 义务。

## 参考资料

- [GitHub 仓库](https://github.com/nobodywho-ooo/nobodywho)
- [GitHub REST API](https://api.github.com/repos/nobodywho-ooo/nobodywho)
- [官方文档](https://docs.nobodywho.ooo/)
- [Changelog](https://github.com/nobodywho-ooo/nobodywho/blob/main/CHANGELOG.md)
- [Security Policy](https://github.com/nobodywho-ooo/nobodywho/blob/main/SECURITY.md)
- [LICENSE](https://github.com/nobodywho-ooo/nobodywho/blob/main/LICENSE)
