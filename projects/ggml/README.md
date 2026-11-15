<!-- markdownlint-disable MD013 -->

# ggml（ggml-org/ggml）

- GitHub：<https://github.com/ggml-org/ggml>
- 核查：2026-11-16（Asia/Shanghai）07 时段；15,891 stars / 2,018 forks / 386 open issues（含 PR）；仓库 ID `538180525`。
- 热度：官方综合 / C++ daily 均为 +53；首次建档不等于新项目发布。
- 版本：稳定 [v1.0.0](https://github.com/ggml-org/ggml/releases/tag/v1.0.0)，UTC 11-13；固定 master `417a024b4fb6bc3116d41af7c067166a039bdf12`，CMake 版本同为 1.0.0；MIT。
- 证据：官方发行、固定文档与示例相关代码的静态核读；本轮未编译、推理或测试性能。

## 定位

GGML 是面向机器学习的轻量 C/C++ 张量库，提供计算图、量化数据类型、多种 CPU / GPU / NPU 后端与调度。它是执行层基础设施：模型加载、tokenizer、采样、服务与应用协议仍需由上层项目组合。不能把 GGML、GGUF 文件格式和 llama.cpp 应用当作同一对象。[固定 README](https://github.com/ggml-org/ggml/blob/417a024b4fb6bc3116d41af7c067166a039bdf12/README.md)

## 用法

学习时先固定源码版本，按 README 使用 CMake 构建；以 `examples/simple` 的矩阵乘法理解维度与存储方向，再接具体模型。以下仅为待执行示例：

```bash
git clone https://github.com/ggml-org/ggml
cd ggml
git checkout v1.0.0
cmake -S . -B build
cmake --build build --config Release -j 8
```

`simple-ctx` 不支持 GPU，`simple-backend` 演示 CPU / CUDA / Metal 后端。CUDA 构建开关默认关闭，Apple 上 Metal 有平台相关默认值；选择 GPU 需匹配工具链和构建选项，不能从一次默认构建推出已使用 GPU。`GGML_RPC` 默认关闭。[示例说明](https://github.com/ggml-org/ggml/blob/417a024b4fb6bc3116d41af7c067166a039bdf12/examples/simple/README.md)、[构建选项](https://github.com/ggml-org/ggml/blob/417a024b4fb6bc3116d41af7c067166a039bdf12/CMakeLists.txt)

## 原理

示例先创建张量与 `ggml_mul_mat` 图节点，再由 backend scheduler 分配图缓冲、上传输入、执行计算并取回结果。张量的逻辑形状、内存布局和后端缓冲分开处理，量化格式减少存储与传输负担，但具体算子仍需对应后端实现。[后端示例](https://github.com/ggml-org/ggml/blob/417a024b4fb6bc3116d41af7c067166a039bdf12/examples/simple/simple-backend.cpp)

GGUF 则以元数据键值、张量描述和二进制数据保存模型；文件名只是便于人读的约定，类型与布局需读真实元数据。它不替代运行时对架构、算子和量化格式的支持。[GGUF 规范](https://github.com/ggml-org/ggml/blob/417a024b4fb6bc3116d41af7c067166a039bdf12/docs/gguf.md)

## 价值

适合研究端侧推理的内存、数据搬移与异构执行，也适合作为小型算子实验入口。与庞大模型相比，矩阵示例更容易对照参考结果、分开构图 / 分配 / 传输 / 执行时间。跨后端接口能减少应用重复接入代码，实际加速效果仍取决于工作负载。

## 风险边界

- **1.0 迁移并非只改版本号。** 发行说明明确删除 deprecated API 和旧 `DIAG_MASK` 算子，并把 RPC 协议升至 v9；调用方、构图代码和远端组件要一起核对。[发行说明](https://github.com/ggml-org/ggml/releases/tag/v1.0.0)
- 多后端性能改动属于维护方发行记录，本轮没有同机对照。FP8 / 低比特支持不证明任意模型质量、速度或所有硬件均受益。
- README 的运行阶段零分配目标有初始化、图缓冲规划与上层应用范围；示例仍显式分配图和缓冲，不能解释为整个进程无需分配内存。
- 本地库、远端 RPC、模型下载与应用日志是不同边界；RPC 版本握手不能据此视为身份认证或安全隔离。本轮未审计 RPC 安全实现。
- MIT 约束库代码；权重、训练数据和下游分发各有独立许可，转换成 GGUF 不改变这些权利。

## 补充建议

先用 CPU 浮点参考结果，再测一个量化配置与一个目标后端。固定提交、编译器、驱动、构建开关、形状和线程数，记录数值误差、峰值内存及分阶段耗时。跨主机实验应单列网络与访问策略。核心及 CMake 贡献按上游 README 指引投向 llama.cpp；不要误以为本仓库是所有变更的首选入口。

## 参考资料

- [仓库 API](https://api.github.com/repos/ggml-org/ggml)、[v1.0.0](https://github.com/ggml-org/ggml/releases/tag/v1.0.0)。
- [固定 README](https://github.com/ggml-org/ggml/blob/417a024b4fb6bc3116d41af7c067166a039bdf12/README.md)、[CMake](https://github.com/ggml-org/ggml/blob/417a024b4fb6bc3116d41af7c067166a039bdf12/CMakeLists.txt)、[MIT](https://github.com/ggml-org/ggml/blob/417a024b4fb6bc3116d41af7c067166a039bdf12/LICENSE)。
- [矩阵示例](https://github.com/ggml-org/ggml/blob/417a024b4fb6bc3116d41af7c067166a039bdf12/examples/simple/README.md)、[后端代码](https://github.com/ggml-org/ggml/blob/417a024b4fb6bc3116d41af7c067166a039bdf12/examples/simple/simple-backend.cpp)、[GGUF](https://github.com/ggml-org/ggml/blob/417a024b4fb6bc3116d41af7c067166a039bdf12/docs/gguf.md)。
