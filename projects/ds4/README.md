<!-- markdownlint-disable MD013 -->

# DwarfStar / ds4（antirez/ds4）

> 上游仓库：<https://github.com/antirez/ds4> · 归类：模型、训练与推理基础设施 · 本页基于 2026-10-05 的 GitHub API、README、模型 / 性能 / 测试 / server 文档、MODEL_CARD 与 LICENSE 静态整理，未下载百 GB 级 GGUF、编译 Metal / CUDA / ROCm、运行模型或复测性能与质量。

- 抓取快照：23,429 stars、2,251 forks、756 open issues。
- 热度信号：GitHub 综合 Trending 抓取时约 +211 当日 stars。
- 版本与许可：代码 MIT；无 GitHub Release / tag，模型由项目脚本从独立制品源下载并有各自来源与许可。

## 定位

DwarfStar 是为少数大型开放权重模型定向优化的原生推理引擎，而非通用 GGUF runner。当前重点覆盖 DeepSeek V4 / V4.1 Flash、部分 PRO、GLM 5.2 / 5.3、Qwen3.8 Flash Next，并针对 Apple Metal、NVIDIA CUDA 与 Strix Halo ROCm 实现 SSD streaming、tensor / pipeline parallel、server 和本地 coding agent。

## 用法

克隆仓库后按硬件使用 `make`、`make cuda-spark`、`make cuda-generic` 或 `make strix-halo`。例如 `./download_model.sh ds4f-q2` 下载模型，`./ds4` 提供交互 CLI，`./ds4-server --ctx 32768` 提供 loopback HTTP 服务，`./ds4-agent` 直接运行带工具格式的本地 coding agent；Pi、OpenCode、Codex CLI 与 Claude Code 可接 server。

## 原理

项目以 C、Metal / CUDA / ROCm kernels 和专用 GGUF 转换工具实现窄模型路径，并针对 routed experts、量化 KV、SSD 读取、MTP speculative decoding 与多设备并行优化。会话可把 token、KV 状态和 trace 保存到 `~/.ds4/kvcache`，server 支持多 session；内置 eval 主要是 DwarfStar 集成回归，不是官方模型排行榜。

## 价值

它把前沿大模型在 96--512 GB 个人设备或多卡工作站上的“能跑、怎么量化、怎么测、怎么服务”收拢到一套窄而透明的工程实现。对于愿意固定模型和硬件的研究者，源码、转换脚本、性能记录和数值测试比只提供封装 API 更便于定位瓶颈。

## 风险边界

- README 明确项目快速变化、beta 质量且模型支持是 opportunistic；无 Release / tag 意味着采用时必须固定 commit，不能依赖浮动 `main` 或默认模型链接。
- 作者的 M5 Max、DGX Spark、L40S、RDMA 与 Strix Halo 性能是特定模型、量化、上下文和硬件记录，本轮未复现；SSD streaming 的吞吐、磨损和内存余量也因设备而异。
- 代码 MIT 不自动覆盖 DeepSeek、GLM、Qwen 权重、转换产物、评测数据或输出用途；下载前须逐制品核对 model card、上游许可和校验值。
- `ds4-agent` 能读文件并调用工具，保存的会话、KV snapshot 和 trace 可能含私有代码 / 提示；本地运行不等于最小权限或自动脱敏。
- 多机 RDMA、server 暴露和多用户并发会引入网络、认证、资源争用与数据隔离问题；README 的默认 loopback 不能替代部署侧访问控制。
- 仓库声明大量代码由 AI coding agents 强辅助开发；集成测试和 QA 记录仍不能替代特定硬件上的数值、回归与安全验收。

## 补充建议

固定当前 commit `0aaea5a238fb`、模型 revision、GGUF 哈希、编译器与驱动，只下载一个明确许可的量化制品；先运行数值 / sampling / eval 回归，再在自有 prompt 上记录 TTFT、tok/s、内存、温度、功耗与质量。server 保持 loopback，Agent 用专用低权限用户；跨机 / RDMA 仅在隔离网络中验证。

## 参考资料

- [GitHub 仓库](https://github.com/antirez/ds4)
- [GitHub REST API](https://api.github.com/repos/antirez/ds4)
- [README 与使用入口](https://github.com/antirez/ds4/blob/main/README.md)
- [模型与内存要求](https://github.com/antirez/ds4/blob/main/docs/MODELS.md)
- [性能与测量说明](https://github.com/antirez/ds4/blob/main/docs/PERFORMANCE.md)
- [测试说明](https://github.com/antirez/ds4/blob/main/docs/TESTING.md)
- [Server 文档](https://github.com/antirez/ds4/blob/main/docs/SERVER.md)
- [MODEL_CARD](https://github.com/antirez/ds4/blob/main/MODEL_CARD.md)
- [LICENSE](https://github.com/antirez/ds4/blob/main/LICENSE)
