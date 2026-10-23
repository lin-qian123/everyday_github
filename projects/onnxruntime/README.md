<!-- markdownlint-disable MD013 -->

# onnxruntime

- 主上游：[microsoft/onnxruntime](https://github.com/microsoft/onnxruntime)
- 分类：模型、训练与推理基础设施。
- 核验日期：2026-10-24（Asia/Shanghai）；默认分支 `main` 快照 `73b0fc6c0533`。
- [API](https://api.github.com/repos/microsoft/onnxruntime) 快照：22,154 stars / 4,360 forks / 1,818 open issues；发行列表首项 [v1.31.0](https://github.com/microsoft/onnxruntime/releases/tag/v1.31.0)（UTC 2026-10-09，正式）。累计量不是今日增长，主线也不等于发行版。

## 定位

ONNX Runtime 是跨平台机器学习推理与训练运行时，接受 ONNX 模型，利用计算图优化与不同硬件后端执行。适用于把训练框架导出的模型接入桌面、移动或服务端应用；并非模型权重或完整 Agent 产品。 [README.md](https://github.com/microsoft/onnxruntime/blob/73b0fc6c0533771f01958ca1f19dc0d77ed36ce3/README.md)

## 用法

先选 CPU 或与设备兼容的 GPU / Execution Provider 构建，在独立环境锁版本。以下为已有可信 ONNX 文件的最小 CPU 检查，需自行提供 `model.onnx`；本轮未执行：

```sh
python -m pip install onnxruntime==1.31.0
```

```python
import onnxruntime as ort
session = ort.InferenceSession("model.onnx", providers=["CPUExecutionProvider"])
print(session.get_providers())
print([(x.name, x.shape, x.type) for x in session.get_inputs()])
```

之后按真实输入类型 / 形状准备数组并调用 `session.run`，不要把成功加载当成数值正确或已使用目标加速器。 [官方 Python 入门](https://onnxruntime.ai/docs/get-started/with-python.html)

## 原理

Execution Provider 把支持的子图映射到 CUDA、CoreML、QNN、CPU 等后端，图优化、融合与内存规划进一步改变执行方式。按优先级配置多个 EP 时，部分算子可能落到另一后端，因此需要 profiler 核实际覆盖与数据拷贝成本。 [Execution Providers](https://onnxruntime.ai/docs/execution-providers/)

## 价值

统一应用侧推理接口，减少不同训练框架与设备之间的接入成本。速度收益依赖模型、精度、batch、动态形状与 EP；应同时报告导出误差、冷启动和真实硬件性能。

## 风险边界

- 正式发行首项 v1.31.0；主线 `VERSION_NUMBER` 已为 1.32.0。CUDA plugin 也有独立发行，主线、运行时 wheel 和 EP 插件需要分别锁定。 [VERSION_NUMBER](https://github.com/microsoft/onnxruntime/blob/73b0fc6c0533771f01958ca1f19dc0d77ed36ce3/VERSION_NUMBER)
- 本轮读取主线及 v1.31.0 的隐私文档：受支持官方 native 构建默认有遥测，平台可走 ETW 或 1DS；部分目标不含 provider。需要按实际构建核对。`ORT_DISABLE_TELEMETRY=1` 要在初始化前设置，仅适用于 1DS；`--no_telemetry` 是构建选项，普通 API 关闭非必要事件可能晚于初始化事件。 [docs/Privacy.md](https://github.com/microsoft/onnxruntime/blob/73b0fc6c0533771f01958ca1f19dc0d77ed36ce3/docs/Privacy.md)、[v1.31.0 隐私说明](https://github.com/microsoft/onnxruntime/blob/v1.31.0/docs/Privacy.md)
- 外部模型与自定义算子需按不可信输入处理；量化 / 图优化可能改变精度，CPU 回退也会影响延迟。根 MIT 不覆盖外部模型与全部 EP 依赖。 [LICENSE](https://github.com/microsoft/onnxruntime/blob/73b0fc6c0533771f01958ca1f19dc0d77ed36ce3/LICENSE)

## 补充建议

先与原框架对照固定输入，记录输出最大误差与任务指标；再做冷 / 热启动、P50 / P95、内存和实际 EP 分配。按应用要求在初始化前设置遥测策略，并观察网络行为。本轮未下载模型、安装 wheel、运行推理或做性能对照。

## 参考资料

- [README.md](https://github.com/microsoft/onnxruntime/blob/73b0fc6c0533771f01958ca1f19dc0d77ed36ce3/README.md)（固定 commit）。
- [docs/Privacy.md](https://github.com/microsoft/onnxruntime/blob/73b0fc6c0533771f01958ca1f19dc0d77ed36ce3/docs/Privacy.md)（固定 commit）。
- [VERSION_NUMBER](https://github.com/microsoft/onnxruntime/blob/73b0fc6c0533771f01958ca1f19dc0d77ed36ce3/VERSION_NUMBER)（固定 commit）。
- [LICENSE](https://github.com/microsoft/onnxruntime/blob/73b0fc6c0533771f01958ca1f19dc0d77ed36ce3/LICENSE)（固定 commit）。
- [v1.31.0 隐私说明](https://github.com/microsoft/onnxruntime/blob/v1.31.0/docs/Privacy.md)（本轮另行读取发行 tag）。
- [官方 Python 入门](https://onnxruntime.ai/docs/get-started/with-python.html)、[Execution Providers](https://onnxruntime.ai/docs/execution-providers/)（动态文档）。
- [发行列表](https://github.com/microsoft/onnxruntime/releases)、[仓库 API](https://api.github.com/repos/microsoft/onnxruntime)（动态状态）。
