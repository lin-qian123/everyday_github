<!-- markdownlint-disable MD013 MD034 -->

# VoiceStudio：本地优先的语音克隆、配音与转写工作台

## 项目概览

- 上游仓库：https://github.com/debpalash/VoiceStudio
- GitHub API 快照（2026-09-01）：12,684 stars、1,964 forks、28 个开放 issue
- 当前 release：`v0.5.1`；上游标记为 active beta
- 主要技术：Tauri、Python backend、TTS / ASR、CUDA / MPS / ROCm
- 主项目许可证：AGPL-3.0；可选引擎和模型保留各自许可证

## 定位

VoiceStudio 是桌面语音生产工作台，覆盖语音克隆与设计、视频配音、听写、转写、说话人分离、长篇故事/有声书和批处理。它集成多种 TTS/ASR 引擎，并提供本地 API、OpenAI 兼容音频接口和 MCP Server。

## 用法

普通用户可从 release 下载 macOS、Windows 或 Linux 包；首次启动会创建托管 Python 环境并下载默认模型。从源码运行的上游入口是：

```bash
git clone https://github.com/debpalash/VoiceStudio.git
cd VoiceStudio
bun install
bun run desktop
```

语音克隆需要用户提供干净参考音频。使用任何非本人声音前，应先取得明确授权，并为生成内容设置标识、保存同意记录。

## 原理

Tauri 桌面前端连接 Python 服务，后端通过 registry 选择 TTS、ASR、分离、翻译和水印引擎。视频配音管线通常经过提取音轨、转写/说话人分离、翻译、语音生成、时间对齐和重新封装；批处理与远程 worker 承担长任务和 GPU 调度。

“646 种语言”是目录规模，不表示每个引擎、口音和任务都有同等质量。实际覆盖由所选模型、语言、参考音频和硬件决定。

## 价值

- 把多种语音引擎和常见生产任务放进同一可视化工作台。
- 本地默认存储有利于处理内部音频，但仍需核对可选联网功能。
- 桌面、REST/SSE/WebSocket、OpenAI 兼容 API 和 MCP 适合不同工作流。
- 自检、诊断 bundle、批队列和 remote worker 有助于定位复杂环境问题。

## 风险边界

- 语音克隆可能被用于冒充、诈骗、骚扰或未经同意的身份再现。
- 本地运行不自动解决训练数据、声音权利、音乐/视频版权和跨境隐私义务。
- 可选模型、引擎和 worker 可能有不同许可、下载来源和网络出口。
- active beta、平台打包和大模型依赖意味着安装、GPU 兼容和输出质量仍可能波动。
- 本页基于静态源码树、API 与 README；未实际复现语音质量、语言覆盖或水印效果。

## 补充建议

1. 只用本人或已授权的参考音频，保存用途、期限、撤回和再分发授权。
2. 记录每个输出的引擎、模型、版本、参数、参考音频哈希和后处理步骤。
3. 对远程 worker、模型下载和 optional network feature 做抓包与凭据审计。
4. 用多说话人、噪声、方言和长视频测量转写、对齐、音色相似与失败模式。
5. 对外发布时使用显著标识，并独立验证 AudioSeal 等水印在转码、剪辑后的可检测性。

## 参考资料

- 仓库与 README：https://github.com/debpalash/VoiceStudio
- 官方站点：https://voicestudio.sh
- 中文 README：https://github.com/debpalash/VoiceStudio/blob/main/README_CN.md
- 安装文档：https://github.com/debpalash/VoiceStudio/tree/main/docs/install
- 性能基准说明：https://github.com/debpalash/VoiceStudio/blob/main/docs/benchmarks.md
