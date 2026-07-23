# skeptic

## 定位

`skeptic` 是以对抗性测试审查 PR 的 Claude Code skill，尝试推翻 diff 中的每项有效性声明，并与基线对照。

截至 2026-07-23，GitHub API 显示其创建于 2026-07-22，约 1 star；属早期开发者信号。

## 用法

对 PR 或 diff 运行流程，要求输出新增测试、基线对照和可定位的反例，而不是仅给文字意见。

## 原理

通过 hostile tests 与 base control run 区分新回归和既有弱点，使 agent 审查更接近可执行反证。

## 价值

- 有助于降低“看起来合理”的 AI 代码被直接合并的风险。
- 适合与常规 code review 和 CI 形成互补。

## 风险边界

- 对抗测试覆盖有限，不能证明没有漏洞。
- 运行任意测试或构造输入可能带来时间和安全成本。

## 补充建议

先确定危险接口、兼容性和数据边界，再针对性生成反例；保留稳定的失败测试。

## 参考资料

- GitHub：<https://github.com/tokyubevoxelverse/skeptic>
