# LTX-2（Lightricks/LTX-2）

- GitHub: https://github.com/Lightricks/LTX-2
- 模型页: https://huggingface.co/Lightricks/LTX-2.3
- 论文: https://arxiv.org/abs/2601.03233
- 记录日期: 2026-06-20 (Asia/Shanghai)

## 定位

`LTX-2` 是 Lightricks 开源的音视频基础模型与推理/训练工具栈。它的野心不是只做 text-to-video，而是把同步音视频、高保真输出、不同性能模式、API 访问、LoRA 训练和多种 pipeline 收到同一套模型体系中。

## 热度信号

1. GitHub API 在 2026-06-20 抓取时显示约 `7.7k stars`、`1.2k forks`，并进入 GitHub Trending 日榜。
2. 官方 README 直接称其为 `the first DiT-based audio-video foundation model`，并强调 `synchronized audio and video`、`multiple performance modes`、`production-ready outputs`。
3. 仓库不仅给出模型，还给出 `ltx-core`、`ltx-pipelines`、`ltx-trainer` 三个包，以及 ComfyUI 集成、LoRA 与多条视频生成 pipeline，说明它是完整生态，而不是单个 checkpoint。

## 用法

### 1) 克隆并准备环境

README 的 Quick Start 很直接：

```bash
git clone https://github.com/Lightricks/LTX-2.git
cd LTX-2
uv sync --frozen
source .venv/bin/activate
```

### 2) 下载模型与附加组件

官方要求从 Hugging Face 下载：

- `LTX-2.3` 主模型 checkpoint
- spatial / temporal upscaler
- distilled LoRA
- Gemma 文本编码器
- 若干 camera / control / lipdub LoRA

### 3) 选择 pipeline

README 明确列出的主要路径包括：

- `TI2VidTwoStagesPipeline`：高质量 text/image-to-video
- `DistilledPipeline`：更快推理
- `A2VidPipelineTwoStage`：audio-to-video
- `ICLoraPipeline`：video-to-video / image-to-video
- `LipDubPipeline`：口型重配与重述

## 原理

1. 仓库把推理、pipeline 和训练拆成独立包，形成“模型内核 + 应用管线 + 微调训练”的完整结构。
2. 通过 two-stage、distilled、upscaler、IC-LoRA 等设计，它试图在质量、速度和控制能力之间做分层取舍。
3. 从 README 能看出，项目很重视 production 级工作流，因此专门提供 ComfyUI 集成、推理优化建议和大量可复用 LoRA。
4. 这使它更像一个开放视频生成平台底座，而不是孤立的研究论文复现仓库。

## 价值

- 对做视频生成、音视频同步、后期可控编辑和模型微调的团队来说，它提供了非常完整的开源入口。
- 它说明多模态热点已经从“出图”扩展到“声音、镜头控制、口型、时间区域重生成”这样的更复杂视频生产环节。
- 与 `OpenMontage`、`palmier-pro` 这类工作流项目结合看，`LTX-2` 更像底层生成能力供给侧。

## 风险边界

- 模型与附加组件体量大，部署和显存门槛都不低，不适合轻量环境直接上手。
- README 展示的是丰富能力集合，但不同 pipeline 的质量、速度和稳定性很可能差异明显，不能默认“一套全都成熟”。
- 视频生成涉及内容安全、版权、肖像、配音和合成真实性问题，尤其是 `LipDubPipeline` 这类能力，落地时要单独做合规评估。

## 补充建议

1. 第一次评估时优先选择单一 pipeline，例如 `DistilledPipeline` 或 `TI2VidTwoStagesPipeline`，先看部署成本与输出稳定性。
2. 如果你更关心工作流整合，可以把它和 ComfyUI、时间线编辑器、视频 agent 流水线一起看，而不是只看 benchmark。
3. 对研究团队，最值得追踪的是它的“统一音视频基础模型”路线是否会继续向实时性、可控性和低成本推理推进。

## 参考资料

- https://github.com/Lightricks/LTX-2
- https://huggingface.co/Lightricks/LTX-2.3
- https://arxiv.org/abs/2601.03233
- https://github.com/Lightricks/ComfyUI-LTXVideo/
- https://github.com/trending
