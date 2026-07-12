# fable-method

<!-- markdownlint-disable MD013 -->

## 定位

`fable-method` 是一组从 Claude Fable 5 工作流中提炼出的 agent skills 和评测材料。它把“think / act / prove”写成可执行流程：先分类任务、定义 done、并行收集证据、做一个明确推荐、最小改动、观察验证，再诚实报告结果。

截至 2026-07-13，GitHub API 显示该仓库约 286 stars、40 forks，创建于 2026-07-06，许可证为 MIT。它不是单纯 prompt 集，而是带失败案例、评测日志和 judge skill 的方法论包。

## 用法

Claude Code plugin 安装方式：

```text
/plugin marketplace add Sahir619/fable-method
/plugin install fable@fable-method
```

也可作为 standalone skills 安装：

```bash
git clone https://github.com/Sahir619/fable-method
bash fable-method/install.sh
```

包含的核心 skills：

```text
fable-method
fable-loop
fable-judge
```

## 原理

项目把 agent 工作拆成明确阶段，并给每个阶段设置退出条件和验证标准。README 记录了多轮 eval：它强调方法价值集中在“陷阱任务”中，例如规格与测试冲突、虚假完成报告、弱 executor、无人值守长任务等。

## 价值

- 把抽象的“谨慎、验证、少改”变成更具体的 agent 执行流程。
- 对 Codex / Claude Code / Cursor 这类工具的团队规范有迁移价值。
- `fable-judge` 可用于审查 agent 自称完成的工作，和自动化验收思路一致。
- 与 `fable-soul`、`loopkit`、`loopy` 一起构成 agent loop 方法论热点。

## 风险边界

- 方法论来自特定模型和作者经验，不能保证跨模型、跨任务稳定提升。
- 评测场景虽有日志，但仍需独立复测，不能只看 README 宣称。
- 过度流程化会让简单任务变慢，需要保留 trivial path。
- judge skill 只能辅助发现问题，不能替代真实测试、lint 和人工 review。

## 补充建议

- 适合把其中的 done definition、intent gate、verification loop 拆进团队 `AGENTS.md`。
- 对高风险自动化任务，可以单独引入 `fable-judge` 做完成报告审计。
- 观察它是否会被其他 agent harness 吸收，形成更通用的 verification pattern。

## 参考资料

- GitHub 仓库：<https://github.com/Sahir619/fable-method>
- 评测结果：<https://github.com/Sahir619/fable-method/blob/main/eval/RESULTS.md>
- 技能说明：<https://github.com/Sahir619/fable-method/tree/main/skills>
