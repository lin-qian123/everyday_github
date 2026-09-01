<!-- markdownlint-disable MD013 MD034 -->

# OpenShell：在基础设施层约束自主 AI agents 的隔离运行时

## 项目概览

- 上游仓库：https://github.com/NVIDIA/OpenShell
- GitHub API 快照（2026-09-02）：8,475 stars、1,251 forks、549 个开放 issue
- 当前 release：`v0.0.116`
- 主要技术：Rust / Python CLI、gateway、container / MicroVM / Kubernetes、声明式策略与推理路由
- 许可证：Apache-2.0

## 定位

OpenShell 是 NVIDIA 开源的 agent runtime。它把 coding agent、研究 agent 或长期 autonomous agent 放进独立 sandbox，并在 agent 进程之外控制文件系统、网络、进程和模型推理流量。

它解决的是运行时约束，不是模型事实性、任务规划或业务审批。官方资料曾将其描述为 early preview；`v0.0.x` release 和大量开放 issue 也提示接口与平台支持仍在快速演进。

## 用法

上游快速入口会执行远程安装脚本：

```bash
curl -LsSf https://raw.githubusercontent.com/NVIDIA/OpenShell/main/install.sh | sh
openshell sandbox create -- codex
```

创建 sandbox 后，可以用 `openshell policy set` 应用 YAML 策略、用 `provider create` 注入凭据、用 `logs` 和 `term` 观察运行状态。生产试用前应先下载并审查安装脚本、固定 release / commit，并在专用测试主机上运行官方策略演示。

## 原理

OpenShell 的 gateway 管理 sandbox 生命周期并形成认证边界；sandbox 承载 agent；policy engine 拦截文件、网络和进程行为；privacy router 可把推理请求送到受控后端。出站连接按“允许、推理路由、拒绝并记录”三类处理。

文件系统与进程策略在 sandbox 创建时锁定，网络和推理策略可热更新。凭据由 provider 注入运行环境，不写入 sandbox 文件系统；实际隔离强度仍取决于 Docker、Podman、MicroVM 或 Kubernetes 后端及主机配置。

## 价值

- 把 agent 安全边界从提示词移到 agent 难以自行修改的基础设施层。
- 用声明式策略统一管理文件、进程、网络和推理出口。
- 支持 Claude Code、Codex、OpenCode、Copilot CLI 等现有 agent，减少应用改造。
- gateway、日志和 TUI 为权限变更、允许/拒绝决策和故障提供观察面。

## 风险边界

- container 不自动等于强 VM 隔离；内核、runtime、挂载、特权模式和设备透传都会改变威胁模型。
- 错误或过宽的策略、镜像、provider 与 community sandbox 仍可能泄露凭据或允许数据外传。
- 凭据不落盘不能消除运行时窃取、日志泄露、被授权 API 滥用和供应链风险。
- GPU passthrough 标为 experimental；驱动、CDI、镜像库和多租户隔离需独立验证。
- 安装脚本会改动本机环境，gateway 是高价值控制面；升级、回滚、审计与恢复必须测试。
- 本页依据上游 README、官方文档、官方博客与 API，未安装，也未进行逃逸、策略绕过或多租户安全测试。

## 补充建议

1. 固定 `v0.0.116` 和安装脚本哈希，在可重建测试主机上验证安装、卸载与回滚。
2. 从 deny-by-default 开始，用最小只读 GitHub API 场景逐项放开文件、binary、destination、method 和 path。
3. 分别测试 Docker 与 MicroVM 后端的挂载、内核、网络、设备和多租户边界，不混用安全结论。
4. 将策略变更、provider 使用、日志导出和 sandbox 镜像纳入代码审查与供应链签名。
5. 用恶意 prompt、被污染 skill、依赖安装和凭据滥用样本做回归，并保留人工批准和紧急停止通道。

## 参考资料

- 仓库与 README：https://github.com/NVIDIA/OpenShell
- 官方文档：https://docs.nvidia.com/openshell/latest/
- Releases：https://github.com/NVIDIA/OpenShell/releases
- 官方安全设计博客：https://blogs.nvidia.com/blog/secure-autonomous-ai-agents-openshell/
- 架构资料：https://github.com/NVIDIA/OpenShell/tree/main/architecture
- 安全实践：https://docs.nvidia.com/openshell/latest/security/best-practices
- 官方策略演示：https://github.com/NVIDIA/OpenShell/tree/main/examples/sandbox-policy-quickstart
