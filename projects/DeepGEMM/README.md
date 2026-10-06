<!-- markdownlint-disable MD013 -->

# DeepGEMM（deepseek-ai/DeepGEMM）

> 上游仓库：<https://github.com/deepseek-ai/DeepGEMM> · 归类：模型、训练与推理基础设施 · 本页基于 2026-10-07 的 GitHub API、README、源码 manifest、测试与 LICENSE 静态整理，未占用 SM90 / SM100 GPU 编译内核或复测吞吐、延迟和数值误差。

- 抓取快照：8,678 stars、1,371 forks、150 open issues。
- 热度信号：GitHub 综合 Trending 抓取时约 +363 当日 stars；最后 push 为 2026-09-30。
- 版本与许可：MIT；API latest Release 为 `v2.1.1.post3`，首个 tag 为 `v2.1.1`，当前 `deep_gemm/__init__.py` 为 `2.8.1`，存在发行 / tag / manifest 漂移；本页固定审计 commit `057ca5964aae`。

## 定位

DeepGEMM 是 DeepSeek 面向现代大模型计算的 NVIDIA GPU tensor-core kernel 库，覆盖 FP8、FP4、BF16 GEMM、分组 GEMM、MQA scoring、HyperConnection 与融合通信 / 计算的 Mega MoE。它更接近底层算子和性能工程资产，而不是完整模型服务框架。

## 用法

上游要求 NVIDIA SM90 或 SM100、Python 3.8+、支持 C++20 `<format>` 的编译环境、CUDA Toolkit 12.9+、PyTorch 2.3+ 与 CUTLASS 4.0+。应递归拉取 submodule，在固定 commit 的隔离构建环境执行 `develop.sh` 或 `install.sh`，再从 `tests/` 选择与目标 shape、dtype、layout、GPU 和 PyTorch 版本一致的正确性与 benchmark 用例。

## 原理

Python extension 暴露密集 / 分组矩阵乘、attention indexer 与 Mega MoE 接口；DeepJIT 在运行期按 shape 和配置生成、编译并缓存 CUDA kernel。SM90 与 SM100 的 layout、scale 格式和支持范围不同，例如前者的缩放因子为 FP32，后者使用打包 UE8M0；Mega MoE 还利用 symmetric memory，把 dispatch、两层线性、SwiGLU、通信与 combine 重叠。

## 价值

项目把 DeepSeek 生产型模型中的关键 kernel 收到相对集中、可读的 CUDA 代码与测试中，对学习 FP8 / FP4、TMA、MoE 通信重叠和 JIT 选型有直接价值。对匹配硬件和固定 workload，它也可能减少通用库在特殊 shape 上的调度与融合开销。

## 风险边界

- 只支持特定 NVIDIA 架构与较新的 CUDA / 编译栈；AMD、Apple Silicon、旧卡和不同 ABI 不能据此推断兼容或加速。
- 上游“匹配或超过专家调优库”和 H800 峰值 1,550 TFLOPS 是作者结果，本轮未在固定功耗、shape、warmup、精度与基线版本下复测。
- FP8 / FP4 缩放、layout、对齐、mask 和 fused communication 的错误可能静默影响数值；吞吐通过不等于模型质量或训练收敛通过。
- DeepJIT 会在运行时编译并写缓存，submodule 与编译器也是供应链；生产环境需固定源码、依赖、编译参数和缓存权限。
- API latest Release、tag 与源码 `2.8.1` 不一致，不能只按 GitHub “Latest” 或浮动 `main` 判断可复现版本。
- MIT 仅覆盖本仓库代码，不自动覆盖 CUTLASS、PyTorch、驱动、模型权重、训练数据或使用它生成的模型制品。

## 补充建议

为目标 GPU 建立 shape × dtype × layout 的小型回归矩阵，同时记录准确率 / 最大误差、吞吐、延迟分位数、显存、JIT 首次开销与缓存命中；先同 cuBLASLt / CUTLASS 在相同输入上做差分，再进入端到端模型。部署时固定 commit、submodule SHA、CUDA / driver / PyTorch 与编译器，并把 `DG_JIT_CACHE_DIR` 放到受控、可清理的目录。

## 参考资料

- [GitHub 仓库](https://github.com/deepseek-ai/DeepGEMM)
- [GitHub REST API](https://api.github.com/repos/deepseek-ai/DeepGEMM)
- [README 与接口](https://github.com/deepseek-ai/DeepGEMM/blob/main/README.md)
- [Python manifest](https://github.com/deepseek-ai/DeepGEMM/blob/main/deep_gemm/__init__.py)
- [构建脚本](https://github.com/deepseek-ai/DeepGEMM/blob/main/setup.py)
- [测试目录](https://github.com/deepseek-ai/DeepGEMM/tree/main/tests)
- [MIT License](https://github.com/deepseek-ai/DeepGEMM/blob/main/LICENSE)
- [Mega MoE benchmark PR](https://github.com/deepseek-ai/DeepGEMM/pull/316)
