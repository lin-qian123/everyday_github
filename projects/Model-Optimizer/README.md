<!-- markdownlint-disable MD013 -->

# NVIDIA Model Optimizer（NVIDIA/Model-Optimizer）

- GitHub：<https://github.com/NVIDIA/Model-Optimizer>
- 抓取快照：2026-09-25，4,052 stars、628 forks、417 open issues
- 热度信号：GitHub 综合 / Python Trending 抓取时约 +22 当日 stars
- 版本与许可：Apache-2.0；latest GitHub Release 为 `0.47.0`，tags 已出现 `0.48.0dev`

## 定位

NVIDIA Model Optimizer（ModelOpt）是模型压缩与部署优化工具库，覆盖 post-training quantization、quantization-aware training、distillation、pruning、sparsity、speculative decoding 和 ONNX export。它面向 LLM、VLM、diffusion 与视觉模型，并衔接 TensorRT-LLM、TensorRT、vLLM、SGLang、Megatron Bridge 和 Hugging Face 生态。

## 用法

稳定版可安装 `nvidia-modelopt[all]`，开发者也可从源码 editable install，或使用预装在 NVIDIA PyTorch / NeMo / TensorRT-LLM container 的版本。典型流程是加载模型与校准集，选择量化 / 剪枝 / 蒸馏 recipe，评估精度，再导出到目标 runtime；仓库还提供不同模型族、backend 和 Windows 的示例 / support matrix。

## 原理

量化路径把权重 / activation 映射到 FP8、INT8、INT4 等更低精度表示，并可通过校准或 QAT 恢复质量；剪枝 / sparsity 删除低贡献参数，distillation 用 teacher 约束较小 student，speculative decoding 训练 draft module 预测额外 token。ModelOpt 保存转换状态并将产物导出到具体 deployment backend，实际收益由硬件 kernel、模型结构和 runtime 共同决定。

## 价值

它把多种压缩技术、模型适配和 NVIDIA 推理栈连接在一个公开仓库中，便于从训练后处理到部署做一致实验。对需要在 GPU 成本、吞吐、延迟、显存和质量之间取舍的团队，统一 recipe 与 export 路径能减少各模型单独拼装脚本的维护成本。

## 风险边界

- 上游的 2×--4× 压缩、加速和精度保持是技术 / 示例口径，不是所有模型、校准集、GPU 与 workload 的保证；本轮未复跑 benchmark。
- 量化、剪枝、蒸馏和 speculative decoding 都可能产生任务相关质量退化；只看 perplexity 或少量通用 benchmark 不能替代私有任务金标和长尾安全测试。
- 安装 `[all]`、container、checkpoint 与 export runtime 会引入多类第三方软件 / 模型许可证；Apache-2.0 根许可不覆盖所有依赖和权重。
- tags 已出现 `0.48.0dev`，而稳定 Release 是 `0.47.0`；上游说明 0.x 阶段 deprecation 迁移期可短至约一个 release / 一个月，升级需要回归。
- 预量化 checkpoint、kernel 和 TensorRT / CUDA 版本高度耦合；“成功导出”不证明目标设备上的数值一致性、吞吐或故障恢复。

## 补充建议

对每个目标模型固定原始权重 hash、校准数据、ModelOpt / CUDA / driver / runtime 与 GPU SKU，记录质量金标、P50 / P95 latency、throughput、显存、能耗和 cold-start。先跑单一技术与未优化 baseline，再测试组合 recipe；任何升级都重做 export compatibility 和少数关键层的数值差分。

## 参考资料

- [GitHub 仓库](https://github.com/NVIDIA/Model-Optimizer)
- [GitHub REST API](https://api.github.com/repos/NVIDIA/Model-Optimizer)
- [0.47.0 Release](https://github.com/NVIDIA/Model-Optimizer/releases/tag/0.47.0)
- [官方文档](https://nvidia.github.io/Model-Optimizer/)
- [安装说明](https://nvidia.github.io/Model-Optimizer/getting_started/2_installation.html)
- [支持矩阵与示例](https://github.com/NVIDIA/Model-Optimizer/tree/main/examples)
- [CHANGELOG](https://github.com/NVIDIA/Model-Optimizer/blob/main/CHANGELOG.rst)
- [LICENSE](https://github.com/NVIDIA/Model-Optimizer/blob/main/LICENSE)
