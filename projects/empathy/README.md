# empathy

## 定位

`empathy` 是 Daniel Roe 发布的 Agent Skill，目标不是提高 agent 的产出量，而是在 agent 准备向开源维护者、issue 或 PR 评论区发送人类可见文本前，加入沟通与披露约束。

截至 2026-07-31，GitHub API 快照显示该仓库创建于 2026-07-30，约 28 stars、0 forks，MIT 许可证。它是早期开发者信号，不是对 agent 社区沟通效果的独立实证评测。

## 用法

兼容 Agent Skills 的宿主可直接安装；也可先以项目级规则试用，再决定是否全局启用。

```bash
npx skills add danielroe/empathy
```

在派发会写入 issue、PR 或评论的任务时，显式要求 agent 先读该 skill；维护者也可将其原始 `SKILL.md` 链接放入仓库的 `AGENTS.md`。

## 原理

它把发布前检查写进结构化 Markdown：读者是否知道在同 agent 交互、信息是否真正有用、是否尊重称谓、是否足够简短，以及“不发是否更合适”。这种规则层不替代模型能力，而是尝试在生成与外部沟通之间加入可审阅的行为门槛。

## 价值

- 将 agent 身份披露、人工复核状态与注意力成本变成明确的工程约束。
- 适合开源协作、自动化 triage 和批量评论等最容易造成噪声的场景。

## 风险边界

- 技能文本不能保证宿主真的加载；仓库自身也提示模型可能跳过技能，需要在任务提示或系统规则中强制。
- “共情”不等于可以代表人类作承诺；权限、发布和社区规范仍应由维护者控制。
- 不应把礼貌措辞用于掩盖自动化身份、未经核验的结论或大规模骚扰。

## 补充建议

先在一个有明确 PR 模板和人工审核的仓库中试点，记录无效评论率、维护者反馈与漏报率。对外发言保留 agent 身份、操作范围和人工审核状态，必要时默认只产出草稿。

## 参考资料

- GitHub：<https://github.com/danielroe/empathy>
- GitHub API 快照：<https://api.github.com/repos/danielroe/empathy>
- Agent Skills：<https://agentskills.io>
