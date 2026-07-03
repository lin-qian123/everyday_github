# local-llm

- GitHub：<https://github.com/jamesob/local-llm>
- 抓取时间：2026-07-04（Asia/Shanghai）
- 今日信号：GitHub API 显示该仓库创建于 2026-07-03，抓取时约
  `292 stars / 7 forks`，主题集中在本地运行高端 LLM、GPU 互联、
  vLLM Docker 配置和本地语音转文字。

## 定位

`local-llm` 是 James O'Beirne 对“在本地运行接近前沿能力的大模型”的
硬件、系统与运行配置记录。它不是一个通用框架，而是一份可复查的
本地 AI 基础设施手册：从 2 张二手 RTX 3090 的低预算方案，到 4 张
RTX PRO 6000 的高 VRAM 方案，再到 PCIe switch、NCCL、Docker runner
和 STT 配置。

它代表的热点不是“又一个聊天 UI”，而是开发者开始认真评估：在 2026 年，把模型、语音转写和 agent 运行尽量留在本地，究竟需要什么硬件、系统参数和维护成本。

## 用法

仓库主要通过 README 和 `runners/` 目录交付：

```bash
git clone https://github.com/jamesob/local-llm
cd local-llm
ls runners
```

典型使用方式包括：

- 阅读硬件 BOM，判断 48GB、384GB VRAM 等不同预算下能跑什么模型。
- 参考 `runners/GLM-5.2-594B` 这类目录，理解 vLLM、Docker Compose、DCP / MTP 等 serving 参数。
- 使用 `tools/measure-gpu-speed.sh` 做 GPU P2P 带宽和延迟测量。
- 参考 `runners/stt` 搭建本地 `whisper-large-v3` 语音转文字服务。

## 原理

该项目的核心是把“本地前沿模型运行”拆成几个工程层：

1. **VRAM 预算**：模型大小、量化方式、上下文长度和并行策略决定需要多少显存。
2. **GPU 互联**：多卡推理不只看单卡算力，还依赖 P2P 带宽、PCIe 拓扑、ACS、IOMMU 和 NCCL 行为。
3. **服务封装**：用 vLLM / Docker Compose 把复杂启动参数固定下来，减少每次手工调参。
4. **输入层本地化**：语音转文字同样可放在本地 GPU 上，形成更完整的隐私优先 AI 工作流。

## 价值

- 给本地模型实践者提供真实 BOM、系统参数和踩坑记录，而不是抽象 benchmark。
- 帮助判断“买云端 API”与“自建本地推理机器”的成本、隐私、维护复杂度差异。
- 对 agent 开发者有参考意义：本地模型如果要承担编码、语音、长上下文任务，瓶颈通常在系统工程而非单个 prompt。
- 可作为 `ollama`、`vllm`、`Rapid-MLX`、`llama.cpp` 等项目之外的实践型补充。

## 风险边界

- README 中的硬件价格、模型选择和最佳配置会快速过期，不能当成长期采购建议。
- 高端多卡机器涉及供电、散热、驱动、BIOS、PCIe 拓扑和 Docker/NVIDIA runtime 维护，不适合没有系统经验的用户直接复制。
- 仓库是个人实践记录，不是经过广泛硬件组合验证的厂商方案。
- 本地运行不等于自动安全：模型权重来源、服务暴露、日志和本地数据权限仍需单独治理。

## 补充建议

- 与 `vllm`、`ollama`、`Rapid-MLX` 放在一起观察：前者偏生产 serving，后两者偏易用和 Apple Silicon，本项目偏高端本地硬件实战。
- 如果只想低成本入门，本项目的 2x RTX 3090 和 STT 部分比 4x RTX PRO 6000 更有参考价值。
- 后续可跟踪仓库是否继续更新 GLM、Qwen、DeepSeek、Kimi 等开放权重模型的 runner。

## 参考资料

- GitHub 仓库：<https://github.com/jamesob/local-llm>
- vLLM：<https://github.com/vllm-project/vllm>
- Whisper large-v3：<https://huggingface.co/openai/whisper-large-v3>
