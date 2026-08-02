# time-to-first-token

## 定位

`time-to-first-token` 是面向工程师的 10 周 LLM 推理服务实践路线图：以一个 OpenAI-compatible 服务为主线，串起部署、观测、压测、量化、推测解码、路由和可复现实验。截至 2026-08-03 的 GitHub API 快照：项目创建于 2026-08-02，约 32 stars、1 fork，Apache-2.0。

## 用法

README 建议具备 Python、Transformer 架构与命令行基础后，以每次约 30 分钟、每周 5 次推进，并安装 vLLM、GuideLLM、SGLang、Docker/Prometheus/Grafana 等。它要求最终产出一个可部署且有 benchmark 的服务；GPU 租赁、模型选择和云账号由使用者自行承担。

## 原理

课程顺序以 roofline 模型区分 prefill 的计算瓶颈和 decode 的内存带宽瓶颈，先建立指标与压测，再比较连续批处理、分页注意力、KV 管理、量化和推测解码等优化。最终以 TTFT、逐 token 延迟、吞吐、队列深度与成本作为权衡证据。

## 价值

- 将散落的推理优化知识收敛为逐步可交付的工程产物。
- 强调先测量后优化，便于避免只凭吞吐或单一 demo 下结论。

## 风险边界

- 是学习路线与外部资料集合，不提供可直接用于生产的托管服务或安全基线。
- “1000+ 并发”等目标依赖模型、GPU、流量形态和版本；不应外推为任意业务的性能承诺。
- 云 GPU、模型权重与日志中均可能包含费用、许可证和数据泄露风险。

## 补充建议

先为实际业务定义 SLO（TTFT、P95、失败率、每请求成本），锁定模型和版本，再复用路线中的基准方法；任何公开 benchmark 都应附带硬件、并发形状、输入/输出长度和完整命令。

## 参考资料

- GitHub：<https://github.com/patchy631/time-to-first-token>
- GitHub API 快照：<https://api.github.com/repos/patchy631/time-to-first-token>
- vLLM：<https://docs.vllm.ai/>
