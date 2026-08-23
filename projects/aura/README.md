<!-- markdownlint-disable MD013 -->

# aura

> 上游仓库：[Grevix/aura](https://github.com/Grevix/aura) · 归类：模型、训练与推理基础设施 · 本页基于 2026-08-24 的上游 README、仓库目录与 GitHub API 快照整理。

## 定位

`aura`（Adaptive Ultra-Low-Memory Runtime for AI）是面向低内存消费级设备的本地 LLM 推理编排器。它不实现新的模型内核，而是在 Ollama、GGUF 与 `llama.cpp` 外围，根据可用内存、上下文长度和量化等级生成执行计划，并尝试用操作系统级机制限制推理进程的内存预算。

API 快照：3 stars、0 forks、0 个开放 issue；创建于 2026-08-23；Apache-2.0。它只是非常早期的公开开发者信号，不是 GitHub Trending 排名，也不能证明 README 中的跨平台、性能或内存上限主张。

## 用法

先在非关键主机、已安装 Rust 1.80+ 与本地模型 runtime 的环境中构建，再把 `plan` 的结果与系统监控对照：

```sh
git clone https://github.com/Grevix/aura.git
cd aura
cargo build --release

./target/release/aura doctor
./target/release/aura plan --model llama3.2:3b --memory 4G
./target/release/aura run --model llama3.2:3b --memory 4G --prompt "Explain quantum computing."
cargo test --workspace
```

上游还提供 `benchmark` 与 `audit` 子命令；应将其 JSON 输出、实际 RSS/峰值内存、吞吐、上下文长度和模型版本一并保存，不能只采信项目自报结果。

## 原理

- 硬件探测器读取 CPU/SIMD、RAM、页大小、存储与 GPU 状态；规划器在给定预算下尝试缩减上下文并选择可容纳的量化方案。
- 运行层解析 Ollama manifest 或 GGUF 路径，随后调用 `llama.cpp` 后端；因此生成质量由底层模型与量化决定，不会因 `aura` 本身提高模型智能。
- README 描述 Windows Job Object、Linux cgroup v2 `MemoryMax` 与 macOS RSS 监控等平台机制。它们的语义不同：commit 限制、cgroup 限制与采样式监控不能视为同等强度的硬隔离。

## 价值

- 将“这个模型能否在这台机器、这个上下文和预算下运行”变成可先验规划、可记录的工程问题，减少盲目加载后系统 swap 或 OOM 的试错。
- 对本地模型实验可同时输出硬件探测、执行计划与基准工件，便于比较量化、上下文和成本之间的取舍。
- 复用 Ollama / GGUF / `llama.cpp` 生态，而非要求迁移现有模型格式或服务接口。

## 风险边界

- README 所列 4 GB 结果是项目作者在特定硬件和模型版本上的自报基准；不同 OS、驱动、内存压力、并发和 mmap 行为都可能改变峰值内存与稳定性。
- 低量化或缩短上下文会影响任务质量和长文一致性；“能运行”不等于能满足质量、延迟或吞吐要求。
- cgroup、Job Object 与本机命令仍需要足够权限；错误的限制可能杀死推理进程或影响同机服务，不能把它理解为通用安全沙箱。
- 模型、提示词、日志与 Ollama 服务的网络暴露仍需独立治理；本项目不替代供应链、模型许可、隐私或内容安全审查。

## 补充建议

1. 先在固定模型、固定 prompt 集和空闲/受压两类机器状态下运行 `plan`，将预测值与真实峰值 RSS、延迟和输出质量并列记录。
2. Linux 上确认实际创建的 cgroup、控制器启用状态和清理路径；macOS 上尤其不要将 RSS 监控当作不可突破的内存硬界。
3. 把模型文件的版本、量化、context、Ollama/llama.cpp revision 与基准 JSON 纳入实验元数据；升级任何一项后重测。
4. 先以只读测试和小预算运行，确认失败时会安全退出且不会中断共享开发机上的其他重要进程。

## 参考资料

- [上游 README / 架构、命令与基准口径](https://github.com/Grevix/aura)
- [GitHub API 元数据](https://api.github.com/repos/Grevix/aura)
- [上游许可证](https://github.com/Grevix/aura/blob/main/LICENSE)
- [llama.cpp](https://github.com/ggml-org/llama.cpp)
- [Ollama 文档](https://docs.ollama.com/)
