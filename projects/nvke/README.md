<!-- markdownlint-disable MD013 -->

# NVKE：在自有 GPU 基础设施上管理 Kubernetes 集群的预览控制面

- 上游：[dsx-ai-factory/nvke](https://github.com/dsx-ai-factory/nvke)；仓库 ID：`1323115536`。
- 快照：2026-11-08（Asia/Shanghai）；stars / forks / open issues（含 PR）：537 / 87 / 182；官方 daily 榜 综合 / Go +125，不是自然日结算。
- 分类：模型、训练与推理基础设施；最新发行：[v0.23.1](https://github.com/dsx-ai-factory/nvke/releases/tag/v0.23.1)（UTC 2026-11-03 23:54:25，非预发行标记）。
- 核读基线：`main@92c39b8ad563ebe5ef705f781b3038b901aba10f`。以下为文档与抽样源码核读，作者声明与本轮运行验证分开。

## 定位

NVIDIA Kubernetes Engine 面向平台团队，在自有机器上建立管理面，并为客户创建独立 control plane、etcd 与 node pool 的 Kubernetes 工作负载集群。它管理 GPU 计算底座的生命周期，不是模型、推理服务或训练调度器。上游明确仍是 Preview，不建议生产使用。

## 用法

先读 local quickstart，使用 Linux 实机 / VM（amd64 或 arm64，至少 6 CPU、12 GiB 可用内存、100 GiB 可用磁盘）、Docker 与虚拟 TPM。macOS 另走 Colima local-site 指南，不能把 Linux 步骤直接当原生 Mac 安装。

源码构建需要当前 go.work 指定的 Go 1.27.3 和 GNU Make 4+，`make build` 只构建二进制，不创建集群。评估环境依次配置 kind 管理集群、Tilt 管理面、CAPNICo 和 mock-NICo；模拟器用容器代替实际机器，不需要 GPU 或 NVIDIA 账号。真实部署还需准备硬件、网络、镜像、注册表和基础设施接口。

## 原理

临时 seed 集群引导管理集群；管理面通过 Cluster API、基础设施 provider 和节点 agent 驱动工作负载集群。节点借 TPM 与 SPIFFE / SPIRE 建立身份后取得 join 凭据。配套 NVKR 负责按固定输入构建制品，NVKE 负责部署与运行生命周期；制品可构建、可引导与真实硬件验证是不同阶段。

## 价值

适合希望向多个团队提供 Kubernetes 服务的 GPU 平台研究：可跟踪集群、节点池、证书与可选 etcd 加密，避免把单一共享集群当所有租户的唯一控制面。独立集群有管理价值，但不能据此直接声称 GPU、网络、存储与管理面都已实现安全隔离。

## 风险边界

- 安装后 API 默认在管理节点 NodePort 30080 提供 HTTP，认证关闭。文档的 permissive 模式只检查 / 计数，不拒绝；需部署自己的 TLS 入口并切换 enforcing。
- 当前访问文档明确：被认证接纳的调用方仍可调用全部端点；v0.23.0 引入授权库基础，不等于所有产品路径已有细粒度授权。
- 客户拿到的 admin kubeconfig 无单独撤销路径，证书到期前有效；客户须在集群内另建更窄权限。
- 管理集群不自升级 / 自扩缩 / 自替换，尚无管理面升级和备份恢复流程；FDE 镜像仅用于评估，不提供静态数据保密性。
- README 写预览仅兼容 NICo，限制页又写部署启用后支持 LaunchLayer，存在文档口径差异。按固定版本与目标 provider 核验，不自行推断两者功能等价。
- 根许可 Apache-2.0，制品和依赖另核；本轮未构建、引导节点、申请硬件或测试身份 / 租户隔离。

## 补充建议

先在一次性环境验证创建、节点 Ready、删除和失败恢复，再记录真实部署的镜像 digest、provider、TLS / OIDC、备份责任与退出方案。把控制面访问、租户工作负载和硬件供应路径分别验收。v0.23.1 包含 tenant kubeconfig 解析 allowlist 修复；升级判断应核对目标 release 的完整变更与依赖清单。

## 参考资料

- [README.md](https://github.com/dsx-ai-factory/nvke/blob/92c39b8ad563ebe5ef705f781b3038b901aba10f/README.md)
- [docs/get-started/quickstart-local.md](https://github.com/dsx-ai-factory/nvke/blob/92c39b8ad563ebe5ef705f781b3038b901aba10f/docs/get-started/quickstart-local.md)
- [docs/overview/preview-status.md](https://github.com/dsx-ai-factory/nvke/blob/92c39b8ad563ebe5ef705f781b3038b901aba10f/docs/overview/preview-status.md)
- [docs/operate/api-authentication.md](https://github.com/dsx-ai-factory/nvke/blob/92c39b8ad563ebe5ef705f781b3038b901aba10f/docs/operate/api-authentication.md)
- [LICENSE](https://github.com/dsx-ai-factory/nvke/blob/92c39b8ad563ebe5ef705f781b3038b901aba10f/LICENSE)
- [GitHub API 快照](https://api.github.com/repos/dsx-ai-factory/nvke)；[发行列表](https://github.com/dsx-ai-factory/nvke/releases)。
- [v0.23.0 授权库与凭据生命周期变更](https://github.com/dsx-ai-factory/nvke/releases/tag/v0.23.0)。
