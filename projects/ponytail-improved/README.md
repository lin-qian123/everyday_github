# ponytail-improved

## 定位

`ponytail-improved`（README 对外名称为 Ponytail）是一组可安装的 agent skills 与两个生命周期 hook，目标是在 coding agent 写代码前依次检查“是否根本不需要做、仓库/标准库/平台是否已有能力”，以抑制过度工程。

截至 2026-07-29，GitHub API 显示其创建于 2026-07-28，约 378 stars、55 forks，采用 MIT；这是单日早期开发者信号，不等同于其 README 中成本、速度或代码量对比的独立验证。

## 用法

项目 README 给出的一键安装方式如下；它需要本机有 Node.js。安装前应先阅读脚本与将写入的 agent 配置，特别是在团队共享规则目录时。

```bash
node ponytail.js -i
```

安装后可在支持 skills 的宿主中使用 `/ponytail` 调整强度，并以 `/ponytail-review`、`/ponytail-audit` 审查当前差异或全仓库。先在非关键仓库试运行，再决定是否把规则写进团队默认配置。

## 原理

它把“先复用、后新增”的决策写成一条七级阶梯：跳过不必要需求，依次检查仓库、标准库、平台、既有依赖与一行实现，最后才编写最小新代码。hook 用于在 agent 生命周期中持续激活这套规则；项目同时声明不应删减验证、错误处理、安全与可访问性。

## 价值

- 将 YAGNI 与依赖复用变成 agent 可执行的检查点，适合减少小功能的额外抽象。
- 提供 diff 与全仓库两种审查入口，便于把“够用即可”的判断留在代码评审链路中。

## 风险边界

- “54% 更少代码、20% 更低成本”等数字来自项目自身的会话样本，尚非跨仓库、可复现的基准结论。
- 极简策略不能替代需求澄清、性能设计、可演进性评估或安全审查；复杂域模型也不应被机械压成一行。
- lifecycle hook 会影响 agent 上下文与行为，应审计其读取范围、配置修改和与既有 hook 的冲突。

## 补充建议

将其当作一次“提出更小方案”的 gate，而非自动否决复杂实现。对每次被拒绝的抽象记录原因，并用测试、可访问性检查和生产指标验证简化没有损失关键约束。

## 参考资料

- GitHub：<https://github.com/0xwilliamortiz/ponytail-improved>
- GitHub API 快照：<https://api.github.com/repos/0xwilliamortiz/ponytail-improved>
