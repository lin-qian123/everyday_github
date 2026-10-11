<!-- markdownlint-disable MD013 -->

# nao（getnao/nao）中文解读

> 上游仓库：<https://github.com/getnao/nao> · 归类：办公、商业与行业应用 · 本页基于 2026-10-12 的 README、文档、Release、许可证与 GitHub REST API 静态整理；未连接 warehouse、同步企业元数据、运行 SQL 或复测 evaluation。

## 定位

nao 是面向数据团队的 analytics agent 框架：先把数据库、metadata、modeling、规则、文档、工具和 MCP 组织成文件型 context，再向业务用户提供自然语言分析、可视化、来源与反馈界面。它把“Agent 上下文如何版本化和测试”放在部署聊天 UI 之前。

## 用法

```bash
pip install nao-core
nao init
cd <project>
nao debug
nao sync
nao chat
```

`nao init` 生成项目目录、`nao_config.yaml` 与 `RULES.md`；`sync` 拉取数据 / metadata / repo context；`chat` 默认在本地 Web UI 提供查询。测试目录可用 YAML 保存问题与期望 SQL，再执行 `nao test` 和 `nao test server`。

## 原理

- context builder 把异构 data stack 的 schema、语义、规则和工具同步到可版本化项目目录。
- Agent 根据自然语言与 context 生成分析 / SQL，并把 reasoning、source 和可视化返回前端。
- 测试框架用固定问题与期望 SQL 评估 context / Agent 版本变化。
- 后端使用 Fastify、Drizzle 与 tRPC，前端使用 TanStack Query / shadcn，可通过 Docker 自托管。

## 价值

- 把业务语义、数据模型、规则与评测放进可审阅的工程资产，而不是只依赖系统提示。
- 支持自托管与自带模型 key，适合在既有数据栈旁逐步试点。
- 为数据团队提供用户反馈和版本回归入口，便于把错误从一次性聊天转成可测样例。

## 风险边界

- NL2SQL、来源展示和“透明 reasoning”都不能证明答案正确；schema drift、指标口径、join、时间窗口和权限过滤必须由确定性检查兜底。
- self-hosted 不自动等于离线或安全：数据库、LLM、Slack、repo 与 Web 部署仍形成多条凭据和数据出口。
- 最小化数据库权限、只读视图、row / column policy、query budget、结果脱敏和 tenant 隔离需要外部配置。
- GitHub API 未识别 SPDX；根 LICENSE 说明“大多数文件”为 Apache-2.0，但带 `@license Enterprise` 标记的文件受另行商业条款约束，采用前必须逐文件审计。

## 补充建议

- 从只读、合成或脱敏 warehouse 开始，建立问句—SQL—结果三层金标，并加入越权、prompt injection 与高成本查询样例。
- 对 `nao sync` 产物做 secret / PII 扫描，明确哪些 context 可进入 provider、日志、反馈和测试报告。
- 版本升级时同时固定 nao release、context commit、模型、数据库 snapshot 与评测集，避免把口径漂移误判成模型改进。

## 参考资料

- GitHub 仓库：<https://github.com/getnao/nao>
- GitHub REST API：<https://api.github.com/repos/getnao/nao>
- `v0.3.22` Release：<https://github.com/getnao/nao/releases/tag/v0.3.22>
- 官方文档：<https://docs.getnao.io>
- Self-hosting guide：<https://docs.getnao.io/nao-agent/self-hosting/deployment-guide>
- Context skills：<https://docs.getnao.io/nao-agent/context-engineering/skills>
- LICENSE：<https://github.com/getnao/nao/blob/main/LICENSE>
