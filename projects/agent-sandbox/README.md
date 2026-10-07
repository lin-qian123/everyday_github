<!-- markdownlint-disable MD013 -->

# agent-sandbox（kubernetes-sigs/agent-sandbox）

> 上游仓库：<https://github.com/kubernetes-sigs/agent-sandbox> · 归类：Agent 框架与技能生态 · 本页基于 2026-10-08 的 GitHub API、README、CRD / configuration / runtime 文档与源码静态整理，未部署 Kubernetes 集群、gVisor、Kata 或 Firecracker workload。

- 抓取快照：4,180 stars、549 forks、184 open issues。
- 热度信号：GitHub Go Trending 抓取时约 +19 当日 stars；最后 push 为 2026-10-07。
- 版本与许可：最新 Release `v1.0.5`，Apache-2.0；本页固定审计 commit `42679cc4bd42`。

## 定位

agent-sandbox 是 Kubernetes SIGs 的有状态 singleton workload 控制器，面向 Coding Agent、computer-use、RL rollout 等需要“每个任务一个长期环境”的场景。它用 Sandbox、Template、Claim 与 WarmPool CRD 统一创建、挂起、恢复、过期和复用 Pod，而不是在 Kubernetes 之外发明新的调度系统。

## 用法

在测试集群安装 controller / CRD 后，以 Sandbox 或 SandboxTemplate 声明 Pod template、volume、service、runtimeClass 和 lifecycle，再由 Claim 获取 cold 或 warm sandbox。安全试用应显式设置非 root、只读 filesystem、资源限额、NetworkPolicy、最小 service account、shutdownTime，并选择 gVisor / Kata 等符合威胁模型的 runtimeClass。

## 原理

controller 将 Sandbox reconcile 为 Pod、可选 headless Service 与 PVC；extensions 提供 template、warm pool 和 claim，降低大量 Agent 冷启动延迟。`operatingMode` 在 Running / Suspended 间切换，volume 保留状态；`shutdownTime` 与 policy 负责到期清理。隔离强度由底层 runtime 决定：runc 是 namespace / cgroup，gVisor 是用户态内核拦截，Kata / Firecracker 路线才接近每 Pod VM。

## 价值

它把有状态 Agent 环境从自定义脚本提升为 Kubernetes 原生声明式资源，可复用 RBAC、quota、scheduler、PVC、metrics 和 lifecycle。WarmPool 与 Claim 兼顾启动延迟和独占状态，适合评测、交互式 coding 与弹性 worker 平台统一运维。

## 风险边界

- 名称叫 sandbox 不代表强隔离；默认 runc 仍共享宿主内核，恶意 / 不可信代码需要 gVisor、Kata、专用节点或更强外部边界。
- controller 负责生命周期，不自动提供 egress allowlist、secret 隔离、镜像可信、Pod Security、tenant quota 或运行时漏洞修复。
- Pod template 可以挂载 token、PVC、host capability 和网络；错误 RBAC / admission 配置会让 Agent 获得集群或跨租户权限。
- WarmPool 会保留预启动环境；claim adoption、volume、镜像层和后台进程必须验证没有前一租户残留或 secret 污染。
- `shutdownTime` 未设置时 sandbox 可无限存在；Retain 仅保留 CR 对象但会删 Pod / Service，不能代替数据保留与取证策略。
- RuntimeClass 跨 gVisor / Kata 的 CI 与性能文档仍含 proposal / 非生产测量；不能把方向性延迟数字当本集群 SLA。

## 补充建议

用两个恶意测试租户做文件、网络、Kubernetes API、PVC、warm reuse 和节点 escape 对抗验证；默认关闭 automount service-account token，设置 NetworkPolicy、seccomp、capability drop、ephemeral limit 与 TTL。对 controller、runtime、node image、CRD 版本和 cleanup event 建立独立审计与故障恢复演练。

## 参考资料

- [GitHub 仓库](https://github.com/kubernetes-sigs/agent-sandbox)
- [GitHub REST API](https://api.github.com/repos/kubernetes-sigs/agent-sandbox)
- [配置说明](https://github.com/kubernetes-sigs/agent-sandbox/blob/main/docs/configuration.md)
- [API 参考](https://github.com/kubernetes-sigs/agent-sandbox/blob/main/docs/api.md)
- [性能调优](https://github.com/kubernetes-sigs/agent-sandbox/blob/main/docs/performance-tuning.md)
- [Runtime-aware CI proposal](https://github.com/kubernetes-sigs/agent-sandbox/blob/main/docs/kata-ci-proposal.md)
- [安全策略](https://github.com/kubernetes-sigs/agent-sandbox/blob/main/SECURITY.md)
- [v1.0.5 Release](https://github.com/kubernetes-sigs/agent-sandbox/releases/tag/v1.0.5)
