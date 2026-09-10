<!-- markdownlint-disable MD013 -->

# colibri（JustVugg/colibri）中文解读

> 证据快照：2026-09-11（Asia/Shanghai）。GitHub REST API 显示 27,434 stars、3,005 forks、114 open issues，Apache-2.0；最新 release 为 `v1.10.2`。本文未下载数百 GB / TB 级模型，也未在 CPU、Metal、CUDA 或多 GPU 环境复现上游 benchmark。

## 定位

colibri 是用纯 C runtime 探索超大 Mixture-of-Experts（MoE）模型本地推理的引擎。它把 VRAM、RAM 与 NVMe 视为统一层级，只让 dense 部分常驻快速内存，并按 router 结果从磁盘加载需要的 experts，使 744B 到 2.8T 参数的稀疏模型能在远低于完整权重常驻要求的机器上运行。

它解决的是“能否加载与以多慢的速度运行”这一 inference systems 问题，不等于消费级机器能获得数据中心相同吞吐、并发、长上下文或服务可靠性。

## 用法

上游提供 Linux、macOS 和 Windows 预编译 release，也可源码构建。以参考 GLM-5.2 int4 容器为例，权重约 372 GB：

```bash
COLI_MODEL=/nvme/glm52_i4 ./coli doctor --deep
COLI_MODEL=/nvme/glm52_i4 ./coli plan
COLI_MODEL=/nvme/glm52_i4 ./coli chat
./coli serve --model /nvme/glm52_i4
```

`coli` launcher 和转换/API helper 使用 Python，token loop runtime 为 C。不同模型的磁盘、RAM、precision 与 backend 约束不同；不能把 GLM-5.2、Kimi K3、DeepSeek V4 Flash、Qwen 或 OLMoE 的要求混用。

## 原理

- dense attention、shared experts、embedding 等常驻 RAM/VRAM；routed experts 保存在磁盘并按 token/layer 读取。
- per-layer LRU、历史热度 pinning、one-layer lookahead prefetch 与 batched expert union 尝试减少重复 I/O。
- 可选 CUDA、Metal、Vulkan、NUMA 与多 SSD；不同 tier 的放置只应改变速度，不应静默改变 router semantics 或精度。
- safetensors 转换、int4/int8 state、MTP speculative decoding 和 recurrent-state checkpoint 分别降低权重、KV 或重复 prefill 成本。
- 上游以 transformers oracle、teacher forcing、端到端 benchmark 和 issue 实验记录校验部分语义/性能，但本页只做静态审阅。

## 价值

- 把 MoE sparsity 与存储层级结合，扩展“模型必须全部装进 VRAM”的传统假设。
- 纯 C engine 和显式指标有利于研究 I/O、cache、prefetch、quantization 与 heterogeneous execution。
- 上游强调记录 cold/warm cache、TTFT、tok/s、expert hit、bytes read 和质量，适合作为可复现实验模板。
- 支持从小型 OLMoE 到超大 Kimi K3 的多架构，可用于比较不同 MoE 路由和存储行为。

## 风险边界

- 在磁盘流式运行 372 GB 或 1.6 TB 权重可能只有每秒零点几 token；“能跑”与“可交互/可服务”是不同结论。
- 上游吞吐、TTFT、71.6% lookahead predictability、57× KV 压缩等数字依赖特定模型、硬件、缓存和实现版本，不能外推。
- int4/FP8/MXFP4、MTP 和不同 converted container 会影响质量；token-exact 某条 forward path 不代表所有任务质量等价。
- 权重与 tokenizer/代码许可证各自独立，Apache-2.0 只覆盖本仓库代码；模型下载还涉及存储、带宽和上游使用条款。
- warm history 可能过拟合常见 prompt；多 SSD、cluster、Metal/Vulkan 都需要独立故障与一致性测试。

## 补充建议

1. 先用约 7 GB 的 OLMoE 或较小 Qwen3.6 容器验证格式、doctor、输出和 API，再考虑数百 GB 权重。
2. 固定 commit、model hash、converter、precision、prompt、context、cache state 和硬件，至少重复 cold/warm benchmark。
3. 同时报告 token-level/任务质量、TTFT、decode tok/s、RSS/VRAM、磁盘读量、功耗和失败恢复，不只报峰值。
4. 对多盘与 cluster 做拔盘、worker 丢失、校验失败和中断恢复测试，并保留模型与派生容器许可证清单。

## 参考资料

- GitHub：<https://github.com/JustVugg/colibri>
- GitHub REST API：<https://api.github.com/repos/JustVugg/colibri>
- Releases：<https://github.com/JustVugg/colibri/releases>
- Quick Start：<https://github.com/JustVugg/colibri/blob/main/docs/quickstart.md>
- Benchmark 协议：<https://github.com/JustVugg/colibri/blob/main/docs/benchmarks.md>
- Metal 后端：<https://github.com/JustVugg/colibri/blob/main/docs/metal.md>
- LICENSE：<https://github.com/JustVugg/colibri/blob/main/LICENSE>
