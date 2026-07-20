<!-- markdownlint-disable MD013 -->

# graphkit

## 定位

`graphkit` 是一个 Claude Code skill，把长时程 coding task 拆成 executor 和 supervisor 两类 agent node，通过 ledger、directives 和 git tree 连接，避免单一 agent loop 在长上下文中漂移。它把“loop engineering”推进为更显式的“graph engineering”方法。

## 今日信号

- GitHub：<https://github.com/levi-qiao/graphkit>
- 创建时间：2026-07-19。
- 抓取时约 23 stars、1 fork。
- 语言 / 许可证：Shell，MIT。
- Topics：`agentic`、`claude-code`、`multi-agent`、`orchestration`、`skill`。

## 用法

安装后在 Claude Code 中运行 `/graphkit`，按 interview 填写目标、验收门槛、红线、分支、提交授权和 supervisor 间隔。它会在仓库中生成 `.graphkit/<date-slug>/`，包括 executor prompt、supervisor prompt、ledger、directives 和 ops 文档。用户再把 executor prompt 交给执行 agent，supervisor 定期以新上下文审查 ledger 和 git tree。

## 原理

graphkit 的核心不是复杂运行时，而是把状态写成文件：executor 每轮只做一个 ledger item；supervisor 每次冷启动，只读 ledger 和 git tree，通过 directives 单向纠偏。两个 node 不共享上下文，也不同时写同一文件，从结构上降低“执行者自我判定完成”的漂移风险。

## 价值

- 对长任务、迁移、性能优化、生产化收尾这类容易漂移的 coding agent 工作流有直接参考意义。
- 不依赖 LangGraph 或服务端编排，Markdown 文件即可复用到不同 agent host。
- 把“强模型少量监督 + 便宜执行模型多轮执行”的成本结构说清楚。

## 风险边界

- 目前主要面向 Claude Code skill；跨 Codex / OpenCode 等 runtime 需要用户手工适配。
- ledger 纪律依赖 agent 和用户持续遵守，不能替代真实测试、CI 和代码审查。
- supervisor 只读文件与 git tree，若验收信号没有写入 ledger 或测试命令，仍可能漏判。

## 补充建议

- 后续观察是否增加更多 node role、自动调度和跨 agent host 示例。
- 可与 `loop-engineering`、`fable5-mode`、`pilotfish`、`agentsmith` 一起归入 coding agent 方法论 / harness 工程线索。
- 用于真实项目时，应把验收命令、冻结 contract 和不可触碰文件写进 ledger 初始模板。

## 参考资料

- GitHub 仓库：<https://github.com/levi-qiao/graphkit>
- README：<https://github.com/levi-qiao/graphkit#readme>
- 中文 README：<https://github.com/levi-qiao/graphkit/blob/main/README.zh-CN.md>
