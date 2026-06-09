# andrej-karpathy-skills（forrestchang/andrej-karpathy-skills）

- GitHub: https://github.com/forrestchang/andrej-karpathy-skills
- 记录日期: 2026-04-22 (Asia/Shanghai)

## 这是什么

`andrej-karpathy-skills` 是一个面向 AI 编码助手的“行为约束包”，核心是把 Andrej Karpathy 对 LLM 编码常见失误的观察，收敛成可直接装载到 Claude Code / Codex 等环境的规则与技能文件。

按 GitHub 页面快照（2026-04-22 抓取）约为 `71.5k stars`、`6.5k forks`，属于近期增长非常快的开发者工作流类项目。

## 为什么值得关注

1. 它不是新模型，而是“如何正确使用模型”的工程方法论。
2. 重点解决高频痛点：擅自假设、过度抽象、无关改动、目标不可验证。
3. 可直接落地到团队协作规范，降低 AI 改代码时的返工率与回归风险。

## 怎么用（最短路径）

### 1) Claude Code 插件方式（推荐）

```bash
/plugin marketplace add forrestchang/andrej-karpathy-skills
/plugin install andrej-karpathy-skills@karpathy-skills
```

### 2) 项目级 CLAUDE.md 方式

```bash
curl -o CLAUDE.md https://raw.githubusercontent.com/forrestchang/andrej-karpathy-skills/main/CLAUDE.md
```

已存在 `CLAUDE.md` 的仓库，可改为 append 方式合并。

## 核心原理

1. 先思考再编码（Think Before Coding）
在执行前显式声明假设、不确定性与方案权衡，避免“错误前提上高速执行”。

2. 简单优先（Simplicity First）
约束模型不要为单次需求引入预先抽象，减少“100 行问题写成 1000 行框架”的倾向。

3. 外科式改动（Surgical Changes）
只改与当前任务直接相关的代码，禁止顺手重排、删注释、改邻近逻辑，降低 diff 噪音。

4. 目标驱动执行（Goal-Driven Execution）
把“做什么”改写成“什么算完成”，并用测试/检查命令闭环验证，让 Agent 可自校正。

## 适用场景

1. 团队引入 Codex/Claude Code 后的统一编码护栏。
2. 高频小步迭代项目，减少 AI 引入的隐性技术债。
3. 代码评审压力较大的仓库，用规则前置降低无效改动。

## 价值与风险

价值：
- 低成本提升 AI 编码产出的稳定性。
- 把个人经验转成团队可复用规范。

风险：
- 过严约束可能降低探索式任务速度。
- 规则只管过程，不替代架构判断与业务决策。

## 我认为有价值的补充材料

1. 把四原则映射到 CI（例如：变更范围检查、无关文件改动阻断）。
2. 为仓库补充“任务模板库”（bugfix/refactor/feature）提高可执行性。
3. 在 PR 模板中加入“假设列表 + 验证证据”字段，统一复盘口径。

## 参考来源

- https://github.com/forrestchang/andrej-karpathy-skills
- https://github.com/forrestchang/andrej-karpathy-skills/blob/main/README.md
- https://ossinsight.io/trending
