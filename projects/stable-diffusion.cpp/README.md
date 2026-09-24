<!-- markdownlint-disable MD013 -->

# stable-diffusion.cpp（leejet/stable-diffusion.cpp）

- GitHub：<https://github.com/leejet/stable-diffusion.cpp>
- 抓取快照：2026-09-25，7,233 stars、811 forks、270 open issues
- 热度信号：GitHub 综合 / C++ Trending 抓取时约 +69 当日 stars
- 版本与许可：MIT；latest GitHub Release 为滚动构建 `master-913-b167b94`（2026-09-24）

## 定位

stable-diffusion.cpp 是基于 ggml 的纯 C / C++ diffusion inference runtime，目标类似 llama.cpp：用轻量本地二进制在 CPU、CUDA、Vulkan、Metal、OpenCL、SYCL 等 backend 上运行图像 / 视频生成与编辑模型。当前上游列出 Stable Diffusion、FLUX、Qwen Image、Wan、LTX 等多条模型路径。

## 用法

用户可从 Releases 下载预编译 binary，或按 CMake build guide 为目标 backend 编译；下载有权使用的 `.ckpt`、`.safetensors` 或 `.gguf` 权重后，以 `sd-cli` 指定模型和 prompt 生成图像，也可使用 `sd-server`、embedded Web UI、Docker、RPC 或社区语言 binding。仓库还提供量化、backend placement、caching、LoRA 和 troubleshooting 指南。

## 原理

项目用 ggml tensor / graph 把 diffusion、VAE、text encoder、sampler 与多类 attention / cache 优化落到统一 C++ runtime；模型转换可生成 GGUF 或 safetensors，backend 负责 CPU / GPU kernel 和内存放置。量化、Flash Attention、VAE tiling、TAESD、cache 与分层 offload 在显存、速度和质量之间提供可组合取舍。

## 价值

它让没有完整 Python / PyTorch 环境的桌面、服务器和部分移动设备也能运行多类图像 / 视频模型，并通过同一 CLI / library 接口覆盖不同 GPU vendor。对端侧、离线、嵌入式和跨平台产品，单二进制与 GGUF 生态可明显降低部署复杂度。

## 风险边界

- README 明确项目处于活跃开发、API 与 CLI 可能频繁变化；滚动 `master-*` release 不等于稳定语义版本，应用需固定 commit / artifact hash。
- “支持某模型”不证明所有分辨率、LoRA、ControlNet、量化和 backend 都与原始 pipeline 数值 / 画质等价；本轮未做图像或视频回归。
- MIT 只覆盖 runtime 源码；Stable Diffusion、FLUX、Qwen、Wan、LTX 等权重、训练数据、输出用途和社区 wrapper 各自有许可 / 政策。
- 不同 backend、RNG、量化和 kernel 会改变速度、显存与输出；跨平台可复现选项仍要在目标硬件上验证。
- 生成内容可能涉及人物肖像、商标、版权、隐私与不安全内容；本地运行不会自动提供来源证明、过滤或发布授权。

## 补充建议

选择一个权利清晰的模型和固定 prompt / seed / image fixture，记录 commit、compiler、backend、driver、量化格式与模型 hash；对 CPU、CUDA / Metal / Vulkan 做图像差分、失败样例、峰值内存和延迟对照。产品接入应单独实现内容政策、来源记录、输出审阅与版本回滚，而不是依赖 runtime 名称推断合规。

## 参考资料

- [GitHub 仓库](https://github.com/leejet/stable-diffusion.cpp)
- [GitHub REST API](https://api.github.com/repos/leejet/stable-diffusion.cpp)
- [最新滚动 Release](https://github.com/leejet/stable-diffusion.cpp/releases/tag/master-913-b167b94)
- [构建指南](https://github.com/leejet/stable-diffusion.cpp/blob/master/docs/build.md)
- [性能指南](https://github.com/leejet/stable-diffusion.cpp/blob/master/docs/performance.md)
- [backend 选择](https://github.com/leejet/stable-diffusion.cpp/blob/master/docs/backend.md)
- [量化与 GGUF](https://github.com/leejet/stable-diffusion.cpp/blob/master/docs/quantization_and_gguf.md)
- [LICENSE](https://github.com/leejet/stable-diffusion.cpp/blob/master/LICENSE)
