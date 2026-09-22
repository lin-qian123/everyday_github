<!-- markdownlint-disable MD013 -->

# nasiko（Nasiko-Labs/nasiko）

- GitHub：<https://github.com/Nasiko-Labs/nasiko>
- 抓取快照：2026-09-23，7,618 stars、1,636 forks、58 open issues
- 热度信号：GitHub Rust Trending 抓取时约 +734 当日 stars
- 版本与许可：API 为 `NOASSERTION`、根 LICENSE 为 Apache-2.0；最新 GitHub Release `v1.0.0`，workspace manifest 为 `0.1.0`

## 定位

Nasiko 是多 Agent 的自托管控制面，把 A2A 代理、MCP gateway、LLM router、OCI registry、flow guard、secret、成本与 OpenTelemetry trace 放入一个服务入口。它也能给 Claude Code、Codex、Cursor CLI 和 OpenCode 安装 session reporting hook，或把模型请求路由到集中配置的 provider。

## 用法

Docker 路径启动 Postgres、Redis、RustFS、OTel Collector、Tempo、Loki 和 nasiko-server；至少要替换默认管理员密码并设置加密 / JWT key。CLI 可 scaffold、build、push、deploy、chat、管理 secret / MCP / registry。Coding-agent 集成会修改用户级配置或安装 hook，并把完成 turn 排队上传到控制面；应先在专用系统用户和测试 Agent 上试用。

## 原理

所有 Agent-to-Agent 流量经单一控制面代理，入口执行 TLS、认证、用户 / Agent ACL、allowlist、速率与 flow budget。三段式 router 先按 embedding shortlist，再按会话 rerank，最后让 LLM 选择 Agent。MCP 和 LLM gateway 在服务端持有真实凭据，向 Agent 发短期身份 token；持久状态落入 Postgres、Redis、S3，Agent 以 Docker 容器运行。

## 价值

当 Agent 数量增加后，路由、凭据、循环、成本、版本和失败排查会迅速变成运维问题。Nasiko 给这些问题一个可观测、可限额、跨语言 A2A 的集中入口，并提供从本地开发到镜像部署的完整操作面。

## 风险边界

- 单一控制面也是单一高价值故障 / 攻击面；TLS、ACL、secret encryption、短期 token 和 trace 的实现仍需对抗验证。
- Docker 容器、flow guard 和 A2A proxy 不等于强多租户沙箱；恶意镜像、宿主挂载、网络出口和 registry 供应链需另行隔离。
- Coding-agent hook 会把 turn / session 数据送到控制面，LLM router 会改用户级全局配置；这会影响同机其他项目与敏感会话。
- 默认 `admin/changeme` 只适合初次本地启动，生产环境必须在暴露端口前替换全部默认 secret 和地址。
- Release `v1.0.0`、workspace `0.1.0` 和 README 功能面存在版本语义漂移，不能仅凭标签推断稳定性。

## 补充建议

在隔离主机用合成 Agent 建立四组测试：跨租户 ACL、恶意 / 递归 A2A、secret / log 泄漏、控制面与 Redis / S3 故障。为 hook 和模型路由保留自动卸载 / 回滚检查；外部暴露前固定镜像 digest、最小网络策略、OIDC 和独立管理员账户，并审计 trace 中的 prompt / tool 数据。

## 参考资料

- [GitHub 仓库](https://github.com/Nasiko-Labs/nasiko)
- [GitHub REST API](https://api.github.com/repos/Nasiko-Labs/nasiko)
- [官方文档](https://docs.nasiko.com)
- [A2A 协议说明](https://github.com/Nasiko-Labs/nasiko/blob/main/docs/A2A_PROTOCOL.md)
- [v1.0.0 Release](https://github.com/Nasiko-Labs/nasiko/releases/tag/v1.0.0)
- [LICENSE](https://github.com/Nasiko-Labs/nasiko/blob/main/LICENSE)
