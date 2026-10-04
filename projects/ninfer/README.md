<!-- markdownlint-disable MD013 -->

# NInfer（Neroued/ninfer）

> 上游仓库：<https://github.com/Neroued/ninfer> · 归类：模型、训练与推理基础设施 · 本页基于 2026-10-05 的 GitHub API、README、performance methodology、serving / conversion 文档、model card、CMake 与 LICENSE 静态整理，未使用 RTX 5090 / CUDA 13.1、下载 `.ninfer` 权重、编译或复测吞吐与能力分数。

- 抓取快照：2,694 stars、536 forks、129 open issues。
- 热度信号：GitHub C++ Trending 抓取时约 +42 当日 stars。
- 版本与许可：代码 Apache-2.0；无 GitHub Release / tag，当前 runtime 只接受 v3 `.ninfer` artifact；官方权重在 Hugging Face 独立发布。

## 定位

NInfer 是从头实现的 C++ / CUDA 单卡推理引擎，为一张 GeForce RTX 5090 上的少数 Qwen3.6 / Qwen3.8 Dense 与 MoE checkpoint 做窄优化。它提供本地 CLI、OpenAI / Anthropic compatible HTTP API、图像 / 视频输入、长上下文、prefix reuse 与 1--8 条固定 execution lanes。

## 用法

环境要求 64-bit Linux、RTX 5090、支持 `sm_120a` 的 CUDA toolkit、CMake 3.28、C++20、Ninja、FFmpeg dev 和 libcurl。源码构建后，从 Hugging Face 下载官方 v3 `.ninfer` artifact，用 `ninfer-serve` 启动 server 或 `ninfer` 单次推理；context、KV capacity / dtype、concurrency、vision 与 speculative decoding 都需在启动时显式配置。

## 原理

artifact 将模型配置、编码权重、逻辑 binding 与 frontend resource 打包，runtime 用专用 CUDA kernels、CUDA Graph、量化 KV、MTP / DFlash speculative decoding 和固定显存 residency 执行。共享 KV / StateImage 池支持 prefix retention、host snapshot、pressure pause / resume；server 负责兼容协议和 usage accounting，但解析出的 tool call 只返回客户端，不由 NInfer 执行。

## 价值

它用极窄的硬件 / 模型边界换取可深入优化的单卡吞吐，并把 benchmark workload、时间口径、模型制品来源和长上下文资源调度写得较细。对 RTX 5090 的固定研究平台，这比宣称“通用支持”更容易定位 kernel、KV、concurrency 与质量之间的真实取舍。

## 风险边界

- 只支持 `sm_120a` RTX 5090、单 GPU、单 resident model；不支持多卡、offload、priority / QoS，不能把结果外推到其他 Blackwell、数据中心卡或通用部署。
- README throughput 与 EvalScope 分数来自作者固定硬件和配置，其中能力评测为 0-shot、规则评分、每题一个 sample；本轮未独立复现，吞吐也不证明答案质量。
- 代码 Apache-2.0 与 Hugging Face artifact、Qwen 原权重、二次量化来源是不同制品链；必须固定 model revision、artifact hash、conversion recipe 和对应 model card。
- 无 Release / tag 和安装包，意味着浮动源码 / artifact schema 可能变化；v2 到 v3 upgrade 工具也需保留原件与转换日志。
- 示例 Docker 将服务发布到 `0.0.0.0:8080`；OpenAI / Anthropic compatibility 不自动提供认证、TLS、rate limit 或多租户隔离。
- prefix / response state、prompt、image / video 与 metrics 可能含敏感数据；解析 tool call 不执行虽缩小副作用，但调用方仍需自己授权工具。

## 补充建议

固定当前 commit `abb7f14f8145`、CUDA / driver、一个 v3 artifact 和 SHA-256；先跑单请求 correctness / perplexity，再按上游 methodology 复测 TTFT、prefill、decode、makespan、显存与失败率。server 仅绑定 loopback 或置于带认证 TLS 的 gateway 后，关闭不需要的 response state / logs，并用自己的金标测量量化和 speculative decoding 对质量的影响。

## 参考资料

- [GitHub 仓库](https://github.com/Neroued/ninfer)
- [GitHub REST API](https://api.github.com/repos/Neroued/ninfer)
- [README、性能与能力表](https://github.com/Neroued/ninfer/blob/master/README.md)
- [Performance methodology](https://github.com/Neroued/ninfer/blob/master/docs/performance/methodology.md)
- [Serving 文档](https://github.com/Neroued/ninfer/blob/master/docs/serving.md)
- [权重转换与 v2→v3](https://github.com/Neroued/ninfer/blob/master/docs/weight-conversion.md)
- [CMake 硬件边界](https://github.com/Neroued/ninfer/blob/master/CMakeLists.txt)
- [Qwen3.8 NVFP4 model card](https://github.com/Neroued/ninfer/blob/master/model-cards/Qwen3.8-27B-nvfp4-NInfer/README.md)
- [LICENSE](https://github.com/Neroued/ninfer/blob/master/LICENSE)
