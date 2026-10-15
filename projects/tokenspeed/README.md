<!-- markdownlint-disable MD013 -->

# TokenSpeed（lightseekorg/tokenspeed）中文解读

> 上游仓库：<https://github.com/lightseekorg/tokenspeed> · 归类：模型、训练与推理基础设施 · 证据快照：2026-10-16（Asia/Shanghai）。API：2,464 stars / 336 forks / 90 open issues；MIT；Release / Python manifest `v0.1.1` / `0.1.1`。本页为上游文档与相关源码的静态整理，未安装运行、接入真实数据 / 凭据、复测性能或完成全面安全审计。

## 定位

TokenSpeed 是 LightSeek 的 LLM 推理引擎，面向 Agent 常见的长上下文、工具调用与交互式解码负载。核心设计是 C++ 调度控制面、Python 执行面和可插拔 GPU kernels；适合研究调度、KV cache 和硬件优化如何共同影响服务延迟。上游“speed-of-light”“TensorRT-LLM-level performance”属于项目定位与作者性能声明。

## 用法

先按官方 Getting Started 匹配 GPU、驱动、CUDA / ROCm 与 Python 版本，再在独立环境固定 runtime 和 kernel 制品；运行 `tokenspeed env`、`tokenspeed serve --help` 核对实际安装。最小服务示例是 `tokenspeed serve openai/gpt-oss-20b --host 127.0.0.1 --port 8000 --tensor-parallel-size 1`，模型能否装入显存需另算。API 兼容 OpenAI 风格，首次只接本地合成请求。

## 原理

- Scheduler 用有限状态机表达请求生命周期、KV cache 所有权与执行重叠时机；上游强调用 C++ 类型系统在编译阶段约束部分资源状态。
- Python 层负责模型与执行集成，kernel registry 按后端选择 attention / MoE 等实现，使算法开发与低层优化分开。
- AsyncLLM 入口与 SMG 集成，降低 CPU 请求处理开销；并行方式、量化、parser 与 cache 参数共同决定部署行为。

## 价值

- 提供研究调度正确性与性能折中的明确结构，便于把单个 kernel 优化放回完整 serving workload。
- 同时保留 Python 扩展入口和专用 kernel，适合对照 vLLM / TensorRT-LLM 做固定条件的工程评估。
- 文档区分 CUDA、ROCm、Hopper 和特定 AMD 架构路径，有助于避免把一个设备上的结论泛化到全部 GPU。

## 风险边界

- 官方 runner 示例含 `--privileged`、host network / IPC / PID、共享缓存目录与浮动 `latest`；它是高权限开发环境，采用前应逐项收敛。
- launching 示例含 `0.0.0.0` 与 `--trust-remote-code`；首次改为 loopback，生产补认证 / TLS / 限流，模型远端代码先审阅。
- CUDA / ROCm nightly kernel 同版本号可能对应不同依赖；官方明确不要混用两个 extra index，且 nightly 可被重建替换，版本号本身不足以复现。
- README 的 tokens/s 和 Pareto 曲线与模型、量化、GPU、并发和输入输出长度绑定；本页未独立复测，编译期资源约束也不等于整个服务无漏洞。

## 补充建议

- 用同一模型 revision、精度、硬件和请求分布比较 TTFT、TPOT、吞吐、显存与答案质量，分别报告低并发和饱和区间。
- 记录 wheel SHA、镜像 digest、kernel 版本、驱动与完整启动参数；先做取消、OOM、超长输入和 parser 失败测试。
- 不把宿主私有缓存或凭据直接挂入特权 runner；模型权重和第三方 kernel 的许可另行核对。

## 参考资料

- 上游仓库：<https://github.com/lightseekorg/tokenspeed>
- GitHub REST API：<https://api.github.com/repos/lightseekorg/tokenspeed>
- README：<https://github.com/lightseekorg/tokenspeed/blob/main/README.md>
- 开始使用：<https://github.com/lightseekorg/tokenspeed/blob/main/docs/guides/getting-started.md>
- 启动服务：<https://github.com/lightseekorg/tokenspeed/blob/main/docs/guides/launching.md>
- Python manifest：<https://github.com/lightseekorg/tokenspeed/blob/main/python/pyproject.toml>
- 安全报告入口：<https://github.com/lightseekorg/tokenspeed/blob/main/SECURITY.md>
- LICENSE：<https://github.com/lightseekorg/tokenspeed/blob/main/LICENSE>
- Releases：<https://github.com/lightseekorg/tokenspeed/releases>
