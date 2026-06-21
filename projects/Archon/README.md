# Archon（coleam00/Archon）

- GitHub: https://github.com/coleam00/Archon
- 官网: https://archon.diy
- 文档: https://archon.diy/docs/
- 记录日期: 2026-06-21 (Asia/Shanghai)

## 定位

`Archon` 是一个面向 coding agent 的工作流引擎，主打把计划、实现、验证、评审、PR 创建等开发步骤写成可重复执行的 YAML 工作流。它关心的不是“再做一个聊天代理”，而是让 AI 编程流程变得可编排、可复现、可并行。

## 热度信号

1. GitHub API 在 2026-06-21 抓取时显示约 `22.5k stars`、`3.4k forks`，`updated_at` 为 `2026-06-21T00:13:55Z`。
2. GitHub Trending Developers 的 TypeScript 榜单在 2026-06-21 抓取时把 `Archon` 作为热门仓库之一展示。
3. 官方 README 直接写出 `The first open-source harness builder for AI coding`，并把自己类比为 “AI coding workflows 的 Dockerfile + GitHub Actions”。

## 用法

### 1) 用 YAML 定义工作流

README 展示的核心模式是把开发过程写入 `.archon/workflows/*.yaml`：

```yaml
nodes:
  - id: plan
    prompt: "Explore the codebase and create an implementation plan"
  - id: implement
    depends_on: [plan]
    loop:
      prompt: "Read the plan. Implement the next task. Run validation."
      until: ALL_TASKS_COMPLETE
      fresh_context: true
  - id: run-tests
    depends_on: [implement]
    bash: "bun run validate"
```

### 2) 把验证和 AI 节点混编

它支持在同一流程中混合 bash、测试、代码审查和 AI 节点，不必把所有阶段都交给模型自由发挥。

### 3) 并行运行任务

README 明确强调每次运行使用独立 git worktree，适合并行处理多个任务。

## 原理

1. 它把 agent 的“智能部分”和“流程约束部分”拆开，让流程由工作流控制，模型只在需要推理的位置介入。
2. 通过 loop、approval gate、validation step 这些机制，减少一次性 prompt 驱动下的随机性。
3. 从其工作流结构看，它更接近开发流水线引擎，而不是单纯的聊天式开发助手。

## 价值

- 对希望把 AI 编码工作流程标准化的团队，它比纯 CLI 助手更接近组织级工程工具。
- 它很适合“一个 repo 里反复执行相似任务”的场景，比如 bugfix、代码审查、PR 生成和验证流程。
- 它代表了一个明显趋势：大家开始不再满足于“模型厉害”，而是要把 agent 纳入确定性工程流水线。

## 风险边界

- 工作流越强，前期设计成本越高，不适合把每个一次性探索任务都硬塞进 YAML。
- 使用独立 worktree、循环节点和审批节点后，仓库权限、资源占用和失败恢复都需要额外治理。
- 它提升的是流程可控性，不自动保证代码质量；验证脚本和规则本身仍要由团队维护。

## 补充建议

1. 初次使用时先固化最稳定的两个流程，例如“修 bug + 跑测试”和“需求实现 + PR 说明”，不要一次铺太宽。
2. 若团队已经有 CI、PR 模板和评审规范，应优先把 Archon 接到既有约束上，而不是平行重建一套流程。
3. 评估重点不应只看成功率，还应看失败时是否易于回滚、复跑和审计。

## 参考资料

- https://github.com/coleam00/Archon
- https://archon.diy
- https://archon.diy/docs/
- https://github.com/trending/developers/typescript
