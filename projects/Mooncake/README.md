<!-- markdownlint-disable MD013 -->

# Mooncake

## 定位

Mooncake 围绕 KV cache 和 tensor 数据搬运组织大模型服务：Transfer Engine 负责跨设备 / 主机传输，Store 管理分布式对象，EP / PG 后端服务并行计算；prefill / decode 分离与共享 KV 池是不同接入路径。它不提供模型权重，也不能只靠安装包替换完整推理服务。[固定 README](https://github.com/kvcache-ai/Mooncake/blob/d49cef4115f17ae58ef299e730f1db890b7f0092/README.md)、[架构](https://github.com/kvcache-ai/Mooncake/blob/d49cef4115f17ae58ef299e730f1db890b7f0092/docs/source/design/architecture.md)

- 上游：[kvcache-ai/Mooncake](https://github.com/kvcache-ai/Mooncake)，仓库 ID `819733173`。
- 2026-11-23（Asia/Shanghai）07 时段：官方 C++ daily **+6**；API stars / forks / open issues（含 PR）**7,107 / 1,516 / 1,111**。[API](https://api.github.com/repos/kvcache-ai/Mooncake)
- 最新核到非预发行版 [v0.3.14](https://github.com/kvcache-ai/Mooncake/releases/tag/v0.3.14)，UTC 2026-11-03；当前主干 `d49cef4115f17ae58ef299e730f1db890b7f0092`。下面主干文档可能比发行包新，命令与功能必须按安装版本复核。
- 分类：`模型、训练与推理基础设施`。本轮仅抽读文档、元数据及会议摘要，未下载权重、启动 master、申请硬件或运行推理 / 通信测试。

## 用法

按目标硬件选择包与驱动。主干 quick start 要求 Python 3.10+；CUDA、非 CUDA、NPU、ROCm 等有不同构建，RDMA 还依赖网卡、驱动和内存注册能力。不能用某个后端安装成功外推全平台支持。[快速开始](https://github.com/kvcache-ai/Mooncake/blob/d49cef4115f17ae58ef299e730f1db890b7f0092/docs/source/getting_started/quick-start.md)、[协议矩阵](https://github.com/kvcache-ai/Mooncake/blob/d49cef4115f17ae58ef299e730f1db890b7f0092/docs/source/getting_started/supported-protocols.md)

在兼容 Linux 的独立测试环境，可参考固定 **0.3.14** 非 CUDA 包入口；本轮只核到该 PyPI 版本存在、要求 Python >=3.10，没有安装或验证 wheel：

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install 'mooncake-transfer-engine-non-cuda==0.3.14'
mooncake_master --help
```

[PyPI 版本元数据](https://pypi.org/pypi/mooncake-transfer-engine-non-cuda/0.3.14/json)。单机 API 演练还需启动 Store master，默认 RPC 端口 50051；主干示例让 `MooncakeDistributedStore.setup` 使用 `metadata_server="P2PHANDSHAKE"`、`protocol="tcp"` 和 `master_server_addr="127.0.0.1:50051"`，然后 put / get / close。该路径无需单独 TE 元数据服务，但 loopback 客户端地址不证明 master 只监听本机。[主干完整示例](https://github.com/kvcache-ai/Mooncake/blob/d49cef4115f17ae58ef299e730f1db890b7f0092/docs/source/getting_started/quick-start.md)

生产接入应选择框架相应指南：PD 直接传输与 HiCache / Store pooling 的 connector、配置和版本不同。先确认 vLLM / SGLang 的具体版本、模型、KV 格式和网络拓扑，再开启跨实例共享。[集成目录](https://github.com/kvcache-ai/Mooncake/blob/d49cef4115f17ae58ef299e730f1db890b7f0092/README.md)

## 原理

prefill 生成的 KV cache 可在兼容请求间复用，减少重复前缀计算；共享池利用主机内存及其他层级容量，传输引擎把 KV 或 tensor 搬到计算节点。收益取决于重用率、搬运带宽与延迟，缓存低命中时也可能增加网络和调度开销。[架构](https://github.com/kvcache-ai/Mooncake/blob/d49cef4115f17ae58ef299e730f1db890b7f0092/docs/source/design/architecture.md)

Store 将 key 当作不透明字符串，模型 / release / 请求组的命名由推理框架负责。SGLang 的 served model / extra_backend_tag、vLLM 的 cache_prefix / cache_salt 和 Store 的 tenant_id 解决不同层级的共享范围；同一租户不自动说明 KV 兼容。[共享与隔离](https://github.com/kvcache-ai/Mooncake/blob/d49cef4115f17ae58ef299e730f1db890b7f0092/docs/source/deployment/kv-cache-sharing-and-isolation.md)

## 价值

- 给 PD 分离、前缀复用、层级缓存和训练 / rollout 数据交换提供可组合的数据层。
- 提供多后端协议、可追溯部署文档与匿名请求 trace，可用于模拟容量 / 命中率，并设计目标集群实验。
- 开源实现和论文可帮助分析系统瓶颈；本轮没有独立测量吞吐、数值正确性、尾延迟、成本或故障恢复。

## 风险边界

- **性能声明有版本与分母。** 当前 README 写 Kimi 特定实际负载下多处理 75% 请求；FAST'25 官方会议摘要则列 trace 实验有效请求容量 +59%～498%，A800 / H800 部署 +115% / +107%。这些来自不同资料及场景，不合成为当前通用加速比，也不视为本文复现。先固定 SLO、输入 / 输出长度、cache 命中、硬件与基线。[README](https://github.com/kvcache-ai/Mooncake/blob/d49cef4115f17ae58ef299e730f1db890b7f0092/README.md)、[USENIX 摘要](https://www.usenix.org/conference/fast25/presentation/qin)
- **支持按组件核。** classic TE 与 TENT 的矩阵不同，例如当前文档把 TPU 列为 TENT 实验性、XPU 列为 TENT advanced；能走 TCP 不说明获得 RDMA / GPUDirect 的性能。当前主干功能未必在 0.3.14 wheel 中，需用目标构建复核。[协议矩阵](https://github.com/kvcache-ai/Mooncake/blob/d49cef4115f17ae58ef299e730f1db890b7f0092/docs/source/getting_started/supported-protocols.md)
- **KV 兼容与命名。** 模型权重、量化、adapter 或 KV layout 改变时应更换 release namespace；路径末尾同名也可能造成 vLLM 标识碰撞。不要每请求随机 salt 后仍期待跨请求命中。[共享规则](https://github.com/kvcache-ai/Mooncake/blob/d49cef4115f17ae58ef299e730f1db890b7f0092/docs/source/deployment/kv-cache-sharing-and-isolation.md)
- **租户默认与认证分层。** tenant quota admission 默认关闭；严格模式需显式启用和注册租户，quota 包含完成的 MEMORY replicas 与在途 MEMORY allocations。tenant_id / namespace 是对象分组与配额机制，不能单凭它证明调用者身份、传输加密或恶意租户隔离；本轮没有全链路安全审计。[多租户部署](https://github.com/kvcache-ai/Mooncake/blob/d49cef4115f17ae58ef299e730f1db890b7f0092/docs/source/deployment/multi-tenancy.md)
- **控制面和恢复。** quota admin API 与 metrics 共用 HTTP 端口；应核网络暴露和管理授权。Store 的 eviction、HA、oplog、SSD / 外部存储配置各有条件，缓存服务不能未经恢复演练就当作唯一持久数据源。[部署指南](https://github.com/kvcache-ai/Mooncake/blob/d49cef4115f17ae58ef299e730f1db890b7f0092/docs/source/deployment/mooncake-store-deployment-guide.md)、[租户管理](https://github.com/kvcache-ai/Mooncake/blob/d49cef4115f17ae58ef299e730f1db890b7f0092/docs/source/deployment/multi-tenancy.md)
- **trace 与许可。** 公开 trace 提供到达时间、token 长度和重映射 block hash，能支持缓存模拟，不能重建回答质量或代替真实租户流量。代码 Apache-2.0；模型、服务、硬件 SDK 与数据条款另核。[trace 说明](https://github.com/kvcache-ai/Mooncake/blob/d49cef4115f17ae58ef299e730f1db890b7f0092/FAST25-release/README.md)、[LICENSE](https://github.com/kvcache-ai/Mooncake/blob/d49cef4115f17ae58ef299e730f1db890b7f0092/LICENSE-APACHE)

## 补充建议

先在单机 TCP 做 put / get、关闭与重连，再用小流量验证缓存 key、模型切换和版本 namespace；之后才测 RDMA / 多节点。在同一 workload 下分别报告命中率、网络字节、TTFT、逐 token 延迟、满足 SLO 的请求吞吐及恢复耗时，把 trace 模拟、通信测试与完整推理验收分开。

## 参考资料

- [固定 README](https://github.com/kvcache-ai/Mooncake/blob/d49cef4115f17ae58ef299e730f1db890b7f0092/README.md)、[v0.3.14](https://github.com/kvcache-ai/Mooncake/releases/tag/v0.3.14)、[架构](https://github.com/kvcache-ai/Mooncake/blob/d49cef4115f17ae58ef299e730f1db890b7f0092/docs/source/design/architecture.md)。
- [快速开始](https://github.com/kvcache-ai/Mooncake/blob/d49cef4115f17ae58ef299e730f1db890b7f0092/docs/source/getting_started/quick-start.md)、[支持协议](https://github.com/kvcache-ai/Mooncake/blob/d49cef4115f17ae58ef299e730f1db890b7f0092/docs/source/getting_started/supported-protocols.md)、[部署指南](https://github.com/kvcache-ai/Mooncake/blob/d49cef4115f17ae58ef299e730f1db890b7f0092/docs/source/deployment/mooncake-store-deployment-guide.md)。
- [多租户](https://github.com/kvcache-ai/Mooncake/blob/d49cef4115f17ae58ef299e730f1db890b7f0092/docs/source/deployment/multi-tenancy.md)、[KV 共享与隔离](https://github.com/kvcache-ai/Mooncake/blob/d49cef4115f17ae58ef299e730f1db890b7f0092/docs/source/deployment/kv-cache-sharing-and-isolation.md)、[公开 traces](https://github.com/kvcache-ai/Mooncake/blob/d49cef4115f17ae58ef299e730f1db890b7f0092/FAST25-release/README.md)、[FAST'25 会议摘要与视频入口](https://www.usenix.org/conference/fast25/presentation/qin)。本轮未通读论文或完整观看演讲。
