<!-- markdownlint-disable MD013 -->

# pilotfish

## 定位

`Nanako0129/pilotfish` 是一个面向 Claude Code 的多模型编排配置层。它主张让 frontier model 负责规划、判断和复核，把搜索、机械编辑、测试等高容量工作委派给更便宜的模型/子 agent，再用 fresh-context verification 控制质量。

## 用法

项目不是传统运行时框架，而是一组安装到 `~/.claude/` 的配置：settings、role agents 和 policy。README 强调全局安装、每个项目复用，并提供 fallback 机制。

## 原理

pilotfish 的核心是角色化 delegation policy：主会话使用更强模型，若干全局 subagent 被固定到不同模型层级和能力面。它还覆盖 Explore 等内置行为，避免高成本模型承担所有后台搜索和例行工作。

## 价值

- 把“多模型成本优化”落到 Claude Code 日常配置，而不是停留在论文或 SaaS 控制面。
- 强调 verifier subagent 和 fresh context，契合近期 agent 评测对自我批判不足的共识。
- 对订阅额度有限但任务较多的用户有现实意义。
- 作为配置型项目，便于研究不同角色、模型和成本策略的组合。

## 风险边界

- 它深度依赖 Claude Code 版本、模型命名和订阅规则，外部条件变化会影响效果。
- 更便宜模型执行机械任务不等于总是可靠，仍需测试和人工审查。
- 全局安装会影响所有项目，错误 policy 可能扩散到无关工作区。
- README 中的成本数字需要按用户自己的账号、任务和模型重新测量。

## 补充建议

- 先在单独 Claude profile 或测试账号里试用，确认不会污染主工作流。
- 记录同一任务在 all-frontier 与 orchestrator/worker 策略下的成本、耗时和失败模式。
- 关注是否支持 Codex、Grok Build、Gemini CLI 等其他 harness 的同类策略。

## 参考资料

- GitHub: <https://github.com/Nanako0129/pilotfish>
