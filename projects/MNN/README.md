<!-- markdownlint-disable MD013 -->

# MNN：面向手机与边缘设备的推理引擎和 LLM 工具链

- 上游：[alibaba/MNN](https://github.com/alibaba/MNN)；仓库 ID：`181436799`。
- 快照：2026-11-08（Asia/Shanghai）；stars / forks / open issues（含 PR）：16,423 / 2,511 / 67；官方 daily 榜 C++ +26，不是自然日结算。
- 分类：模型、训练与推理基础设施；最新发行：[3.6.2](https://github.com/alibaba/MNN/releases/tag/3.6.2)（UTC 2026-10-29 09:38:22，非预发行标记）。
- 核读基线：`master@5b74a931887ba5b4d9f65b222cc18dd1a16599a8`。以下为文档与抽样源码核读，作者声明与本轮运行验证分开。

## 定位

MNN 是阿里开源的轻量深度学习计算引擎，覆盖模型转换、压缩、张量计算、训练与多后端推理。MNN-LLM 在其上提供 LLM 导出和生成；移动聊天 App、Diffusion 和 Avatar 属于不同应用 / 子路径。选择引擎支持，仍需确认目标模型、算子、精度与实际硬件。

## 用法

先固定 3.6.2 发行作为评估基线；Python 包入口为 `pip install mnn==3.6.2`，不能据此假设所有移动端 / NPU 组件都已安装。LLM 路径先取得有权使用的模型，按 transformers 文档导出为 MNN，并配置 tokenizer、embedding、权重与 JSON 文件，再构建对应后端。

源码中的 macOS / Linux 基础 LLM 示例为：

```bash
cmake -S . -B build -DMNN_LOW_MEMORY=true -DMNN_BUILD_LLM=true -DMNN_SUPPORT_TRANSFORMER_FUSE=true
cmake --build build --parallel
```

构建后按文档运行 `llm_demo model_dir/config.json`；视觉、音频、Metal / OpenCL / Hexagon 等另需相应选项和依赖。导出工具通过 PyMNN 或 MNNConvert 转换模型；从 ONNX 到 MNN 的转换成功不证明数值等价。本轮未安装、构建或下载权重。

## 原理

转换器将上游图和权重变为 MNN 表示并做图优化，运行时根据 backend、设备、算子与精度选择执行路径。LLM 导出配套 tokenizer、embedding 和 runtime config；低比特权重、算子融合、缓存以及投机解码分别减少存储、计算或自回归等待。INT4 权重并不表示所有算子都做全整数计算。

## 价值

适合在手机、PC 或嵌入式设备上研究模型部署、内存和异构加速。统一工具链可减少模型格式和硬件后端之间的接线，但通用支持表不能替代某个模型 / OS / GPU 的验收。

当前 README 的 11-04 新闻自报 MNN-Pocket-0.3B、W4A16 制品 173 MB、iPhone 18 Pro 解码 350 tok/s；3.6.2 发行另报告 Qwen3.5-2B 在 iPad Pro M5 的 DFlash 解码 2.09 倍。两者是不同模型 / 设备的作者结果，不能合并为本轮实测或任意手机的速度承诺。

## 风险边界

- 后端表包含不支持或“有 bug / 未优化”项；低精度、动态输入、量化配置与硬件代际会改变可用性。Hexagon 等不能从 CPU 成功推断兼容。
- 量化、图融合和投机解码须检查数值 / 任务质量；分别测 prefill、decode、首 token 延迟、上下文长度、峰值内存、耗电与持续温升。
- 主线 SHA 与 3.6.2 发行不同；API、模型导出依赖、编译选项、制品 / 缓存格式需按同一基线核对。
- 引擎能本地推理，不代表配套 App 的模型下载、更新或其他网络行为全部离线。
- 根代码 Apache-2.0 不自动覆盖模型权重、数据、第三方 backend SDK、App 资产或人物声音权利。
- 没有执行转换 / 推理 / 手机安装、GPU / NPU 测试，未复现作者速度、精度或模型能力。

## 补充建议

选一个模型和目标设备，保留原模型 / 导出制品哈希、tokenizer、量化参数与 backend 配置。先用相同输入比较参考模型的输出 / 质量，再做固定输入长度、输出长度、线程与热状态的基准。把“低磁盘占用”“低峰值内存”和“更快解码”分项报告，并记录不支持路径。

## 参考资料

- [README.md](https://github.com/alibaba/MNN/blob/5b74a931887ba5b4d9f65b222cc18dd1a16599a8/README.md)
- [transformers/README.md](https://github.com/alibaba/MNN/blob/5b74a931887ba5b4d9f65b222cc18dd1a16599a8/transformers/README.md)
- [LICENSE.txt](https://github.com/alibaba/MNN/blob/5b74a931887ba5b4d9f65b222cc18dd1a16599a8/LICENSE.txt)
- [GitHub API 快照](https://api.github.com/repos/alibaba/MNN)；[发行列表](https://github.com/alibaba/MNN/releases)。
