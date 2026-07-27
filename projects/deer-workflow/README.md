# deer-workflow

## 定位

`deer-workflow` 是开源动态工作流 runtime：用 TypeScript 保留编排逻辑，并把语义工作委托给可替换的 agent runtime。

截至 2026-07-27，GitHub API 显示其创建于 2026-07-26，约 143 stars、15 forks；属于高可见度早期信号。

## 用法

用 TypeScript 定义流程、状态和控制分支，再选择适合的 agent runtime 处理语言理解或生成步骤。

## 原理

将确定性的 orchestration 与非确定性的模型推理解耦，便于替换模型、审计状态并测试工作流控制面。

## 价值

- 适合需要可维护业务流程而非单次聊天的 agent 应用。
- 让工作流测试和模型评测可分别进行。

## 风险边界

- runtime 可替换不保证工具语义、输出格式和错误模式一致。
- 分布式状态、重试和幂等性仍需应用层明确实现。

## 补充建议

先为关键节点建立 schema、超时、回滚和人审门槛，再评估多 runtime 的实际兼容性。

## 参考资料

- GitHub：<https://github.com/deerwork-ai/deer-workflow>
