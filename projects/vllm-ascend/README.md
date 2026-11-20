<!-- markdownlint-disable MD013 -->

# vllm-ascend

## 定位

vLLM Ascend 是 vLLM 社区维护的华为昇腾 NPU 硬件插件，通过平台注册、模型及通信适配和 NPU 算子让 vLLM 使用 Ascend。它不是独立模型，也不是把 CUDA wheel 换个设备名即可完成的通用替代。

- 上游：[vllm-project/vllm-ascend](https://github.com/vllm-project/vllm-ascend)，仓库 ID `924058625`。
- 2026-11-21（Asia/Shanghai）07 时段：官方 Python daily **+7**；API stars / forks / open issues（含 PR）为 **3,127 / 2,794 / 5,433**。[API](https://api.github.com/repos/vllm-project/vllm-ascend)
- 最新核到非预发行版 [v0.30.0](https://github.com/vllm-project/vllm-ascend/releases/tag/v0.30.0)，UTC 10-29；更新的 [v0.32.0rc1](https://github.com/vllm-project/vllm-ascend/releases/tag/v0.32.0rc1)，UTC 11-10，**仍是预发行**。main 固定快照 `7a7ed073c481d5e3a2fc2194c5b879efb2d373c0` 又是独立开发状态。
- 分类：`模型、训练与推理基础设施`。首次建档，项目并非今日首发；本轮未申请 NPU、安装软件栈、下载权重或运行推理。

## 用法

先确定 **硬件型号 → 驱动 / 固件 → CANN → PyTorch / torch_npu → vLLM / 插件 → 模型 / 量化 / 并行组合**，再按对应版本指南操作。不要混用 main 的新说明和稳定版镜像。

固定 main README 的推荐软件栈为 Linux、Python 3.12、CANN 9.2.1、PyTorch 2.10.0、torch_npu 2.10.0.post7，vLLM 与插件版本匹配；同一快照 `setup.py` 的包元数据却只写 `python_requires>=3.10`，它不能代替经过验证的软件栈要求。[README](https://github.com/vllm-project/vllm-ascend/blob/7a7ed073c481d5e3a2fc2194c5b879efb2d373c0/README.md)、[setup.py](https://github.com/vllm-project/vllm-ascend/blob/7a7ed073c481d5e3a2fc2194c5b879efb2d373c0/setup.py)

main Quick Start 用预构建容器和 Qwen3-0.6B 做最小工作负载。以下仅展示**软件栈已准备好后**的服务 / 查询步骤，本轮未执行；实际部署还要选择版本对应镜像与设备映射：

```bash
vllm serve Qwen/Qwen3-0.6B --host 127.0.0.1 --port 8000
```

另一终端查询：

```bash
curl --fail http://127.0.0.1:8000/v1/completions \
  -H 'Content-Type: application/json' \
  -d '{"model":"Qwen/Qwen3-0.6B","prompt":"Beijing is a","max_tokens":5,"temperature":0}'
```

这里把上游示例改为显式 loopback；若在容器中由宿主访问，需按容器网络配置监听地址与端口映射，不能直接套用容器内 loopback。成功标准至少包括非空 `choices[0].text`，HTTP 200 或服务日志本身不能证明推理正确。[固定在线示例](https://github.com/vllm-project/vllm-ascend/blob/7a7ed073c481d5e3a2fc2194c5b879efb2d373c0/docs/source/getting_started/quick_start/online/qwen3-0.6b.inc.md)

## 原理

`setup.py` 通过 `vllm.platform_plugins` 注册 Ascend，通过 general plugins 注册 KV connector、model loader、profiling 和模型。[初始化入口](https://github.com/vllm-project/vllm-ascend/blob/7a7ed073c481d5e3a2fc2194c5b879efb2d373c0/vllm_ascend/__init__.py)返回 `NPUPlatform`，部分通用入口在 engine-core 初始化前应用进程级适配。这里是少量入口抽读，不是全部 kernel、scheduler 或通信实现审计。

vLLM 提供模型服务及调度体系，插件处理设备、执行、通信和算子适配。量化、prefix cache、prefill / decode 分离、推测解码和多种并行配置有组合约束；[feature matrix](https://github.com/vllm-project/vllm-ascend/blob/7a7ed073c481d5e3a2fc2194c5b879efb2d373c0/docs/source/user_guide/support_matrix/feature_matrix.md)明确区分完全、部分、不兼容与未知，单独支持两项不表示可任意叠加。

## 价值

- 为已有昇腾设备提供社区 vLLM 接入路径，可复用熟悉的服务接口和部分部署 / 评测工作流。
- 发行资料把支持范围细化到模型、硬件、量化和部署方式，比只列模型名更有选型价值。
- 可用小模型建立设备、驱动、容器和服务的最小闭环，再逐步放大；本轮没有跨硬件性能或成本实测，不能据此宣称优于 GPU。

## 风险边界

- **版本默认不同。** v0.30.0 发行说明仍默认 Model Runner V1，部分模型要显式用 V2；其说明同时指出 main 已改默认 V2。RC、main 的行为不能直接归给 stable。
- **RC 有明确回退样本。** v0.32.0rc1 Known Issues 列 Qwen2-Audio 初始化失败、A3 特定 GLM pooling P/D 长时间压力下服务中断，以及 950DT 多前缀 GLM workload 的 D-node 吞吐较 v0.30.0 最多约低 50%；均为上游限定场景 / 待查根因，不能扩写为全部模型回退，也不能只保留加速亮点。
- **稳定版仍需看已知问题。** v0.30.0 列 SSD KV pooling / 网络组合限制、结构化输出差异与部分 W4 权重精度问题。其说明还提示上游 `CVE-2026-114053` 与 main 修复；部署前需核对所用 vLLM 的公告、补丁及实际适用性，本轮未复现漏洞，也未认定 stable 制品已修复。[稳定版说明](https://github.com/vllm-project/vllm-ascend/releases/tag/v0.30.0)、[RC 说明](https://github.com/vllm-project/vllm-ascend/releases/tag/v0.32.0rc1)
- **容器不替代宿主栈。** main A2 示例映射 NPU 设备和宿主驱动库，也挂载模型缓存；预构建用户态栈不等于任意主机可用。示例 `-p 8000:8000` 与服务 `0.0.0.0` 应按实际访问范围收敛，认证另行配置。[A2 容器片段](https://github.com/vllm-project/vllm-ascend/blob/7a7ed073c481d5e3a2fc2194c5b879efb2d373c0/docs/source/getting_started/quick_start/ascend_image/atlas-a2.inc.md)
- **“离线推理”仍可能下载权重。** model ID 可能访问外部模型库；真正离线需预置授权权重、依赖与缓存。模型许可、prompt / 日志和服务访问控制与代码 Apache-2.0 分别核对。
- **性能与正确性一起验收。** 分开记录冷启动、prefill、TTFT、decode、队列和完整请求；量化与并行变化还要测输出正确性、任务指标、长时间稳定性与失败请求。

## 补充建议

对已经持有的 NPU 先保存 `npu-smi`、驱动 / 固件、镜像 digest 和完整依赖，再以版本匹配的小模型做非空输出与错误路径验证。大模型部署按支持矩阵逐项开启量化、并行、KV pooling 或推测解码，每次保存相同 workload 的正确性与延迟分布，并保留回退样本。

本轮接续重点是 stable / RC / main 的运行差异、已知问题修复状态和目标设备精度；没有成本、性能或生产可用性验收证据。

## 参考资料

- [固定 README](https://github.com/vllm-project/vllm-ascend/blob/7a7ed073c481d5e3a2fc2194c5b879efb2d373c0/README.md)、[setup.py](https://github.com/vllm-project/vllm-ascend/blob/7a7ed073c481d5e3a2fc2194c5b879efb2d373c0/setup.py)、[平台入口](https://github.com/vllm-project/vllm-ascend/blob/7a7ed073c481d5e3a2fc2194c5b879efb2d373c0/vllm_ascend/__init__.py)。
- [固定 Quick Start](https://github.com/vllm-project/vllm-ascend/blob/7a7ed073c481d5e3a2fc2194c5b879efb2d373c0/docs/source/getting_started/quick_start.md)、[硬件表](https://github.com/vllm-project/vllm-ascend/blob/7a7ed073c481d5e3a2fc2194c5b879efb2d373c0/docs/source/getting_started/installation/supported_hardware.inc.md)、[feature matrix](https://github.com/vllm-project/vllm-ascend/blob/7a7ed073c481d5e3a2fc2194c5b879efb2d373c0/docs/source/user_guide/support_matrix/feature_matrix.md)。
- [v0.30.0](https://github.com/vllm-project/vllm-ascend/releases/tag/v0.30.0)、[v0.32.0rc1](https://github.com/vllm-project/vllm-ascend/releases/tag/v0.32.0rc1)、[Apache-2.0](https://github.com/vllm-project/vllm-ascend/blob/7a7ed073c481d5e3a2fc2194c5b879efb2d373c0/LICENSE)。
