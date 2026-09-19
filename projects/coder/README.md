<!-- markdownlint-disable MD013 MD034 -->

# coder：面向开发者与 Coding Agent 的自托管云开发环境

> 上游仓库：https://github.com/coder/coder · 归类：Coding Agents 与终端助手 · 本页基于 2026-09-20 的 README、官方文档、release、许可证与 REST API 静态整理；未在本机部署 Coder、创建 workspace 或运行 Coder Agents。

## 定位

`coder/coder` 是用 Terraform 定义和供应云开发环境的自托管控制面，支持把 EC2、Kubernetes Pod、Docker 容器等包装成团队 workspace，并让 Coding Agent 在同一套身份、模型治理、费用与审计框架下执行任务。它不是单个终端助手，而是给开发者和 Agent 提供计算环境、访问入口与治理面的平台。

2026-09-20 的 GitHub 官方综合 Trending 抓取显示约 `+406 stars today`；REST API 快照为 `15,602 stars / 1,521 forks / 1,047 open issues`，API 识别为 AGPL-3.0，最新 release 为 `v2.36.6`（9 月 18 日）。

## 用法

上游为 Linux、macOS 和 Windows 提供安装方式；本地评估可安装 CLI 后启动单机服务：

```sh
curl -L https://coder.com/install.sh | sh
coder server
```

默认可在 `http://localhost:3000` 完成初始用户和 Docker template 配置。生产部署应显式配置 PostgreSQL、外部访问 URL、TLS、身份源、备份与容量；workspace template 使用 Terraform 定义基础设施和开发工具，Agent 则通过 Coder Agents 或 registry module 接入 Claude Code、Codex、OpenCode 等宿主。

## 原理

- `coderd` 作为控制面维护用户、template、workspace、审计、代理连接和生命周期状态。
- Terraform provisioner 把 template 变成 VM、容器或 Kubernetes 资源；空闲关机用于降低长期占用成本。
- workspace agent 与控制面通过加密隧道连接，用户再从浏览器、SSH、VS Code 或 JetBrains 进入环境。
- Coder Agents 的执行循环位于自有基础设施控制面；上游强调模型 API key 不进入 workspace，并为每次动作保留用户身份。
- AI Gateway 统一 provider 认证、费用跟踪和审计；实际 prompt、代码及模型数据流仍取决于所选 provider 与部署配置。

## 价值

- 将“给 Agent 一台机器”升级为可模板化、可回收、带身份和审计的环境供应流程。
- 开发者与 Agent 可复用同一 workspace、IDE、依赖和网络策略，减少本地环境漂移。
- Terraform、Kubernetes、PostgreSQL 与既有身份系统便于纳入企业基础设施治理。
- Agent key 集中在控制面而非散落到 workspace，有利于轮换、费用归属和撤销。

## 风险边界

- workspace、容器或 VM 的存在不自动证明强隔离；host mount、service account、网络出口、元数据服务和集群权限必须单独收窄。
- Coding Agent 仍可在获准 workspace 内改代码、执行命令和访问网络；身份审计不能替代命令审批、secret 最小化和写后验证。
- 快速安装脚本与默认 `*.try.coder.app` 适合评估，不应直接视为生产安全配置。
- 根许可证为 AGPL-3.0，仓库另含 `LICENSE.enterprise` 与付费功能说明；部署、修改和分发前应核对社区版与商业功能边界。
- 集中控制面、PostgreSQL、Terraform state、审计日志和模型网关都可能包含敏感元数据，需要备份、保留、加密与访问治理。
- 本页未验证 `v2.36.6` 的安装、升级、workspace 隔离、隧道、费用归属、审计完整性或故障恢复。

## 补充建议

1. 先在隔离测试账号和单一 Docker template 上跑只读 Coding Agent 任务，记录 workspace、网络、secret 和审计事件。
2. 将 Terraform module、镜像 digest、Agent 版本与模型配置锁定，禁止 Agent 修改供应链基线。
3. 对 IMDS、宿主 socket、集群 service account、内部网段和公网出口分别做 deny-by-default 测试。
4. 在采用前演练 PostgreSQL / Terraform state 备份、Agent 中断、workspace 回收、用户撤销和版本回滚。

## 参考资料

- 上游 README：https://github.com/coder/coder
- `v2.36.6` release：https://github.com/coder/coder/releases/tag/v2.36.6
- Coder Agents 文档：https://coder.com/docs/ai-coder/agents
- AI Gateway 文档：https://coder.com/docs/ai-coder/ai-gateway
- GitHub REST API：https://api.github.com/repos/coder/coder
- LICENSE：https://github.com/coder/coder/blob/main/LICENSE
