<!-- markdownlint-disable MD013 -->

# Docker Agent（docker/docker-agent）

> 上游仓库：<https://github.com/docker/docker-agent> · 归类：Agent 框架与技能生态 · 本页基于 2026-10-09 的 GitHub API、README、permissions、sandbox、secrets 与 telemetry 文档静态整理，未连接模型、MCP server、OCI registry 或 Docker Sandbox。

- 抓取快照：4,229 stars、494 forks、45 open issues。
- 热度信号：GitHub Go Trending 抓取时约 +628 当日 stars；最后 push 为 2026-10-08。
- 版本与许可：最新 Release / tag `v1.149.0`，Apache-2.0；本页固定审计 commit `154b78f2d517`。

## 定位

Docker Agent 是 Docker Engineering 的声明式 Agent builder / runtime，也是 Docker CLI plugin。用户以 YAML 定义模型、指令、工具、MCP、RAG、多 Agent 协作、权限与评估，并可把配置打包到 OCI registry，在 CLI、TUI、API、ACP / A2A 或 sandbox 入口运行。

## 用法

Docker Desktop 4.63+ 可直接运行 `docker agent`，也可用 Homebrew 或二进制安装。安全试用先用本地模型或低额度测试 key，建立最小 YAML，只启用只读工具；显式传 `--safety strict` 或 `restricted`，对第三方配置固定 digest，并在需要不可信代码时加 `--sandbox`。secret 优先使用 Compose secret、credential helper 或短期环境变量，不把值写入 YAML。

## 原理

Go runtime 解析 Agent / model / toolset / workflow 配置，按 safety mode 和 deny / allow / ask 规则门控 tool call，再连接内建工具或本地、远端、Docker 化 MCP。OCI 负责分发配置，session、memory、RAG 和 tracing 支撑长流程；sandbox 模式本身只编排 Docker Sandboxes，真实 VM、mount 与网络隔离由所选 `sbx` / `docker sandbox` 后端实现。

## 价值

它把多 provider、MCP、multi-agent、RAG、eval、session 与分发压到一个可版本化入口，适合用相同配置在开发机、CI 和团队 registry 间复现。权限模式、secret provider、OpenTelemetry 和 sandbox integration 也比散装脚本更容易形成统一运行基线。

## 风险边界

- `autonomous` 会允许所有未被 deny / hook 拦截的调用；第三方 YAML 甚至可声明默认 autonomous，必须由用户级 setting 或 CLI 固定下限。
- `restricted` 是工具调用防御，不是安全边界；不可信代码仍应使用 sandbox，且工作目录会以读写 mount 暴露给 VM 内 Agent。
- MCP、shell、model provider、OCI config 与 credential helper 共同形成供应链；签名、digest、tool schema 和 endpoint 必须分别核验。
- secret redaction 只是模式匹配，存在漏报；工具返回、prompt、error、session 与 hook 仍可能包含敏感值。
- telemetry 默认开启，会发送命令名、位置参数、Agent / model / tool、错误和用量；参数与错误可能含 prompt、路径、registry 引用或 secret。
- 多 Agent 协作、RAG 与 eval 只组织执行，不证明答案正确、检索完备、成本可控或外部动作获得授权。

## 补充建议

在用户级配置全局 deny 高危 shell / write / credential 工具，默认 `strict`，第三方 OCI 配置固定 digest 后逐项 review。敏感任务先设 `TELEMETRY_ENABLED=false`，使用只读副本和假 secret；sandbox 中也限制 mount、egress、TTL 与 registry，分别测试 escape、prompt injection、工具参数绕过和 session 恢复。

## 参考资料

- [GitHub 仓库](https://github.com/docker/docker-agent)
- [GitHub REST API](https://api.github.com/repos/docker/docker-agent)
- [README](https://github.com/docker/docker-agent/blob/main/README.md)
- [Permissions](https://github.com/docker/docker-agent/blob/main/docs/configuration/permissions/index.md)
- [Sandbox mode](https://github.com/docker/docker-agent/blob/main/docs/configuration/sandbox/index.md)
- [Secrets](https://github.com/docker/docker-agent/blob/main/docs/guides/secrets/index.md)
- [Telemetry](https://github.com/docker/docker-agent/blob/main/docs/community/telemetry/index.md)
- [v1.149.0 Release](https://github.com/docker/docker-agent/releases/tag/v1.149.0)
