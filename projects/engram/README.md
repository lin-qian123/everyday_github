# engram

<!-- markdownlint-disable MD013 MD012 -->

## 定位

`engram` 是一个面向 Claude Code 和 Codex 的本地学习记忆引擎。它把“让模型解释知识”改造成“学习、回忆、测验、间隔复习”的闭环，目标是让用户下个月仍然记得今天学过的内容。

它更像 agent 时代的个人学习系统，而不是普通笔记工具。

## 用法

Claude Code 安装示例：

```bash
claude plugin marketplace add nagisanzenin/engram
claude plugin install engram@engram
```

Codex 侧也提供安装说明。安装后主要使用三个命令：

```text
/learn kalman filters
/review
/coach
```

项目强调本地 JSON 状态、无需账号、无需云服务，并使用 FSRS-4.5 风格的间隔复习调度。

## 原理

Engram 把一次学习拆成几个可验证环节：

- Curriculum architect：把主题拆成第一性原理概念图。
- Tutor：要求用户先预测、再获得提示、再用自己的话解释。
- Assessor：用独立评估者按 rubric 盲评用户答案。
- Scheduler：把概念和评分写入本地状态，计算下次复习时间。
- Hook：在后续会话中提示到期复习任务。

关键点是它不只保存“模型讲过什么”，而是保存“用户是否能主动回忆并通过评估”。

## 价值

- 对个人知识管理：把 LLM 学习从一次性解释推进到可持续复习。
- 对 agent memory：展示了“记忆”不只是检索上下文，也可以是行为计划和复习日程。
- 对教育产品：强调 free recall、盲评、收据和本地数据，降低幻觉式自信。
- 对 Codex/Claude 用户：可以把编程、数学、论文、系统设计等知识学习纳入日常终端工作流。

## 风险边界

- 学习评估仍依赖模型生成的 rubric 和判断，不能替代专业课程考试。
- 复杂主题拆解质量取决于模型能力和提示约束。
- 本地状态虽然可控，但也需要备份，否则复习历史容易丢失。
- README 中默认示例提到 `python3`；在本机仓库自动化约束中仍以 `python` 为默认，具体安装按项目说明执行。

## 补充建议

- 适合用于长期主题，如数学、Rust、论文阅读、交易框架或系统设计。
- 对关键知识，建议额外导出 Markdown 笔记或 Anki 卡片，避免绑定单一插件。
- 可观察它是否接入更多 agent 宿主，并把学习记录做成跨工具可迁移格式。
- 与 `open-knowledge`、`nanobot`、`agentmemory` 的差异在于：engram 更强调学习验证，不只是长期上下文。

## 参考资料

- GitHub 仓库：<https://github.com/nagisanzenin/engram>
- Codex 安装说明：<https://github.com/nagisanzenin/engram/blob/main/INSTALL-CODEX.md>
