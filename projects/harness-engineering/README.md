<!-- markdownlint-disable MD013 -->

# harness-engineering

## 定位

`harness-engineering` 是 Ryan Lopopolo 对 agent harness 工程的资料库、论证集和上下文包。它不是一个单一 CLI，而是把“让模型之外的环境更可靠”系统化：通过仓库规则、上下文组织、工具边界、验证机制、playbook 和可追溯资料，让 coding agent 在同一个模型能力下更稳定地产出工程结果。

## 用法

- 作为团队的 agent 工程读本：从 `docs/`、`playbooks/` 和 `AGENTS.md` 理解如何把本地约束写成 agent 可读取的工作环境。
- 作为项目模板参考：把非功能需求、完成定义、验证命令、权限边界和接续记录放进仓库，而不是只依赖聊天提示。
- 作为外部上下文：让 Codex、Claude Code 等 agent 在执行复杂工程任务前读取该仓库中的论证和 playbook。

## 原理

项目的核心观点是：agent 的表现不只由模型决定，还由 context、tools、authority、proof 和 feedback loop 决定。仓库通过文档分层、来源索引和任务路由，把组织内部的质量标准、决策历史和操作边界转成可检索上下文；再通过验证和 handoff 机制，让每次运行留下下一次可复用的结构化经验。

## 价值

- 把“提示词技巧”提升为可维护的工程环境设计。
- 适合团队沉淀 coding agent 的完成标准、测试纪律和权限边界。
- 对已经大量使用 Codex / Claude Code / Cursor 的团队，有助于减少同类错误反复出现。
- 与本仓库长期跟踪的 `loop-engineering`、`awesome-harness-engineering`、`agentsmith` 等项目构成同一赛道。

## 风险边界

- 它主要是方法论和资料库，不是开箱即用的自动化平台。
- 具体收益依赖团队是否愿意维护本地规则、验证脚本和任务记录。
- “harness 贡献 90%”一类表述应理解为作者经验性判断，不宜直接当作可泛化指标。
- 若只复制规则文件、不补齐真实测试和权限控制，很容易变成静态文档负担。

## 补充建议

- 可把它作为制定项目 `AGENTS.md` / `CLAUDE.md` / `TODO.md` 的参考材料。
- 与实际 CI、lint、review checklist 配套使用，避免只停留在原则层。
- 对团队项目，优先先整理“完成定义”和“可验证命令”，再扩展复杂 playbook。

## 参考资料

- GitHub：<https://github.com/lopopolo/harness-engineering>
- OpenAI Harness Engineering 文章：<https://openai.com/index/harness-engineering/>
- 作者 X 线索：<https://x.com/_lopopolo/status/2050698864542482709>
