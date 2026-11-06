<!-- markdownlint-disable MD013 -->

# TensorRT-LLM（NVIDIA 推理框架）

- 更新：2026-11-07（Asia/Shanghai）；官方 Python daily +10，为读取快照，不是自然日结算。
- GitHub API：15,030 stars / 2,913 forks / 1,972 open issues（含 PR）；仓库 ID `679366051`。
- 核读基线：`875c4c9f97130222a07704b09e43a8ddb81a9c2c`；仅文档与抽样实现核验，未安装运行或独立评测。

## 定位

TensorRT-LLM 面向 NVIDIA GPU 的 LLM 与视觉生成推理，结合专用 kernel、PyTorch 原生模型、请求调度、KV cache 和多卡 / 多节点执行。它不是模型权重库，也不等同于只把图编译成静态 TensorRT engine 的旧教程路径。[README](https://github.com/NVIDIA/TensorRT-LLM/blob/875c4c9f97130222a07704b09e43a8ddb81a9c2c/README.md)

## 用法

本轮读取的最新发行是 [v1.4.0rc3](https://github.com/NVIDIA/TensorRT-LLM/releases/tag/v1.4.0rc3)（UTC 2026-11-06 21:38），明确是预发行；固定 main 的 version.py 已为 `1.4.0rc4`，不能将主线标识写成已发布稳定包。

安装文档优先推荐匹配版本的 NGC release container；Linux wheel 路径测试系统为 Ubuntu 24.04，当前主线文档涉及 CUDA 13.4、PyTorch 2.14，NGC PyTorch 与公开 PyPI wheel 的构建也不同。不要将这些主线依赖直接套入旧发行。先核镜像可用 tag / digest、驱动、GPU、模型与量化支持，再在容器内按 quickstart 运行：

```bash
trtllm-serve "TinyLlama/TinyLlama-1.1B-Chat-v1.0" --no-telemetry
```

这是官方示例加文档支持的 telemetry 退出选项，未在本机执行。服务提供 /v1/chat/completions；对外映射端口之前须另设认证与访问限制。也可用 Python `LLM.generate()` 离线调用。[安装](https://github.com/NVIDIA/TensorRT-LLM/blob/875c4c9f97130222a07704b09e43a8ddb81a9c2c/docs/source/installation/installation-guide.md)、[Quickstart](https://github.com/NVIDIA/TensorRT-LLM/blob/875c4c9f97130222a07704b09e43a8ddb81a9c2c/docs/source/quick-start-guide.md)

## 原理

LLM 入口负责 tokenization 和执行器管理，各 rank 的 PyExecutor 循环接请求；Scheduler 选择批次，KVCacheManager 管理注意力缓存，ModelEngine 前向计算，Sampler 采样并输出 token。CUDA Graph 降低 launch 开销，overlap scheduler 叠加 CPU / GPU 工作；量化、推测解码和并行策略针对不同资源瓶颈。[架构](https://github.com/NVIDIA/TensorRT-LLM/blob/875c4c9f97130222a07704b09e43a8ddb81a9c2c/docs/source/developer-guide/overview.md)

吞吐、TTFT、单请求 token 延迟和尾延迟是不同指标，必须固定输入 / 输出长度、并发、量化、硬件与服务目标再比较。README 历史宣传数据不代表所有模型和 GPU。

## 价值

适合有 NVIDIA GPU 部署需求、愿意验证模型 / kernel / 量化组合的团队，也适合把在线服务、离线评估和集群编排分开研究。当前硬件页列 Blackwell、Hopper、Ada 部分型号和 A100；不意味着所有这些卡都支持所有模型与精度路径。[硬件页](https://github.com/NVIDIA/TensorRT-LLM/blob/875c4c9f97130222a07704b09e43a8ddb81a9c2c/docs/source/supported-hardware.md)

## 风险边界

- rc3 明列 DSA 模型使用 NVFP4 KV cache 可能输出错误、部分 GB300 warmup / RPC worker 复用可能挂起，以及大 MoE 后复用 worker 初始化可能 OOM；精度正确性必须先于吞吐优化验收。
- rc2 的 wheel 实为 `1.4.0rc2.post1`，而镜像 / 文档保持 rc2；版本号不能只靠名字猜测一一对应。
- 主线 README 说明默认收集使用 telemetry，支持 `TRTLLM_NO_USAGE_STATS=1`、`DO_NOT_TRACK=1`、`TELEMETRY_DISABLED=true`、配置文件或 CLI 关闭。匿名和字段限制是上游声明，本轮未抓包验证。
- 根 LICENSE 主体 Apache-2.0，另列第三方条件；LTX-2 Community License 特别只适用于 `tensorrt_llm/_torch/visual_gen/models/ltx2/`。不能把 API 的 NOASSERTION 或 README Apache badge 当整仓统一授权结论。
- 未拉取镜像 / 权重、申请 GPU、启动服务或复现已知故障；这些是固定文档事实和待验证风险。

## 补充建议

固定源码、镜像 digest、模型 revision / hash 和运行参数，以小金标集先验准确率，再测 TTFT、TPOT、吞吐、p95 / p99、显存、取消请求和 worker 重启。将多卡 / MPI / 网络拓扑、cache dtype 与服务参数入账；遇到 rc3 已知组合先选择文档支持的替代路径并保留回滚版本。

## 参考资料

- [仓库](https://github.com/NVIDIA/TensorRT-LLM)、[rc3 已知问题](https://github.com/NVIDIA/TensorRT-LLM/releases/tag/v1.4.0rc3)、[rc2 wheel 差异](https://github.com/NVIDIA/TensorRT-LLM/releases/tag/v1.4.0rc2)。
- [README 与 telemetry](https://github.com/NVIDIA/TensorRT-LLM/blob/875c4c9f97130222a07704b09e43a8ddb81a9c2c/README.md)、[主线版本](https://github.com/NVIDIA/TensorRT-LLM/blob/875c4c9f97130222a07704b09e43a8ddb81a9c2c/tensorrt_llm/version.py)、[分组件许可](https://github.com/NVIDIA/TensorRT-LLM/blob/875c4c9f97130222a07704b09e43a8ddb81a9c2c/LICENSE)。
- [Quickstart](https://github.com/NVIDIA/TensorRT-LLM/blob/875c4c9f97130222a07704b09e43a8ddb81a9c2c/docs/source/quick-start-guide.md)、[安装](https://github.com/NVIDIA/TensorRT-LLM/blob/875c4c9f97130222a07704b09e43a8ddb81a9c2c/docs/source/installation/installation-guide.md)、[硬件](https://github.com/NVIDIA/TensorRT-LLM/blob/875c4c9f97130222a07704b09e43a8ddb81a9c2c/docs/source/supported-hardware.md)、[架构](https://github.com/NVIDIA/TensorRT-LLM/blob/875c4c9f97130222a07704b09e43a8ddb81a9c2c/docs/source/developer-guide/overview.md)。
