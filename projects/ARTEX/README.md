<!-- markdownlint-disable MD013 -->

# ARTEX（Autumn-27/ARTEX）

> 上游仓库：<https://github.com/Autumn-27/ARTEX> · 归类：办公、商业与行业应用 · 本页基于 2026-10-04 的 GitHub API、README、guard / intercept 源码、配置、Release 与 LICENSE 静态整理，未安装系统、生成 CA、配置 LLM、运行扫描、访问 Demo 或触碰任何目标。

- 抓取快照：1,466 stars、270 forks、41 open issues。
- 热度信号：GitHub Go Trending 抓取时约 +78 当日 stars。
- 版本与许可：GitHub API / LICENSE 为 AGPL-3.0，latest Release / tag 为 `v0.3.14`；README 另附只允许本地隔离学习验证、禁止线上系统测试的用途条款。

## 定位

ARTEX 是 Go 后端、内嵌 Next.js 前端和 PostgreSQL 组成的多 Agent 自主渗透研究系统。它把目标、资产、探索链、工具执行、MITM 流量、发现、复测、报告、审批、MCP 与 ScopeSentry 资产导入放在一个 Web 控制面中。

## 用法

上游提供 Docker / 本地编译 / Release 二进制路径，依赖 PostgreSQL 与 Anthropic 或 OpenAI-compatible LLM。首次启动设置管理员密码；用户可导入资产、设置 planner / worker 与工具、查看双图和流量、人工对话或审批，再对发现发起独立复测。README 明确只允许源码学习与本地隔离原理验证。

## 原理

每个任务由事件驱动 planner 与多个 worker 推进：planner 读取探索图与资产图，派发带资产锚点的 intent；worker 使用真实 Bash / HTTP / Kali 工具执行并把 fact、asset、finding 与 trace 写回。跨 worker 可检索执行过程，共享 todolist 维持多轮攻击链；guard / intercept 在 tool hook 上按数据库规则决定 allow、deny 或 ask。

## 价值

双图把“资产真值”和“探索 / 证据血缘”分开，可帮助研究者审查一个发现从目标、意图、工具到证据的路径；过程 trace、MITM 记录、人工审批和漏洞复测也比只返回 Agent 最终结论更接近可审计的安全研究流程。

## 风险边界

- 这是可执行真实扫描、利用和横向步骤的高危系统；README 明确禁止对任何线上 / 联网系统实际测试，即使获得授权或资产自有也不在作者列出的允许范围内。
- `guard.go` 注释写明旧 RoE authorization-scope 机制已移除；破坏 / 外传 gate 改由普通数据库 intercept rule 实现，用户可禁用或删除，未匹配且 fallback judge 未启用时会放行。
- `New()` 可在 interceptor 尚不可用时创建 guard；审计记录、审批卡和 UI 不能被解释成始终 fail-closed 的内核隔离。
- 记录型 MITM proxy 与 CA、Bash / nmap、MCP、外部 skill、LLM key、数据库和完整攻击 trace 会集中敏感数据并扩大供应链、凭据和日志泄露面。
- 自动“已修复”结论依赖复测 Agent 的输出；复测、报告和 graph lineage 都不能替代安全人员复现、证据保存与修复方确认。
- README 的额外用途限制与标准 AGPL-3.0 文本需要分别理解；再分发、托管和使用前应取得明确法律 / 作者说明，不能只看 API SPDX。

## 补充建议

严格遵循上游范围，只在断网、无生产凭据、可还原的本地靶场中固定 `v0.3.14`；从容器 / VM egress deny、只读 fixture 与单 worker 开始。把 scope 放到系统外的网络 / hypervisor 层执行，默认删除攻击性 credential，锁定 skill / MCP / image hash，并验证无 interceptor、规则删除、审批超时、LLM 误判、MITM CA 泄露和停止任务时的 fail-closed 行为。

## 参考资料

- [GitHub 仓库](https://github.com/Autumn-27/ARTEX)
- [GitHub REST API](https://api.github.com/repos/Autumn-27/ARTEX)
- [README、架构与用途限制](https://github.com/Autumn-27/ARTEX/blob/main/README.md)
- [Guard 源码](https://github.com/Autumn-27/ARTEX/blob/main/guard/guard.go)
- [Intercept 目录](https://github.com/Autumn-27/ARTEX/tree/main/intercept)
- [配置示例](https://github.com/Autumn-27/ARTEX/blob/main/config.example.json)
- [v0.3.14 Release](https://github.com/Autumn-27/ARTEX/releases/tag/v0.3.14)
- [LICENSE](https://github.com/Autumn-27/ARTEX/blob/main/LICENSE)
