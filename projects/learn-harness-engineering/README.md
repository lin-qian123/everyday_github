<!-- markdownlint-disable MD013 MD034 -->

# Learn Harness Engineering

- GitHub: https://github.com/walkinglabs/learn-harness-engineering
- 分类：Agent 框架与技能生态
- 主要语言：TypeScript
- 抓取日期：2026-07-14

## 定位

`learn-harness-engineering` 是一个面向 AI coding agents 的项目式课程，主题是 harness engineering：如何构建环境、状态管理、验证、控制机制、技能和自动化循环，让 coding agent 在真实工程里更可靠。

GitHub API 样本显示该仓库约 `10.3k stars`，README 标注 2026 年 7 月新增 Loop Engineering 更新，包括第 13 讲和第 7 个项目。

## 用法

该仓库更像课程和模板库，而非单一运行工具。使用方式包括：

1. 按课程阅读 lectures，理解 harness、状态、验证、控制和 loop 的基本概念。
2. 跟做 projects，把理论落到实际 agent 工作流。
3. 使用 `skills/harness-creator/` 辅助生成项目级 harness 文件。
4. 复用 `goal-template.md`、`loop-state-template.md`、`maker-prompt.md`、`checker-prompt.md` 等模板。

## 原理

课程把 agent 可靠性问题从“写更好的 prompt”转向“设计更好的运行环境”：

- 环境：工作区、依赖、权限和可复现启动方式。
- 状态：任务目标、当前进度、外部记录和长期上下文。
- 验证：测试、lint、审查、截图、日志和完成判据。
- 控制：预算、停止条件、人工介入点和回滚。
- Loop：把 maker/checker、定时任务、目标循环等自动化结构化。

## 价值

- 对新手：给出比“让 agent 帮我写代码”更系统的学习路径。
- 对团队：提供可讨论的术语和模板，便于统一 coding agent 的使用标准。
- 对本仓库：它解释了近期大量 `skills`、`harness`、`loop` 项目为什么会同时进入热榜。

## 风险边界

- 课程和模板不能替代实际项目验收；每个仓库仍需按技术栈定制。
- Loop 自动化越强，越需要外部状态、审计日志和人工停机开关。
- 课程中引用的工具生态变化很快，具体命令和宿主能力需要按当前版本复核。
- 模板若被机械复制，可能形成表面流程，不能真正提升 agent 质量。

## 补充建议

- 用一个小型真实仓库实践课程项目，不要只阅读概念。
- 把课程中的 maker/checker 结构与现有 CI、review、issue 流程接起来。
- 与 `awesome-harness-engineering`、`loop-engineering`、`loopkit`、`loopy` 横向比较，区分资料索引、方法论、可安装 harness 和 loop library。

## 参考资料

- GitHub 仓库：https://github.com/walkinglabs/learn-harness-engineering
- OpenAI Harness Engineering 文章：https://openai.com/index/harness-engineering/
- Anthropic 长任务 harness 文章：https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents
