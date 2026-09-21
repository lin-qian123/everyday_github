<!-- markdownlint-disable MD013 MD034 -->

# substrate：面向高密度有状态 Agent 的 Kubernetes 执行底座

> 上游仓库：https://github.com/agent-substrate/substrate · 归类：Agent 框架与技能生态 · 本页基于 2026-09-22 的 README、架构 / threat model、benchmark 文档、release、许可证与 REST API 静态整理；未创建集群、运行 sandbox 或复现性能数字。

## 定位

`agent-substrate/substrate` 不是构建 Agent 的 SDK，而是把大量长期存在、经常空闲的 Agent / 工具服务映射到较少 worker 上的执行 runtime。它借助 Kubernetes 管理基础设施，以 gVisor 或 microVM 承载 actor，并围绕创建、暂停、恢复、快照和流量路由补齐 Agent workload 的生命周期。

2026-09-22 的 GitHub 官方 Go Trending 抓取显示约 `+438 stars today`；REST API 快照为 `2,595 stars / 357 forks / 521 open issues`，Apache-2.0，最新 release 为 `v0.1.0`（9 月 10 日）。README 明确标为 early development、API 很可能变化，且不是 Google 官方支持产品。

## 用法

开发 quickstart 需要 Go、Docker、`kubectl`，并用 `kind` 建本地集群：

```sh
./hack/create-kind-cluster.sh
./hack/install-ate-kind.sh --deploy-ate-system
./hack/install-ate-kind.sh --deploy-demo-counter
go install ./cmd/kubectl-ate
kubectl ate create actor my-counter-1 -a ate-demo-counter --template counter
kubectl port-forward -n ate-system svc/atenet-router 8000:80
```

这是一套会创建集群、registry、PostgreSQL / object storage 与控制面的开发部署，不应直接在生产集群照抄。先在隔离项目中跑 Counter Demo，再评估 GKE、Cloud SQL、IAM 与持久快照路径。

## 原理

- `ActorTemplate` 描述 workload，actor 保存身份和状态，worker pool 提供可复用的物理执行槽位。
- `ate-api-server`、controller、node-level `atelet` 与 `atenet` 分别负责控制面、调度、快照 / 恢复和 Envoy 路由。
- actor 暂停时把内存与文件系统写入快照，恢复时可被“传送”到任意合适 worker；流量路由随分配关系更新。
- worker 内部由 gVisor 或 microVM 提供隔离；Kubernetes 仍负责 Pod、node、autoscaling 和底层资源供应。
- 上游 Demo 展示约 250 个 stateful actors 复用 8 个物理 pods；README 的 sub-500 ms、500+ activations/s 和 10x density 是项目自报目标 / 结果，需按公开 benchmark harness 独立复现。

## 价值

- 把 idle-heavy Agent 的状态保留与物理资源解耦，可能降低大规模 coding sandbox、MCP server 和 RL rollout 的常驻成本。
- 同一 actor lifecycle 可跨 gVisor / microVM，便于把 framework-specific harness 与基础设施分层。
- request parking、durable directory、autoscaled worker pool 与 Claude Code multiplex demo 提供了可追踪的验证入口。
- threat model、authentication、egress、observability 与 upgrade runbook 已进入仓库，便于审计问题而不是只看性能口号。

## 风险边界

- 上游 threat model 明写当前实现“little to no security hardening”；`secure-by-default` 愿景不能替代当前版本的对抗验证。
- worker 复用、snapshot storage、network policy、secret 注入、control / data plane 共置和 ActorTemplate 权限都可能形成跨租户逃逸或数据残留路径。
- gVisor / microVM 是隔离组件，不会自动限制 egress、工具业务权限、云 IAM 或存入快照的凭据。
- 521 个 open issues、`v0.1.0` 与不承诺兼容意味着升级、恢复和故障回滚接口仍高度动态。
- 本页未复现吞吐、恢复延迟、30x oversubscription 或故障场景，不能据 Demo 推断目标集群成本与安全性。

## 补充建议

1. 先用无凭据 Counter / Sandbox demo 复现 cold start、resume、worker reuse 和 snapshot corruption 场景。
2. 将 control plane、gateway、worker node 分离，并对 actor ingress / egress、Kubernetes API 与 object storage 默认拒绝。
3. 对每次 suspend / resume 枚举进程、文件、环境变量、mount、网络与策略状态，专门测试前一 actor 残留。
4. 固定 commit 与集群版本，用仓库 Locust harness 记录 P50 / P95 / P99、失败率、快照体积和真实成本。

## 参考资料

- 上游 README：https://github.com/agent-substrate/substrate
- 架构：https://github.com/agent-substrate/substrate/blob/main/docs/architecture.md
- Threat model：https://github.com/agent-substrate/substrate/blob/main/docs/threat-model.md
- Benchmarking：https://github.com/agent-substrate/substrate/blob/main/benchmarking/README.md
- `v0.1.0` release：https://github.com/agent-substrate/substrate/releases/tag/v0.1.0
- GitHub REST API：https://api.github.com/repos/agent-substrate/substrate
- LICENSE：https://github.com/agent-substrate/substrate/blob/main/LICENSE
