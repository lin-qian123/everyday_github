<!-- markdownlint-disable MD013 MD034 -->

# ArcBox：以独立内核 microVM 承载 AI agent 与不可信代码

## 项目概览

- 上游仓库：https://github.com/arcboxlabs/arcbox
- GitHub API 快照（2026-09-03）：2,346 stars、58 forks、42 个开放 issue
- 当前 release：`v0.7.0`
- 主要技术：Rust VMM、Firecracker microVM、VirtIO、Docker-compatible engine、macOS / Apple Silicon
- 许可证：MIT OR Apache-2.0

## 定位

ArcBox 同时提供 macOS 上的 Docker Desktop / OrbStack 替代方案、Linux machines，以及面向 AI agents 和不可信代码的一次性 microVM sandbox。其 sandbox 使用独立内核、文件系统和网络，而不是只依赖 agent 自己的权限提示。

它目前明显偏向 macOS / Apple Silicon；agent sandbox 还要求 M3 或更新芯片、macOS 15+ 和默认 Virtualization.framework 后端。

## 用法

上游提供 Homebrew cask 与远程安装脚本。Docker 兼容模式和 agent sandbox 是不同路径：

```bash
brew install --cask arcboxlabs/tap/arcbox
abctl docker enable
docker run -d -p 8080:80 nginx

abctl sandbox create --from-image myapp:latest --memory 512 --ttl 3600
abctl sandbox run <id> -- ./untrusted-binary
```

`abctl claude` 会在 microVM 中运行 agent，并关闭 agent 自身的权限提示，因为上游把 microVM 视为隔离边界。采用这一模式前必须先验证网络、文件复制、端口暴露和凭据注入策略。

## 原理

ArcBox 自行实现 VMM、VirtIO 设备、文件共享与网络数据面；容器由 guest `dockerd` 提供 Docker-compatible socket。agent sandbox 则在 guest 内通过 nested Firecracker 启动独立 microVM，默认不把主机目录挂入 `/workspace`。

系统支持从镜像或模板创建 sandbox、执行命令、复制文件、暴露端口、checkpoint 和 restore。隔离强度取决于 VMM、nested virtualization、镜像、网络策略以及管理 daemon 的安全性。

## 价值

- 将 agent 与主机从共享进程/容器边界提升到独立内核 microVM。
- 本地 sandbox 与云端 fleet 使用相近原语，便于复用生命周期 API。
- 支持 TTL、snapshot、文件复制和端口暴露，适合可重建 CI / agent 任务。
- 同时提供 Docker / Kubernetes / machine 管理，减少本机多套虚拟化工具叠加。

## 风险边界

- microVM 显著增强隔离，但不能消除 VMM、内核、镜像、网络和管理面漏洞。
- 关闭 agent 权限提示只在外层 policy 足够严格时成立；开放网络和凭据仍可造成真实外部副作用。
- M3+/macOS 15+ 限制意味着 sandbox 结论不能外推到旧 Mac、Linux 或非默认后端。
- Docker 迁移、kubeconfig 切换、socket/context 和卷数据会影响现有开发环境，必须先 dry-run 与备份。
- README 中的启动时间和吞吐数据是上游基准，不是本轮独立复现结果。
- 本页仅核对上游 README、站点、release 与 API，未安装、迁移或进行逃逸测试。

## 补充建议

1. 在空白 M3+ 测试机固定 `v0.7.0`，从无网络、无凭据、无主机挂载的 sandbox 开始。
2. 用恶意依赖、fork bomb、端口扫描、metadata 访问和 symlink 路径构造对抗回归。
3. 对 `sandbox cp`、`expose`、snapshot、restore 和 TTL 逐项验证授权、审计与残留数据。
4. 迁移 Docker Desktop / OrbStack 前导出镜像和卷，先跑 `--dry-run`，记录 context 与 kubeconfig 变化。
5. 不因关闭内层权限提示而取消外层审批；真实发帖、部署、支付和凭据动作仍需人工闸门。

## 参考资料

- 仓库与 README：https://github.com/arcboxlabs/arcbox
- Releases：https://github.com/arcboxlabs/arcbox/releases
- 官方站点：https://arcbox.dev/
- Agent sandbox 文档：https://github.com/arcboxlabs/arcbox/blob/master/docs/agent-sandbox.md
- Sandbox API：https://github.com/arcboxlabs/arcbox/blob/master/docs/sandbox-api.md
