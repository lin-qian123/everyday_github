<!-- markdownlint-disable MD013 -->

# bridgebench

## 定位

`bridge-mind/bridgebench` 是一个面向 vibe coding 模型的 benchmark 与排行榜项目。它不只比较单题代码补全，而是把真实工程任务、上下文材料、模型回答、盲评和 Elo 更新组织成可复核的 arena。

## 用法

仓库提供无需 API key 的审查路径：

```bash
git clone https://github.com/bridge-mind/bridgebench.git
cd bridgebench
npm ci
npm run review
```

`npm run review` 会检查文档链接、验证公开任务 pack、验证示例 journal line，并回放多数票与 Elo 更新机制。

## 原理

BridgeBench 把每个工程场景包装为任务，任务材料可包括源码、diff、CI 日志、API spec、迁移、遥测和 agent session。模型在同一任务上 head-to-head，三名独立模型 judge 盲评，最终结果写入 append-only match journal，leaderboard 和 API 只是派生视图。

## 价值

- 关注 agent / coding model 在工程语境中的表现，而不是孤立算法题。
- 提供可审查 journal，有利于降低“排行榜只给结论”的黑箱问题。
- 对团队选型、模型回归测试和 prompt/harness 评估有参考价值。
- 与近期“只看 SWE-Bench 不够”的讨论方向一致。

## 风险边界

- 模型 judge 仍然可能有偏差，三 judge 多数票不是人类真实验收。
- vibe coding 定义较宽，需要看具体任务覆盖是否代表目标团队工作。
- 公开 synthetic fixture 只能验证审查机制，不能证明模型质量。
- 排行榜可能随私有任务、付费 match 和 judge 配置变化而波动。

## 补充建议

- 使用时不要只看 Elo，必须抽样审查 journal 和任务说明。
- 将自家真实任务转成内部 benchmark，比直接套用公开榜单更可靠。
- 关注是否引入人类审查、任务难度分层和失败案例分类。

## 参考资料

- GitHub: <https://github.com/bridge-mind/bridgebench>
- Leaderboard: <https://bridgebench.ai>
- Vibe Code Bench paper: <https://arxiv.org/abs/2603.04601>
