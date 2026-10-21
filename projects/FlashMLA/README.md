<!-- markdownlint-disable MD013 -->

# FlashMLA

> 更新：2026-10-22（Asia/Shanghai）。分类：模型、训练与推理基础设施。主上游 `deepseek-ai/FlashMLA`；默认分支快照 `0f11e178da1f`。官方资料与源码静态研究；热度、发行及社媒口径见[当日日报](../../daily/2026-10-22/ai-hotspots.md)。

## 定位

DeepSeek 的高性能注意力算子库，当前面向 DeepSeek-V4.1 的 token 稀疏 prefill / decode，另有融合 norm / RoPE / attention / cast 算子与稠密 MHA。它是模型服务的底层内核，不是完整模型、推理服务或 KV 缓存管理系统。[README.md](https://github.com/deepseek-ai/FlashMLA/blob/0f11e178da1f67becb087a324b400854931ec3e3/README.md)

## 用法

先核设备与软件栈，再固定 commit、递归拉子模块并按 README 使用 `pip install -v . --no-build-isolation`。构建脚本导入 torch，Ascend 路径还依赖 torch_npu，不能把跳过构建隔离误解为依赖已齐全。[README.md](https://github.com/deepseek-ai/FlashMLA/blob/0f11e178da1f67becb087a324b400854931ec3e3/README.md) [setup.py](https://github.com/deepseek-ai/FlashMLA/blob/0f11e178da1f67becb087a324b400854931ec3e3/setup.py)

当前 NVIDIA 路径要求 SM100 / SM103、CUDA `>=13.1`（推荐 >=13.2）与 PyTorch `>=2.10`；Ascend 路径要求 950、CANN `>=9.2.0`、torch_npu 和兼容 PyTorch。平台可通过 `FLASH_MLA_BUILD_TARGET_PLATFORM` 指定。[README.md](https://github.com/deepseek-ai/FlashMLA/blob/0f11e178da1f67becb087a324b400854931ec3e3/README.md)

调用顺序包括建立 MLA scheduler 元数据，再在 decode 中调用 `flash_mla_with_kvcache`；输入形状、indices、缓存字节布局与旧版不能混用。[flash_mla/flash_mla_interface.py](https://github.com/deepseek-ai/FlashMLA/blob/0f11e178da1f67becb087a324b400854931ec3e3/flash_mla/flash_mla_interface.py) [README.md](https://github.com/deepseek-ai/FlashMLA/blob/0f11e178da1f67becb087a324b400854931ec3e3/README.md)

## 原理

稀疏路径只对给定 token indices 取对应 KV 并计算 attention，减少访存 / 计算；缓存量化和 tile 调度服务于特定硬件。融合路径合并前后小算子以减少启动和中间数据开销；相同 FLOPs 口径也不能直接代表端到端服务吞吐。[README.md](https://github.com/deepseek-ai/FlashMLA/blob/0f11e178da1f67becb087a324b400854931ec3e3/README.md) [flash_mla/flash_mla_interface.py](https://github.com/deepseek-ai/FlashMLA/blob/0f11e178da1f67becb087a324b400854931ec3e3/flash_mla/flash_mla_interface.py)

## 价值

工程判断：对已使用兼容模型 / 硬件、且 attention 是瓶颈的服务有研究价值。应同时测数值误差、延迟分位数、不同 batch / context / top-k 和总服务开销，再决定是否集成。

## 风险边界

- README 的 2026-09-30 破坏性更新明确移除 Hopper 与 V3 / V3.2 / V4.0 支持，并更换 FP8 / FP4 KV 格式；旧平台需切至其指定历史 commit。旧 H800 benchmark 不能代表当前主线能在 H800 构建运行。[README.md](https://github.com/deepseek-ai/FlashMLA/blob/0f11e178da1f67becb087a324b400854931ec3e3/README.md)
- 当前 decode 不支持未量化 bfloat16 KV；FP4 缓存还有具体输入组合限制。indices 的负值 / 越界及空有效集合有特殊行为，需独立覆盖。[README.md](https://github.com/deepseek-ai/FlashMLA/blob/0f11e178da1f67becb087a324b400854931ec3e3/README.md) [flash_mla/flash_mla_interface.py](https://github.com/deepseek-ai/FlashMLA/blob/0f11e178da1f67becb087a324b400854931ec3e3/flash_mla/flash_mla_interface.py)
- Ascend 与 CUDA 功能范围不同：README 标注融合 kernel、稠密 MHA 暂仅 CUDA。ABI 兼容性也受编入的 GPU 架构或 torch_npu 版本约束。[README.md](https://github.com/deepseek-ai/FlashMLA/blob/0f11e178da1f67becb087a324b400854931ec3e3/README.md)
- TFlops、峰值利用率与提速均是上游特定条件结果，本轮未复现；根 MIT 不覆盖权重与其他子模块条款。GitHub Release 列表为空不等于没有源码更新。[README.md](https://github.com/deepseek-ai/FlashMLA/blob/0f11e178da1f67becb087a324b400854931ec3e3/README.md) [LICENSE](https://github.com/deepseek-ai/FlashMLA/blob/0f11e178da1f67becb087a324b400854931ec3e3/LICENSE)

## 补充建议

保留原服务基线，在目标卡上先跑正确性测试；覆盖长短上下文、空 indices、精度与缓存格式，再做固定负载 benchmark。记录 commit、子模块、驱动、编译器、torch / CUDA 或 CANN、时钟与总延迟。本轮未编译或占用 GPU / NPU。

## 参考资料

- [README.md](https://github.com/deepseek-ai/FlashMLA/blob/0f11e178da1f67becb087a324b400854931ec3e3/README.md)
- [LICENSE](https://github.com/deepseek-ai/FlashMLA/blob/0f11e178da1f67becb087a324b400854931ec3e3/LICENSE)
- [setup.py](https://github.com/deepseek-ai/FlashMLA/blob/0f11e178da1f67becb087a324b400854931ec3e3/setup.py)
- [flash_mla/flash_mla_interface.py](https://github.com/deepseek-ai/FlashMLA/blob/0f11e178da1f67becb087a324b400854931ec3e3/flash_mla/flash_mla_interface.py)
- [仓库 API](https://api.github.com/repos/deepseek-ai/FlashMLA)
