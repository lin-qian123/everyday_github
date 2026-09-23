<!-- markdownlint-disable MD013 -->

# microsandbox（superradcompany/microsandbox）

- GitHub：<https://github.com/superradcompany/microsandbox>
- 抓取快照：2026-09-24，8,400 stars、449 forks、89 open issues
- 热度信号：GitHub Rust Trending 抓取时约 +15 当日 stars
- 版本与许可：Apache-2.0；latest GitHub Release 为 `v0.7.2`

## 定位

Microsandbox 是在本机运行不可信 workload 的 branchable microVM runtime，面向 AI Agent、用户代码、插件、CI、浏览器自动化和开发环境。它提供 CLI 以及 TypeScript、Rust、Python、Ruby、Go SDK，并可运行 OCI image、snapshot / restore、live branch、network allowlist 与 secret proxy。

## 用法

macOS 需 Apple Silicon，Linux 需 KVM，Windows 需 WHP。安装 `msb` 后可用 `msb run` 临时执行，或 create / exec / branch / snap 管理具名 sandbox；SDK 以子进程方式启动 microVM，不要求常驻服务。Agent 可另装上游 skills 或 MCP server，但生命周期、filesystem、volume、network 和 monitoring 权限需单独收窄。

## 原理

CLI / SDK 将 launch config 交给 host runtime，runtime 通过 platform VMM 启动独立 guest kernel，并以版本化 host--guest protocol、control socket / named pipe 和 durable SQLite / disk / snapshot 状态管理生命周期。OCI layer 物化为 root disk；live control 支持资源和 secret 更新；branch / snapshot 复制或恢复运行状态。

## 价值

相较同 host kernel 的普通容器，microVM 为高权限 Agent、生成代码和不可信文档提供更强隔离边界；本地子进程模型又比先搭远端 sandbox control plane 更轻。OCI、SDK、network allowlist、snapshot / branch 适合构建可重复、可回滚的 Agent worker。

## 风险边界

- README 明确项目仍是 beta；breaking changes、缺失功能、兼容矩阵和历史 runtime / snapshot 协议需要随 Release 验证。
- microVM 不是自动安全策略：挂载 host volume、放宽网络、转发 secret、运行高权限 MCP 或使用未审计 image 都可重新扩大攻击面。
- “under 100 ms boot”“secrets that can't leak”等是上游主张，本轮未做逃逸、侧信道、网络、snapshot 或恶意 guest 对抗测试。
- 安装页提供 `curl | sh` / PowerShell pipe，生产环境应改用固定 Release、hash / signature 验证和内部镜像。
- macOS、Linux、Windows 使用不同虚拟化与进程 / disk lock 路径；某一平台通过不代表跨平台隔离、恢复与兼容性等价。

## 补充建议

先用无生产凭据的恶意样例验证 host filesystem、network deny、secret proxy、resource exhaustion、snapshot 恢复和 teardown；固定 `v0.7.2`、OCI digest 与 guest image SBOM。把 sandbox policy 与 Agent tool policy 分开：即使 guest 隔离通过，也要限制 MCP、volume、egress 和回传内容。

## 参考资料

- [GitHub 仓库](https://github.com/superradcompany/microsandbox)
- [GitHub REST API](https://api.github.com/repos/superradcompany/microsandbox)
- [v0.7.2 Release](https://github.com/superradcompany/microsandbox/releases/tag/v0.7.2)
- [官方文档](https://docs.microsandbox.dev)
- [Compatibility Map](https://github.com/superradcompany/microsandbox/blob/main/COMPATIBILITY.md)
- [Security Policy](https://github.com/superradcompany/microsandbox/blob/main/SECURITY.md)
- [LICENSE](https://github.com/superradcompany/microsandbox/blob/main/LICENSE)
