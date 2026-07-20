<!-- markdownlint-disable MD013 -->

# fabrica

## 定位

`fabrica` 是面向 AI agents 的隔离执行环境基础设施，用 Kubernetes、Kata Containers 和 Cloud Hypervisor 提供 ephemeral、forkable、可配额管理的 Agent Computers。它服务的是 agent 运行时安全边界，而不是模型或应用层。

## 今日信号

- GitHub：<https://github.com/mitkox/fabrica>
- 创建时间：2026-07-19。
- 抓取时约 35 stars、7 forks。
- 语言 / 许可证：Go，Apache-2.0。

## 用法

部署侧需要 Linux KVM、Kubernetes、Kata Containers / Cloud Hypervisor。开发者可以构建 sandbox-manager，使用 Helm chart 部署 dev / production profile，通过 REST API 创建、执行、快照和回收 sandbox。项目 README 声称 core control plane 已有较完整测试，runtime 层需要真实 KVM host 验证。

## 原理

每个 agent sandbox 是一个 microVM，具备独立 CPU、内存、存储、网络策略、TTL 生命周期和 workspace CoW clone。控制面负责 API、SQLite 持久化、reconciliation、quota、overlayfs 工作区、Prometheus metrics 和 OpenTelemetry tracing。底层 runtime 依赖 containerd + Kata + Cloud Hypervisor。

## 价值

- 将 agent 执行环境从普通容器推进到 microVM 隔离，对不可信代码执行更有现实意义。
- 适合为 coding agents、security agents、CI repair agents 提供可销毁工作空间。
- 与 `clawk`、`tupper`、`OpenSandbox` 等项目共同说明“agent sandbox”正在成为独立基础设施层。

## 风险边界

- 部署复杂度高，需要 KVM、Kubernetes 和 Kata runtime；不适合轻量个人桌面场景。
- README 中的 production-ready 主要指 control plane core，warm pool 和大规模 runtime 仍需更多真实集群验证。
- microVM 隔离降低风险，但网络策略、镜像供应链、host kernel 和凭据注入仍需要独立审计。

## 补充建议

- 后续跟踪其 Helm chart、runtime smoke tests 和 100+ sandbox 压测在真实 KVM 集群中的结果。
- 可与 `clawk`、`tupper`、`daytona` 做对照：fabrica 更偏 Kubernetes / microVM 多租户平台。
- 试用时先采用 isolated network profile，并将模型凭据通过最小权限 secret 注入。

## 参考资料

- GitHub 仓库：<https://github.com/mitkox/fabrica>
- README：<https://github.com/mitkox/fabrica#readme>
- Kata Containers：<https://katacontainers.io/>
- Cloud Hypervisor：<https://www.cloudhypervisor.org/>
