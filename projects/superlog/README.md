# superlog

## 1. 项目定位

`superlog` 是一个开源 agentic telemetry / observability 工作台，面向 OpenTelemetry 数据接入、日志/指标/trace 聚合、incident 分组和 AI agent 辅助排障。

它的核心卖点是把可观测性系统从“人看图表找问题”推进到“系统把噪声归并成 incident，再交给 agent 形成调查摘要或后续动作”的方向。

## 2. 基本用法

官方 README 给出的本地开发依赖包括 Node.js 20、pnpm 9 和 Docker。快速启动方式如下：

```bash
pnpm install
docker compose up -d
pnpm --filter @superlog/db db:migrate
pnpm dev
```

默认本地服务包括：

- Web：`http://localhost:5173`
- API：`http://localhost:4100`
- OTLP intake：`http://localhost:4101`

项目也提供与 coding agent 配套的 skills 安装入口：

```bash
npx skills add superloglabs/skills --all
```

## 3. 核心原理

`superlog` 的开源社区版包含 Web app、API、OTLP ingest proxy、worker、Postgres schema、ClickHouse 查询、telemetry fingerprinting 和 agent runner 接口。

工作流大致是：

1. 服务通过 OTLP 或相关 helper 把 traces、logs、metrics 送入系统。
2. 后端对噪声信号做 fingerprint 和 incident 分组。
3. worker 与 agent runner 对 incident 生成调查摘要或本地排障记录。
4. Web 工作台提供团队调试和追踪界面。

## 4. 工程价值

AI agent 进入生产工程后，最难的问题之一是“系统出了问题时，agent 能否拿到足够上下文并做出可追踪判断”。`superlog` 把 observability 数据和 agent runner 接起来，是 AI 运维、自愈软件、agentic debugging 的代表样本。

它也说明 agent 工程热点正在从 IDE 扩展到生产系统运行阶段：代码生成、测试验证、发布、监控、incident triage 会逐步形成闭环。

## 5. 风险边界

- 自动 incident 分组和 agent 摘要不能替代 SRE 判断，尤其是生产故障、数据一致性和安全事件。
- OpenTelemetry 数据可能包含请求参数、用户信息或内部服务拓扑，必须做脱敏和访问控制。
- 自愈动作如果未来扩展到自动修复或自动回滚，需要更强的审批、审计和回滚机制。
- 本地社区版和云服务版的能力边界、数据位置、费用模型需要分别评估。

## 6. 补充建议

- 初期只用作“观察 + 摘要”，不要直接授权自动改生产系统。
- 与已有 Datadog、Grafana、Sentry、OpenTelemetry Collector 体系对接时，先明确数据复制路径。
- 适合和 `testsprite-cli` 形成对照：前者偏生产运行观测，后者偏交付前验证。
- 后续可重点跟踪它的 agent runner 是否能支持更明确的 evidence trail 和可回放调查过程。

## 7. 参考资料

- GitHub 仓库：https://github.com/superloglabs/superlog
- 官方网站：https://superlog.sh
- Skills 仓库：https://github.com/superloglabs/skills
- OpenTelemetry：https://opentelemetry.io

