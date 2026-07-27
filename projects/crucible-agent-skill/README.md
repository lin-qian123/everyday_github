# crucible-agent-skill

## 定位

`crucible-agent-skill` 是以简化、删除冗余和降低 diff 规模为目标的 coding agent skill。

截至 2026-07-27，GitHub API 显示其创建于 2026-07-26，约 4 stars；属早期开发者信号。

## 用法

将 skill 作为重构或评审阶段的约束，要求它先列出可删除内容、风险和验证步骤，再生成改动。

## 原理

把“更少代码”变成明确优化目标，通过收缩 diff、消除重复和减少无效复杂度约束 agent 行为。

## 价值

- 可抵消 AI 生成代码常见的无谓抽象和规模膨胀。
- 与测试、性能测量和架构审查结合时更有实际价值。

## 风险边界

- 简化不等于正确；关键兼容性、监控和边界条件可能被误删。
- 不能用风格偏好替代需求和回归测试。

## 补充建议

要求每次删除都有测试、基线对比和可回滚的小提交。

## 参考资料

- GitHub：<https://github.com/ryanelian/crucible-agent-skill>
