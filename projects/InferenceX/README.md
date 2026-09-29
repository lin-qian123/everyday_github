<!-- markdownlint-disable MD013 -->

# InferenceX（SemiAnalysisAI/InferenceX）

> 上游仓库：<https://github.com/SemiAnalysisAI/InferenceX> · 归类：模型、训练与推理基础设施 · 本页基于 2026-09-30 的 GitHub API、README、benchmark / runner 文档、dashboard、贡献规则与 LICENSE 静态整理，未占用 GPU 集群、运行 benchmark 或复核上游结果。

- 抓取快照：1,786 stars、309 forks、291 open issues。
- 热度信号：GitHub Python Trending 抓取时约 +8 当日 stars。
- 版本与许可：Apache-2.0；无 GitHub Release，API 首个 tag 为 `tilert-v0.1.5.post2-inferencex.1`，各 benchmark 子项目独立演进。

## 定位

InferenceX 是持续追踪开源 LLM inference 软件 / 硬件组合的研究平台，前身为 InferenceMAX。仓库包含端到端 serving benchmark、CollectiveX 通信测试、OperatorX kernel 测试、系统功耗模型和 AgentX 长上下文多轮 workload；公开 dashboard 用于展示经上游流程产生的结果。

## 用法

读者可先用公开 dashboard 比较指定模型、硬件和软件栈，再回到 `inferencex-e2e` 的配置、runner、评测和 troubleshooting 文档核对口径。要对已有 endpoint 跑 AgentX，可按 standalone 文档安装 client 并使用 `aiperf profile`。正式提交结果应遵循贡献清单、保存软件镜像 / 参数 / 硬件拓扑，并明确官方与非官方结果身份。

## 原理

平台把持续变化的 vLLM、SGLang、TensorRT-LLM、CUDA / ROCm、kernel、调度与分布式通信版本固定到具体 benchmark run，以 latency / throughput 等曲线追踪 Pareto frontier。端到端、collective、operator 和 power model 分层，避免只凭一个 token/s 数字解释整个系统；AgentX 则加入长上下文、多轮和 agentic workload。

## 价值

推理软件每天变化，静态发布时的一次跑分很快过期。InferenceX 的价值在于公开 benchmark harness、配置和长期曲线，让团队可以从“哪张卡更快”进一步追问具体模型、batch、并发、上下文、精度和软件版本，并复用其检查清单建立内部基线。

## 风险边界

- 官方 dashboard 与 README 数字由项目方提供，本轮未复跑；赞助算力、机器质量、调参经验和软件分支都可能影响可比性。
- 上游要求只有本仓库结果可称 Official InferenceX；fork 或本地运行必须明确标为 unofficial，不能混用品牌与结论。
- 不同模型、精度、prompt / output 长度、batch、并发与 SLA 的 Pareto 曲线不可只抽取峰值 token/s 横比。
- AgentX 的“1Mil+ long context”等标签不自动证明任务正确性、工具成功率、成本可接受或真实生产 workload 代表性。
- 无统一 GitHub Release 且首个 tag 指向特定组件；部署必须固定 commit、镜像、driver 与子项目版本，不能只写“latest”。
- Apache-2.0 覆盖仓库代码，不自动覆盖模型权重、数据集、GPU 软件、厂商工具和 dashboard 内容。

## 补充建议

选型时重跑与自身 workload 对齐的 arrival pattern、输入 / 输出长度、并发、精度和 SLO，并同时记录能耗、错误率、冷启动和总成本。保留完整环境清单、原始日志与置信区间；把 upstream dashboard 当作候选筛选和回归参照，而不是采购或容量规划的唯一依据。

## 参考资料

- [GitHub 仓库](https://github.com/SemiAnalysisAI/InferenceX)
- [GitHub REST API](https://api.github.com/repos/SemiAnalysisAI/InferenceX)
- [公开 Dashboard](https://inferencex.semianalysis.com/)
- [InferenceX e2e](https://github.com/SemiAnalysisAI/InferenceX/tree/main/inferencex-e2e)
- [AgentX standalone](https://github.com/SemiAnalysisAI/InferenceX/blob/main/inferencex-e2e/docs/agentx-standalone.md)
- [PR Review Checklist](https://github.com/SemiAnalysisAI/InferenceX/blob/main/inferencex-e2e/docs/PR_REVIEW_CHECKLIST.md)
- [贡献说明](https://github.com/SemiAnalysisAI/InferenceX/blob/main/CONTRIBUTING.md)
- [LICENSE](https://github.com/SemiAnalysisAI/InferenceX/blob/main/LICENSE)
