<!-- markdownlint-disable MD013 -->

# TensorFold（ashhart/TensorFold）

> 上游仓库：<https://github.com/ashhart/TensorFold> · 归类：模型、训练与推理基础设施 · 本页基于 2026-09-29 的 GitHub API、README、Runbook、API / quantization 文档、Release、第三方声明与 LICENSE 静态整理，未下载模型、运行推理或复现性能数字。

- 抓取快照：554 stars、57 forks、20 open issues。
- 热度信号：GitHub Python Trending 抓取时约 +160 当日 stars。
- 版本与许可：代码 MIT，latest Release、tag 与包内版本均为 `v0.3.6.2` / `0.3.6.2`；模型权重、可选 draft checkpoint 与第三方组件另有许可。

## 定位

TensorFold 是面向 Apple Silicon MLX 与 NVIDIA CUDA 的本地大模型 serving 项目，对外提供 OpenAI-compatible API。它不是通用模型转换器，而是为 Nemotron、Qwen、GLM、Gemma 等列出的模型族提供专用 loader、kernel、draft verification、并发与 prompt-cache 路径。

## 用法

Python 3.11+ 环境可从 Git 安装，随后执行 `tensorfold serve <model-id>`；默认监听 `127.0.0.1:8080`，客户端把 `/v1` 作为 OpenAI-compatible base URL。`tensorfold info` 可先检查配置，`pull` 可提前下载权重；MLX 路径要求受支持的 macOS / MLX 版本，CUDA 路径应使用上游指定的 NVIDIA PyTorch 容器并按模型决定 rank、draft 与 quantization 参数。

## 原理

各模型族实现自己的投影、MoE、量化读取和 speculative drafting。draft token 只有在与同一 engine、weights、runtime、settings 下的串行结果一致时才被接受；`"draft": false` 可作同引擎对照。MLX 还实现按 token prefix 复用的 retained prefix、磁盘 spill 与 snapshot；CUDA 的并发、tensor parallel 和 KV cache 能力按模型族分别限制。

## 价值

它把本地模型、OpenAI-compatible endpoint、speculative decoding 与明确的内存 admission 放进同一服务，对使用 Mac 工作站或固定 NVIDIA 节点的 Agent / 应用较方便。上游还把 benchmark prompt、recipe、release measurement 与串行对照路径公开出来，便于建立可复现实验，而不是只看单一吞吐数字。

## 风险边界

- “exact”只指同一引擎、权重、runtime 与设置下 drafted / serial token 一致，不表示 MLX 与 CUDA、不同量化或不同 rank 的输出相同。
- 支持矩阵按具体 checkpoint、量化 group、draft head 与硬件变化；README 仍把若干路径标为 experimental 或 hardware qualification pending。
- `serve` / `pull` 会下载模型；模型、DFlash / MTP checkpoint 与 GLM 可选组件可能含非商业或其他独立条款，MIT 不能概括全部权利。
- prompt cache、spill 与 persistent snapshot 可能保存对话前缀；`--host 0.0.0.0` 又会扩大网络暴露，默认本地监听不等于生产鉴权。
- 吞吐、内存和并发数字依赖机器、runtime、checkpoint 与 prompt；本页未复现 release benchmark，也未把“可加载”写成“可稳定低延迟运行”。

## 补充建议

固定 Release、Python / MLX / CUDA runtime 与 checkpoint revision，保存启动报告和模型哈希。先用 `draft: false` 建立 correctness 基线，再测 drafting、并发和长上下文；敏感场景关闭 disk snapshot / spill，或将目录放入加密、限权存储。若需局域网访问，在前方增加认证、TLS、限流与审计，不直接公开 serving 端口。

## 参考资料

- [GitHub 仓库](https://github.com/ashhart/TensorFold)
- [GitHub REST API](https://api.github.com/repos/ashhart/TensorFold)
- [v0.3.6.2 Release](https://github.com/ashhart/TensorFold/releases/tag/v0.3.6.2)
- [Runbook](https://github.com/ashhart/TensorFold/blob/main/RUNBOOK.md)
- [API fields](https://github.com/ashhart/TensorFold/blob/main/docs/api.md)
- [Recipes 与 measurements](https://github.com/ashhart/TensorFold/tree/main/docs/recipes)
- [Quantization scope](https://github.com/ashhart/TensorFold/blob/main/docs/quantization.md)
- [Third-party notices](https://github.com/ashhart/TensorFold/blob/main/THIRD_PARTY_NOTICES.md)
- [LICENSE](https://github.com/ashhart/TensorFold/blob/main/LICENSE)
