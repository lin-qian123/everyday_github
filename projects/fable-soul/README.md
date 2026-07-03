# fable-soul

- GitHub：<https://github.com/akseolabs-seo/fable-soul>
- 抓取时间：2026-07-04（Asia/Shanghai）
- 今日信号：GitHub API 显示该仓库创建于 2026-07-03，抓取时约
  `41 stars / 14 forks`，README 定位为 Claude Code 与 Codex
  可用的 AI coding agent judgment layer。

## 定位

`fable-soul` 是一套面向 AI coding agent 的“判断层”规则包。它认为很多 agent 失败并不是不知道怎么写代码，而是缺少资深工程师式的操作纪律：先定位目标与机制、用证据验证、遇到反常结果暂停、不要把弱检查伪装成强验证、能完成的可逆任务不要停在诊断。

项目用一个 skill 包和若干 Markdown 参考文件，把这些规则组织成可加载、可维护、可迁移的 agent 行为层。

## 用法

仓库核心结构包括：

```text
SKILL.md
references/soul.md
references/soul-compact.md
references/maintenance.md
references/transfer-prompts.md
references/evals.md
scripts/sync_soul.py
scripts/validate_skill.py
```

典型使用方式是把它作为 Codex / Claude Code 的 skill 或全局规则加载，让 agent 在执行任务时遵守：

- 任务开始前明确 goal、mechanism、proof。
- 按任务类型选择合适验证方式。
- 对重复失败、缺少机制解释、测试意外通过/失败等红旗信号触发恢复动作。
- 用维护脚本同步规则文件，检查本地副本是否漂移。

## 原理

该项目把“资深判断”拆成三层：

1. **Operating Gates**：任务开始、验证合同、红旗恢复等执行检查点。
2. **Rules**：围绕目标、根因、验证、完成度、沟通粒度、诚实边界的规则。
3. **Maintenance / Transfer**：把真实 agent 失败案例转成可复用规则，并用 eval 场景验证规则是否真的改变行为。

它更像 agent 的操作系统补丁，而不是一个独立应用。

## 价值

- 对高频使用 coding agent 的开发者：帮助减少“改了但没跑”“顺着错误修”“过度解释但不完成”的常见失败。
- 对团队：可以作为全局 agent 行为规范，补齐项目级 `AGENTS.md` 之外的通用工程纪律。
- 对 agent 生态：体现了从“更强模型”转向“更强 harness / rules / evals”的趋势。

## 风险边界

- 规则包不能保证模型一定遵守，尤其是在上下文竞争、工具失败或长任务压缩后。
- 规则过重可能让简单问题产生不必要的仪式感，需要根据任务类型启用不同强度。
- 行为规则来自作者经验，迁移到其他团队前应结合本地工程约束做删改。
- 它不能替代真实测试、CI、代码审查或安全审计。

## 补充建议

- 与 `self-learning-skills`、`loop-engineering`、
  `awesome-harness-engineering` 一起观察：这些项目都在补 agent
  可靠性，但一个偏经验沉淀，一个偏 loop 设计，一个偏资料索引，
  本项目偏行为规则。
- 可把其中“Proof Contract”思路移植到团队自己的 `AGENTS.md`，但不要无脑复制全部规则。
- 后续关注它的 evals 是否会从手工场景扩展为可自动运行的 agent behavior test。

## 参考资料

- GitHub 仓库：<https://github.com/akseolabs-seo/fable-soul>
- Skill 入口：<https://github.com/akseolabs-seo/fable-soul/blob/main/SKILL.md>
