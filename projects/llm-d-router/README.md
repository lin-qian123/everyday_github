<!-- markdownlint-disable MD013 -->

# llm-d Router（llm-d/llm-d-router）

> 上游仓库：<https://github.com/llm-d/llm-d-router> · 归类：模型、训练与推理基础设施 · 本页基于 2026-10-09 的 GitHub API、README、architecture、operations、TLS、release verification 与 Helm 文档静态整理，未部署 Kubernetes / Envoy、模型 server 或复测路由指标。

- 抓取快照：382 stars、424 forks、312 open issues。
- 热度信号：GitHub Go Trending 抓取时约 +4 当日 stars；最后 push 为 2026-10-08。
- 版本与许可：最新 Release / tag `v0.11.0`，Apache-2.0；本页固定审计 commit `ce60ef78d220`。

## 定位

llm-d Router 是 Kubernetes / Envoy 推理数据面的智能入口，前身名称为 Inference Scheduler。它用 Endpoint Picker（EPP）根据 KV-cache locality、负载、priority 和 request objective 选择模型 endpoint，并支持 model rewrite、排队、Standalone / Gateway mode 与 encode / prefill / decode 分离式 serving。

## 用法

本地评估可用 Standalone Helm chart，让自管 Envoy 与 EPP 以 sidecar 或独立 service 运行；生产推荐 Gateway API 的 InferencePool + HTTPRoute。部署前固定 chart / image digest，验证 provenance / SBOM，启用 serving 与 metrics TLS，配置 namespace、RBAC、resource request / limit、queue 与 objective，再以自有长短 context 混合负载对比最简单的 round-robin / least-load 基线。

## 原理

Envoy 或兼容 L7 proxy 经 `ext-proc` 将请求信号交给 EPP；scorer / filter 组合 cache、load、priority 等状态选择 backend。InferenceObjective 表达 scheduling goal，InferenceModelRewrite 支撑模型名重写与 canary；disaggregation sidecar 协调 encode / prefill / decode worker 和 KV / embedding transfer，Gateway API 承载入口与多集群流量管理。

## 价值

在大模型 serving 中，KV-cache locality 和不同阶段负载会让普通负载均衡产生重复 prefill、排队和尾延迟。llm-d Router 将这些信号放入可扩展 EPP，并复用 Kubernetes Gateway / Envoy 生态，适合在多副本、长 context 和分离式推理中做可观测的策略实验。

## 风险边界

- 智能 routing 的收益依赖模型、cache、请求长度、并发、proxy 和 scorer；不能把上游架构目标直接写成自身吞吐或延迟提升。
- EPP 位于全部推理流量路径，错误 objective、model rewrite、queue 或 ext-proc failure 会造成错模型、饥饿、放大尾延迟或全局中断。
- Full-duplex body streaming、TLS、metrics、OpenTelemetry 日志与 proxy 配置可能暴露 prompt、模型名、tenant、priority 和容量信息。
- Gateway、InferencePool、CRD 与 repo consolidation 正在演进；API / chart / image 版本漂移会影响升级和回滚。
- signed provenance 与 SBOM 证明发布链中的特定事实，不证明镜像无漏洞、运行配置安全或第三方 dependency 行为正确。
- stars 低于 forks 且 open issues 较多是当前快照，不应单独解读为质量结论；本轮未运行 benchmark 或 failure injection。

## 补充建议

为每个 model / SLO 建固定 workload，记录 TTFT、TPOT、吞吐、cache hit、queue、公平性和错误率，并与静态路由比较。对 EPP crash、proxy timeout、stale cache、worker churn、超长 request、恶意 priority 和错误 rewrite 做故障注入；升级前核验镜像 provenance / SBOM、CRD diff 与回滚路径。

## 参考资料

- [GitHub 仓库](https://github.com/llm-d/llm-d-router)
- [GitHub REST API](https://api.github.com/repos/llm-d/llm-d-router)
- [README 与架构图](https://github.com/llm-d/llm-d-router/blob/main/README.md)
- [Architecture](https://github.com/llm-d/llm-d-router/blob/main/docs/architecture.md)
- [Operations / sizing](https://github.com/llm-d/llm-d-router/blob/main/docs/operations.md)
- [TLS](https://github.com/llm-d/llm-d-router/blob/main/docs/tls.md)
- [验证发布制品](https://github.com/llm-d/llm-d-router/blob/main/docs/verifying-releases.md)
- [v0.11.0 Release](https://github.com/llm-d/llm-d-router/releases/tag/v0.11.0)
