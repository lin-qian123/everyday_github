<!-- markdownlint-disable MD013 -->

# gcx（grafana/gcx）

> 上游仓库：<https://github.com/grafana/gcx> · 归类：Coding Agents 与终端助手 · 本页基于 2026-10-08 的 GitHub API、README、architecture / auth 文档与源码静态整理，未连接 Grafana Cloud、生产 dashboard、告警或 telemetry 数据源。

- 抓取快照：771 stars、57 forks、325 open issues。
- 热度信号：GitHub Go Trending 抓取时约 +1 当日 star；最后 push 为 2026-10-07。
- 版本与许可：最新 Release / tag `v1.5.0`，Apache-2.0；本页固定审计 commit `1308ec35924a`。

## 定位

gcx 是 Grafana Labs 面向人和 Coding Agent 的统一 CLI，覆盖 Grafana Cloud、Enterprise 与 OSS 的 dashboard、folder、alert、SLO、metrics、logs、traces、profiles 等资源。它同时分发 Agent Skills，让 Agent 能以结构化 JSON、GitOps 文件和明确命令操作可观测性平台。

## 用法

本地安装后先运行 `gcx login` 建立 context；自动化应优先使用只读或最小权限 service-account token。读取用 `gcx resources get`、signal query 等命令；写入前先用 `gcx resources push -p ./resources --dry-run` 审阅 diff。Agent Skills 通过 `gcx agent skills install --all` 安装到宿主技能目录，采用前应先读单个 skill 的工具与写入范围。

## 原理

Go CLI 把资源映射为统一 provider / resource adapter，经 context 选择 Grafana server、Cloud product endpoint 与认证方式；支持 OAuth PKCE、service-account token、Basic Auth、mTLS 和 Cloud Access Policy。动态 client、raw API、pull / edit / push 流程与 JSON 输出为 Agent 提供稳定接口，credential transport 按明确 auth method 选择，避免把旧凭据附到错误目的地。

## 价值

它把 dashboard-as-code、告警调查、SLO 和多类 signal query 放到同一可脚本化入口，并为 Agent 提供可机读输出、dry-run 与 portable skills。相比让模型直接拼 REST 请求，集中 auth、版本检测和资源 schema 更易审计，也便于在人类复核后把变更写回 Git。

## 风险边界

- Viewer、Editor、Admin 与 Cloud product token 能力差异很大；同一 CLI 同时支持读、写、删除、原始 API 和 stack 创建，不能给 Agent 一个全能 token。
- OAuth access / refresh token、CAP、Basic Auth 和 mTLS key 会进入 OS credential store、环境变量或明确授权的配置来源；日志、shell history 和仓库文件不得泄漏它们。
- `--dry-run` 只覆盖支持预览的命令，不能自动证明最终服务器状态、成本、RBAC 或下游告警行为安全；写后必须回读。
- Agent Skills 是操作知识，不是授权层；生产 dashboard、alert、SLO、instrumentation 和 Cloud Assistant 调用仍会产生真实副作用或费用。
- Grafana 12 的部分 app-platform API 需 feature toggle，13+ 才是当前完整支持线；版本差异可能导致读写语义和 schema 漂移。
- 仓库提供的工作流示例没有在本轮真实实例复测；成功命令不能证明 telemetry 完整、根因正确或告警不会漏报。

## 补充建议

为 Agent 建只读测试 stack 和按 datasource / resource 限定的 token，context 名称显式区分 `dev` / `prod`。所有写操作要求“pull → Git diff → dry-run → 人工批准 → push → 回读”，删除另设二次审批；定期扫描配置、日志与技能目录中的 credential，并记录 gcx / Grafana 版本。

## 参考资料

- [GitHub 仓库](https://github.com/grafana/gcx)
- [GitHub REST API](https://api.github.com/repos/grafana/gcx)
- [README 与认证说明](https://github.com/grafana/gcx/blob/main/README.md)
- [架构说明](https://github.com/grafana/gcx/blob/main/ARCHITECTURE.md)
- [Auth system](https://github.com/grafana/gcx/blob/main/docs/architecture/auth-system.md)
- [Config system](https://github.com/grafana/gcx/blob/main/docs/architecture/config-system.md)
- [Data flows](https://github.com/grafana/gcx/blob/main/docs/architecture/data-flows.md)
- [v1.5.0 Release](https://github.com/grafana/gcx/releases/tag/v1.5.0)
