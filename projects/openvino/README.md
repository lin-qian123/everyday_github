<!-- markdownlint-disable MD013 -->

# openvino

## 定位

OpenVINO 是模型转换、图优化与推理运行工具链，通过统一 API 对接 CPU、GPU、NPU 等具体后端。适合已有模型的本地部署与硬件选型；运行时、量化工具、GenAI 管线和 Model Server 属于相关但不同的组件，不能把它们的能力和版本合并看待。

- 上游：[openvinotoolkit/openvino](https://github.com/openvinotoolkit/openvino)，仓库 ID `153097643`，创建于 2018 年；本轮新建档，不是今日新发布的框架。
- 2026-11-19 07 时段：综合 / C++ daily 观察到 **+18**，同仓库不累加；stars / forks / open issues（含 PR）为 **11,308 / 3,601 / 1,159**。[API](https://api.github.com/repos/openvinotoolkit/openvino)
- 最新核到的非预发行版：[2026.4.1](https://github.com/openvinotoolkit/openvino/releases/tag/2026.4.1)，UTC 10-01；PyPI 同版要求 Python **3.10+**。[包元数据](https://pypi.org/pypi/openvino/2026.4.1/json)
- 文档与源码抽样固定在 master `31c323a0e3744cd22e448733c879347989100923`；主线 SHA 和 `2026` 文档站均不等于 2026.4.1 制品的逐字快照。分类：`模型、训练与推理基础设施`。

## 用法

下面从已有本地模型开始；本轮没有安装依赖、下载权重或运行推理。

```bash
python -m pip install openvino==2026.4.1
```

```python
import numpy as np
import openvino as ov

core = ov.Core()
print(core.available_devices)
model = core.read_model("model.xml")  # 同目录准备匹配的权重文件
compiled = core.compile_model(model, "CPU")
input_data = np.load("input.npy")   # 事先按模型约定准备
outputs = compiled({0: input_data})
```

这是单输入模型示意；实际须核输入名、shape、dtype、布局、预处理与输出语义。ONNX 等格式可由相应 frontend 读取，PyTorch / TensorFlow 等模型按转换流程处理。先列出设备，再选确实可用的 CPU / GPU / NPU；`available_devices` 有设备不保证目标模型所有算子、精度和动态 shape 都可编译运行。[README](https://github.com/openvinotoolkit/openvino/blob/31c323a0e3744cd22e448733c879347989100923/README.md)、[设备查询样例](https://github.com/openvinotoolkit/openvino/blob/31c323a0e3744cd22e448733c879347989100923/samples/python/hello_query_device/hello_query_device.py)

## 原理

frontend 把框架格式读入统一模型表示，公共变换和低精度变换处理图，再由设备 plugin 编译、执行，runtime 以统一接口管理请求。CPU / GPU / NPU 是具体执行设备，AUTO、HETERO 与自动 batching 则是设备选择、异构分配或请求组织方式；它们不自动解决模型兼容与业务时延目标。[开发结构](https://github.com/openvinotoolkit/openvino/blob/31c323a0e3744cd22e448733c879347989100923/docs/dev/index.md)、[设备与模式](https://docs.openvino.ai/2026/openvino-workflow/running-inference/inference-devices-and-modes.html)

量化、压缩与生成式应用另涉及 NNCF、Tokenizers、GenAI 等生态组件。通用推理 runtime 能加载模型，不代表已经拥有完整聊天模板、采样、KV-cache 调度和对外认证服务；要按实际组合固定版本。

## 价值

- 对 Intel 平台部署，提供同一模型在不同后端和执行策略间进行工程比较的入口。
- 将模型格式、图编译与应用调用分层，便于定位转换失败、算子缺失或运行误差。
- 成熟的样例、性能文档和生态集成降低起步成本；“可运行”“更快”和“满足精度 / P95 时延”仍应分项验收。

## 风险边界

- **补丁与正确性有关。** 2026.4.1 发行说明列出滑窗 KV-cache 的索引 / shape 问题、动态 shape 的 GPU 输出错误、部分 NPU 驱动崩溃及输入 / blob 解析加固。这是维护方发布说明，本轮没有复现缺陷、补丁或具体受影响设备，不能据版本号宣布所有模型安全正确。
- **吞吐分母要对齐。** 官方性能页将 GenAI 吞吐定义为首 token 之后的 token 速率，不能当作端到端生成时间。比较时应另记模型加载、编译 / 缓存、TTFT、输入输出长度、batch、功耗和任务质量，不能只引用 tok/s。[性能口径](https://docs.openvino.ai/2026/about-openvino/performance-benchmarks.html)
- **量化与动态形状需要回归。** 相同模型名不代表相同权重、图变换和输入布局；先对照原框架数值及真实验证集，再比较速度。不能把 Intel 设备结果外推到任意 CPU / GPU，或把本机设备名称当作驱动可用性证明。
- **本地推理与遥测分开。** 官方遥测页写默认采集匿名使用 / 错误等数据，列出转换、下载与优化等工具，支持 `opt_in_out --opt_out`；这不证明每次 runtime 推理都会上传输入，也不代表关闭该开关就覆盖所有第三方组件。实际部署按所装组件和网络记录核验。[遥测说明](https://docs.openvino.ai/2026/about-openvino/additional-resources/telemetry.html)
- **软件许可不覆盖所有模型。** 本仓库为 Apache-2.0，第三方依赖、权重、数据集和服务仍需分别核；服务化还要配置自己的认证、配额和不可信模型输入边界。[LICENSE](https://github.com/openvinotoolkit/openvino/blob/31c323a0e3744cd22e448733c879347989100923/LICENSE)、[安全报告入口](https://github.com/openvinotoolkit/openvino/blob/31c323a0e3744cd22e448733c879347989100923/SECURITY.md)

## 补充建议

记录模型与权重哈希、OpenVINO / 驱动版本、设备、shape、精度、线程和缓存状态；对原框架 / OpenVINO 建立同输入数值及任务指标对照，再做冷 / 热启动、单请求延迟和并发吞吐测量。LLM 额外固定 tokenizer、聊天模板与采样条件。本轮只核资料和接口示例，不构成性能、模型正确性或硬件适配验收。

## 参考资料

- [2026.4.1 发行说明](https://github.com/openvinotoolkit/openvino/releases/tag/2026.4.1)
- [发行列表](https://github.com/openvinotoolkit/openvino/releases)；固定源码、官方文档与包元数据见各节。
