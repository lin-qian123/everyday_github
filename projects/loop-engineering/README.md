# loop-engineering

## 1. 项目定位

`loop-engineering` 是一个面向 AI coding agent 的 loop 工程模式、脚手架和 CLI 工具集合。它关注的不是“再写一个 agent”，而是把 agent 工作循环设计成可审计、可评分、可复用的系统：包括初始化 agent loop、检查预算、审计准备度、同步状态和选择适合当前工具的工作模式。

它适合已经在使用 Claude Code、Codex、Cursor、opencode、Grok 等工具的开发者和团队，用来把零散 prompt 迁移为有状态、有检查点、有成本边界的工程流程。

## 2. 基本用法

官方 README 给出的快速入口是直接在项目中运行初始化命令：

```bash
npx @cobusgreyling/loop-init .
```

`loop-init` 会生成 skills、state、budget 等文件，并输出 Loop Ready 分数和下一步 loop 命令。项目还提供 `loop-audit`、`loop-cost`、`loop-sync` 等 npm 包，用于审计当前 loop 成熟度、检查成本假设和同步状态。

## 3. 核心原理

项目把 agent 工作流拆成几个工程构件：

- 用 `loop-init` 建立项目级 agent loop 骨架，而不是每次临时写 prompt。
- 用 `loop-audit` 给仓库、技能、状态文件和预算配置打分，暴露缺口。
- 用 `loop-cost` 把 token 和运行预算显式化，避免 agent 长任务失控。
- 用模式库和交互式 picker 帮助用户选择适合当前任务的 loop 结构。
- 面向多种 coding agent 输出适配建议，让同一套 loop 约束可迁移到不同 harness。

这类思路的核心是把“人反复催促 agent”替换成“系统持续提示、检查和约束 agent”。

## 4. 工程价值

`loop-engineering` 的价值在于把 2026 年 coding agent 的经验沉淀成可复用操作层。随着 agent 能跑更久、能改更多文件，真正稀缺的不是单次代码生成，而是稳定的目标、状态、成本、验收和回滚边界。

对本仓库的长期跟踪而言，它和 `awesome-harness-engineering`、`ponytail`、`testsprite-cli` 属于同一条线：从“工具能力”走向“agent harness 工程实践”。它的高星增长说明开发者开始关心如何组织 agent 工作，而不只是选择哪个模型。

## 5. 风险边界

- 项目提供的是 loop 设计和脚手架，不保证 agent 输出一定正确。
- 审计分数只能发现流程缺口，不能替代测试、安全评审和人工验收。
- 成本估算依赖模型价格、缓存命中率和实际任务形态，不能照搬到所有团队。
- 如果把生成的 skills 和状态文件无审查地接入生产仓库，仍可能扩大 agent 的误操作面。

## 6. 补充建议

- 先在非关键仓库运行 `loop-init`，观察生成文件是否符合团队现有 `AGENTS.md` / `README.md` / `TODO.md` 约定。
- 把 `loop-audit` 输出当作 checklist，而不是最终质量结论。
- 与 `testsprite-cli`、`security-audit-skill` 等验证型工具组合时，应明确谁负责发现问题、谁负责验证问题、谁负责最终合并。
- 后续重点观察它是否能沉淀稳定的 loop pattern，而不是只停留在概念传播。

## 7. 参考资料

- GitHub 仓库：https://github.com/cobusgreyling/loop-engineering
- 项目展示页：https://cobusgreyling.github.io/loop-engineering/
- npm 包：`@cobusgreyling/loop-init`、`@cobusgreyling/loop-audit`、`@cobusgreyling/loop-cost`
- 相关讨论入口：https://addyosmani.com/blog/loop-engineering/
