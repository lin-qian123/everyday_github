# caveman（JuliusBrussee/caveman）

- GitHub: https://github.com/JuliusBrussee/caveman
- 记录日期: 2026-04-22 (Asia/Shanghai)

## 这是什么

`caveman` 是一个面向 Claude Code、Codex 等 Agent 编码环境的“输出压缩技能”，通过极简表达风格减少 token 消耗，同时尽量保持技术信息不丢失。

按 GitHub 页面快照（2026-04-22 抓取）约为 `42.3k stars`、`2.2k forks`，是近期非常高热的“AI 协作效率优化”工具。

## 为什么值得关注

1. 它抓住了 AI 编码成本结构里的核心变量：`输出 token`。
2. 不是优化模型本身，而是优化交互协议，迁移成本低。
3. 可作为“速度档位”工具：需求澄清用详细模式，执行反馈用压缩模式。

## 怎么用（最短路径）

### 1) Claude Code

```bash
claude plugin marketplace add JuliusBrussee/caveman && claude plugin install caveman@caveman
```

### 2) Codex

在 Codex 插件界面安装本地/仓库插件后，按项目规则触发 `$caveman`（或对应命令）进入压缩模式。

### 3) 通用技能安装（多 Agent）

```bash
npx skills add JuliusBrussee/caveman
```

## 核心原理

1. 语义保留、语言压缩
去掉寒暄、填充词与冗余过渡，用短句表达同样的技术决策与操作步骤。

2. 答案密度最大化
把“背景叙述”转成“结论 + 动作 + 验证”的结构，提升单位 token 信息量。

3. 可分级强度
通常提供 lite/full/ultra 之类强度档位，平衡可读性与压缩比。

4. 与自动化链路兼容
可结合 commit/review 辅助命令，把压缩策略扩展到 PR 描述、变更说明和日常协作文本。

## 适用场景

1. 长会话开发任务，控制上下文成本。
2. 多 Agent 并行时，减少状态同步文字开销。
3. 批量修复任务中的进度回报与验收摘要。

## 价值与风险

价值：
- 降低 token 消耗与交互延迟。
- 对既有工程流程侵入小，易试点。

风险：
- 信息过度压缩时，可能损失关键约束细节。
- 新成员阅读门槛上升，需要统一术语约定。

## 我认为有价值的补充材料

1. 建立“双通道输出”规范：默认压缩，关键设计节点自动切回详细说明。
2. 对高风险任务启用“强制详细模式 + 检查清单”。
3. 跟踪压缩前后指标：token、回合数、误解率、返工率。

## 参考来源

- https://github.com/JuliusBrussee/caveman
- https://github.com/JuliusBrussee/caveman/blob/main/README.md
- https://www.producthunt.com/products/caveman-claude-code-skill-plugin
- https://ossinsight.io/trending
