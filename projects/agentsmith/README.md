<!-- markdownlint-disable MD013 -->

# agentsmith

## 定位

`agentsmith` 是 PromptPartner 开源的模型无关 agent operating harness，面向 Claude Code、Codex、Gemini 等可读取 `CLAUDE.md` / `AGENTS.md` / `GEMINI.md` 的 coding agent。它试图把真实工程中的计划、实现、验证、交付、handoff 和规则迭代沉淀成可安装的通用 harness。

## 用法

- 通过 `setup.sh` 安装核心规则，并按项目类型选择软件开发、DevOps、研究、设计、文档、数据处理等 profile。
- 在项目中生成或组合 agent 指令文件，让不同 agent 共享同一套完成标准。
- 每个任务按 plan -> implement -> verify -> ship 的闭环推进，验证脚本由项目自身定义。

## 原理

仓库把 harness 拆成 universal core 和 work-type profiles：core 负责不可变的工程纪律，如证据优先、风险分级、验证前不能宣称完成、上下文压缩前 handoff；profile 则负责不同工作类型的具体语气、输出结构和质量门槛。安装脚本把这些部分组合成目标 agent 能读取的规则文件。

## 价值

- 把多 agent 使用经验从个人提示词迁移到项目内可版本化资产。
- 对“同一仓库多人/多 agent 协作”有价值，因为规则和验证习惯能随代码一起演进。
- 与 `harness-engineering` 的方法论互补：前者偏资料和论证，`agentsmith` 偏可安装规则包。

## 风险边界

- 当前仓库创建时间很新，星标增长快但长期维护能力仍需观察。
- license 元数据在 GitHub API 中未明确暴露，生产使用前应检查许可证文件。
- 规则 harness 不能替代真实测试、代码审查和权限控制。
- 若 profile 与既有团队流程冲突，可能导致 agent 过度流程化或输出冗长。

## 补充建议

- 适合先在低风险项目试用，观察任务完成率、验证覆盖和上下文消耗。
- 与项目现有 `AGENTS.md` 合并时要保留本地硬约束，避免覆盖仓库特定规则。
- 可重点关注它是否继续补充跨 agent 兼容性和真实案例。

## 参考资料

- GitHub：<https://github.com/PromptPartner/agentsmith>
- 项目主页：<https://promptpartner.ai>
- README 与文档入口：<https://github.com/PromptPartner/agentsmith#readme>
