<!-- markdownlint-disable MD013 -->

# NVIDIA Dynamo（ai-dynamo/dynamo）中文解读

> 上游仓库：<https://github.com/ai-dynamo/dynamo> · 归类：模型、训练与推理基础设施 · 证据快照：2026-10-16（Asia/Shanghai）。API：8,305 stars / 1,705 forks / 1,993 open issues；API NOASSERTION；根 LICENSE 指定主体 Apache-2.0，DeepSeek-V3.2 测试数据为 MIT；稳定 Release `v1.5.1`；tags 首项是 `v1.6.0-nemotron-3.5-super-vl-dev.1` 开发版。本页为上游文档与相关源码的静态整理，未安装运行、接入真实数据 / 凭据、复测性能或完成全面安全审计。

## 定位

Dynamo 是位于 vLLM、SGLang、TensorRT-LLM 等推理引擎之上的数据中心服务编排层。它协调多 GPU / 多节点的 prefill、decode、KV cache、路由与扩缩容，面向需要低延迟和高吞吐的集群部署；单模型单卡通常可先使用底层引擎。

## 用法

先选固定 `1.5.1` 的官方 runtime 镜像和一个后端，按 quickstart 启动 frontend 与小模型 worker，通过本地 `/v1/chat/completions` 验证基础链路。README 的 vLLM 示例采用 `Qwen/Qwen3-0.6B`、file discovery 与 8000 端口；第一次仅在隔离主机使用。生产按上游 Kubernetes 路径补认证 / TLS 网关、NetworkPolicy、ServiceAccount 与资源限额，再引入 disaggregated serving。

## 原理

- 将 prefill 与 decode 分成可独立扩缩容的 GPU pool，通过 NIXL 等传输 KV 数据。
- Router 结合 worker 负载与 KV 重叠选择目标，减少重复 prefill；KVBM 将缓存管理扩展到 GPU、CPU、SSD 或远端存储。
- Planner 通过 workload profile / SLA 调整规模；Grove、ModelExpress 等配套处理拓扑调度与权重启动。
- Rust runtime 与 Python 扩展组织 frontend、backend 和内部 discovery / event / request planes，后端支持矩阵需要逐项查验。

## 价值

- 把多节点推理的路由、cache 和容量问题统一到可观测控制面，利于分析 TTFT 与吞吐瓶颈。
- prefill / decode 独立配置有机会减少资源浪费，但收益取决于工作负载、网络和卡型。
- 模块化后端与 Kubernetes 集成方便分阶段引入，避免一开始就改写模型执行引擎。

## 风险边界

- 安全文档明确假设可信网络：外部用户只通过带认证 / TLS 的网关访问 frontend；frontend、planner、router、NATS、etcd、ZMQ 等不得直接暴露给不可信网络。
- 示例 Compose / manifests 只用于本地演示；KV 事件和 request planes 可携带或推断 prompt 数据，TLS / mTLS、发布订阅权限和 RDMA 隔离必须联合治理。
- 网关的 Endpoint Picker 负责调度，不负责用户认证；mTLS 身份也不能代替业务授权。
- README 吞吐倍率混有不同硬件 / baseline / 模型条件，本页未复测，不能把跨硬件比较当作软件单独加速倍数。
- API 没识别 SPDX 不代表无许可；根 LICENSE 对主体和一组测试数据分别给出 Apache-2.0 / MIT，镜像依赖、权重和第三方组件还需单列。

## 补充建议

- 固定同型号 GPU、模型 / 精度和 trace，分别比较单引擎、aggregated 与 disaggregated 的 TTFT、TPOT、吞吐、网络与成本。
- 在小型测试集群验证 worker 故障、KV stale、取消、超载和扩缩容，再评估模型迁移与多租户边界。
- 将模型文件、镜像 digest、backend 版本、K8s 配置和完整 benchmark 参数纳入复现清单，优先稳定 Release。

## 参考资料

- 上游仓库：<https://github.com/ai-dynamo/dynamo>
- GitHub REST API：<https://api.github.com/repos/ai-dynamo/dynamo>
- README / 后端矩阵：<https://github.com/ai-dynamo/dynamo/blob/main/README.md>
- CLI quickstart：<https://github.com/ai-dynamo/dynamo/blob/main/docs/fern/pages/cli/getting-started/quickstart.mdx>
- 部署安全与信任模型：<https://github.com/ai-dynamo/dynamo/blob/main/docs/fern/pages/developer-guide/security/secure-deployment-guidelines.md>
- 安全报告入口：<https://github.com/ai-dynamo/dynamo/blob/main/SECURITY.md>
- LICENSE 与测试数据例外：<https://github.com/ai-dynamo/dynamo/blob/main/LICENSE>
- Releases：<https://github.com/ai-dynamo/dynamo/releases>
