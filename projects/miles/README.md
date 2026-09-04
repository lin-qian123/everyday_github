<!-- markdownlint-disable MD013 -->

# miles（radixark/miles）

> 记录日期：2026-09-05（Asia/Shanghai）。本页依据 GitHub REST API、上游 README、文档与 release 做静态整理；未在本机部署或运行训练。

## 定位

`Miles` 是面向大规模 LLM / VLM 后训练的强化学习框架。上游把 SGLang 用作高吞吐 rollout 层，把 Megatron-LM 或 PyTorch FSDP2 用作训练后端，并面向多轮 agent、MoE、低精度和大规模集群提供调度、权重更新、可观测性与故障恢复能力。

2026-09-05 的 GitHub 官方 Python Trending 快照显示约 `+55 stars today`；REST API 快照为 `2,545 stars / 442 forks / 955 open issues`，许可证为 Apache-2.0，最新 GitHub release 为 `v0.1.0`（2026-08-18）。这些数字只表示抓取时点的公开关注和项目状态，不等于训练质量或生产成熟度。

## 用法

上游把安装、硬件矩阵、模型支持和最小实验拆进独立文档。建议先按以下顺序评估：

1. 阅读安装页，确认 GPU、驱动、容器、Megatron-LM / FSDP2 后端和模型组合是否在支持矩阵中。
2. 从 quick start 的小模型、少节点配置开始，先验证数据、rollout、reward、训练和 checkpoint 闭环。
3. 固定镜像、模型 revision、数据集、并行拓扑、精度与随机种子，再扩大 GPU 数量。
4. 对 agentic rollout 单独保存请求、trajectory、reward、失败类型与成本，避免只看最终 reward。

它不是消费级“一键微调器”；没有相应 GPU、网络和分布式运维能力时，应先在受支持的小配置或托管测试环境中验证。

## 原理

- **分离 rollout 与训练**：异步模式让生成 worker 与训练 worker 解耦，并允许配置 on-policy / off-policy 节奏。
- **SGLang rollout 路由**：请求在多个 engine 间分配，保留请求元数据并做健康检查，适配多轮 agent 环境。
- **训练后端**：大型模型和并行 recipe 以 Megatron-LM 为主，同时提供 FSDP2 路径。
- **权重同步**：上游提供面向分离式部署的 P2P / RDMA 权重传输方案，让新权重回到 rollout engine。
- **一致性机制**：Token-in-token-out 避免 rollout 与训练之间反复 detokenize / retokenize；Rollout Routing Replay 记录并重放 MoE expert routing，以减少 rollout 与训练的路由错位。
- **精度与适配器**：覆盖 BF16、FP16、FP8、MXFP8、NVFP4、INT4 QAT、LoRA 与 multi-LoRA；具体数值稳定性依赖模型、硬件和 recipe。

## 价值

- 将 agent 环境、生成服务、reward / verifier、分布式训练和权重回传放入同一工程链路。
- 对大规模 MoE、低精度和异步 RL 提供比教学代码更完整的运行与故障恢复表面。
- 可与 SGLang、Megatron-LM 和多种 sandbox / verifier 生态组合，适合研究大规模 agent 后训练基础设施。
- 上游公开文档、recipe 和 release，便于在固定版本下做可复现审计。

## 风险边界

- 上游的“enterprise-ready”“trillion-parameter”“day-0 support”和性能数字是上游声明；本页未复现实验。
- 异步 rollout 会引入 policy lag、样本新鲜度和 on/off-policy 偏差，吞吐提升不能替代训练正确性检查。
- 低精度、MoE routing replay 和快速权重同步会扩大数值、版本、网络拓扑与 kernel 兼容性矩阵。
- `955` 个开放 issue 是 API 字段快照，可能包含 PR；它既不是故障率，也不是成熟度评分。
- agent 环境提供的 sandbox 仍需逐后端审计文件、网络、凭据、容器逃逸和清理行为。
- 模型权重、训练数据、reward 数据、benchmark 与第三方环境各自有许可证和隐私边界，Apache-2.0 只覆盖本仓库代码。

## 补充建议

- 先做一套单节点、确定性较强的 smoke / correctness baseline，再测多节点吞吐。
- 同时报告有效训练 token、rollout 丢弃率、policy lag、reward 分布、KL、checkpoint 恢复和端到端成本。
- 对上游性能表记录硬件、网络、容器 digest、commit、模型、序列长度、并发与采样参数。
- 把“训练作业启动”“checkpoint 生成”“评测完成”和“目标提升成立”分成不同验收状态。
- 对 agentic RL 保留原始 trajectory 与独立 verifier，抽样人工审查 reward hacking 和数据污染。

## 参考资料

- [GitHub 仓库](https://github.com/radixark/miles)
- [GitHub REST API](https://api.github.com/repos/radixark/miles)
- [官方文档](https://miles.radixark.com/docs)
- [安装说明](https://miles.radixark.com/docs/getting-started/installation)
- [Quick Start](https://miles.radixark.com/docs/getting-started/quick-start)
- [v0.1.0 Release](https://github.com/radixark/miles/releases/tag/v0.1.0)
