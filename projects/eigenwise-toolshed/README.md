<!-- markdownlint-disable MD013 MD034 -->

# Eigenwise Toolshed：六个可独立安装的 Claude Code 插件

> 上游仓库：https://github.com/Eigenwise/eigenwise-toolshed · 归类：Agent 框架与技能生态 · 本页基于 2026-09-15 的 README、插件文档、release、LICENSE 与 GitHub REST API 静态整理；未安装插件、代理网关或 observability 服务。

## 定位

Eigenwise Toolshed 把反复出现的 Claude Code 工程任务拆成六个独立插件：Codebase Mapper、Live Rules、Sidequest、Model Gateway、Observability 和 Quartermaster。它不是一体化 agent，而是一组可按项目、local 或 user scope 选择的扩展，覆盖仓库地图、条件规则、并行工单、额外模型入口、用量观察与安装维护。

2026-09-15 的 GitHub 官方 JavaScript Trending 抓取显示约 `+25 stars today`；REST API 快照为 `247 stars / 26 forks / 8 open issues`，MIT，最新 release 为 `v3.566.0`（2026-09-14）。

## 用法

上游建议先添加 marketplace，再以项目 scope 安装 Quartermaster 或一个已知插件：

```text
/plugin marketplace add Eigenwise/eigenwise-toolshed
/plugin install quartermaster@eigenwise-toolshed --scope project
/reload-plugins
/quartermaster:setup
```

也可以把 `quartermaster` 换成 `sidequest`、`model-gateway`、`observability`、`codebase-mapper` 或 `live-rules`。安装后若改到进程级 gateway 或 model picker，仅 reload plugin 可能不够，需要完整重启 Claude Code。

## 原理

- **Codebase Mapper**：生成小型项目地图，在 session 开始时加载，并只刷新发生变化的区域。
- **Live Rules**：匹配任务时重新注入条件规则，避免把所有规则常驻上下文。
- **Sidequest**：以 ticket、owner、验证 gate 和 integration 状态管理旁路及并行工作。
- **Model Gateway**：在本机代理受支持的 ChatGPT/Codex 与 Grok 订阅模型，并把它们放进 Claude Code `/model` picker。
- **Observability**：按项目 opt-in 收集 session/tool 的选定 metadata，默认本地 SQLite，可选 loopback dashboard 或 remote sink。
- **Quartermaster**：读取本机 transcript 并生成有界汇总，逐项建议、安装和验证改进；原始 transcript 不直接载入模型上下文，但汇总会被当前模型看到。

## 价值

- 六个插件互不强制依赖，可只引入一个明确能力，降低全套安装造成的上下文和权限膨胀。
- project/local/user scope 让团队可以区分可共享配置、机器私有配置和全局工具。
- 对地图、规则、side work、用量和更新建立显式生命周期，有利于减少新 session 的重复探索。
- 文档区分缓存提示、实际更新、reload 和进程重启，避免把“已安装”误认为“当前 session 已生效”。

## 风险边界

- Model Gateway 会安装并运行本地代理、检查订阅登录并改写项目 `.claude/settings.local.json`；认证、端口、进程、模型条款和 provider 数据路径都需独立治理。
- gateway 默认记录 request-route metadata 和 per-session 最大请求体字节数；文档称不记录请求正文，但日志范围、保留期、文件权限和 remote control 仍须实测。
- Observability 可配置 remote sink，且本地数据库在压力下可能早于 30 天清理旧数据；“metadata-only”仍可能暴露仓库身份、模型、工具、成本与工作节律。
- Quartermaster 的本地脚本会读取 transcript 并生成模型可见汇总；有界聚合不是零隐私风险，也不能据 host policy 标签自动放宽权限。
- updater 可按记录的 scope 和路径更新多个活跃 Toolshed 安装；供应链、回滚和跨项目影响需要版本锁与变更审阅。
- 本页未复现 gateway 兼容性、920k 上下文测量、成本估计、sidequest 并行安全或 telemetry 的完整数据流。

## 补充建议

1. 从 project scope 的单一插件开始，固定 `v3.566.0`，记录 plugin、settings、hook 和后台进程的安装前后差异。
2. Model Gateway 只用测试订阅/低后果仓库验证登录、模型 picker、fallback、日志、端口和卸载；不要把 control token 放进 prompt。
3. 用无敏感 fixture 检查 Observability 的 SQLite/outbox/remote sink 内容和删除行为，再决定是否对真实项目 opt-in。
4. 对 Quartermaster 的 transcript 汇总做敏感字段和跨项目泄漏测试；任何权限、plugin 或 allowlist 建议均逐项审批。

## 参考资料

- 上游 README：https://github.com/Eigenwise/eigenwise-toolshed
- 插件文档：https://eigenwise.github.io/eigenwise-toolshed/reference/
- Model Gateway：https://github.com/Eigenwise/eigenwise-toolshed/tree/main/plugins/model-gateway
- Observability：https://github.com/Eigenwise/eigenwise-toolshed/tree/main/plugins/observability
- Quartermaster：https://github.com/Eigenwise/eigenwise-toolshed/tree/main/plugins/quartermaster
- `v3.566.0` release：https://github.com/Eigenwise/eigenwise-toolshed/releases/tag/v3.566.0
- GitHub REST API：https://api.github.com/repos/Eigenwise/eigenwise-toolshed
- LICENSE：https://github.com/Eigenwise/eigenwise-toolshed/blob/main/LICENSE
