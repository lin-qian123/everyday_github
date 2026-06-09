# claude-code-best-practice（shanraisshan/claude-code-best-practice）

- GitHub: https://github.com/shanraisshan/claude-code-best-practice
- 记录日期: 2026-04-23 (Asia/Shanghai)

## 这是什么

`claude-code-best-practice` 是一个面向 Agent 工程化落地的实践仓库，核心是把“命令（Commands）-子代理（Subagents）-技能（Skills）”组织成可复用工作流，帮助团队从零散的提示词使用，迁移到可维护的协作流程。

## 热度信号

1. OSSInsight 趋势快照显示该项目处于近期上升区间，星标信号约 `2.1k`、fork 约 `140`。
2. 仓库目录覆盖 `.claude`、`.codex`、`agent-teams`、`development-workflows` 等模块，说明其定位偏“方法论 + 参考实现”。

## 怎么用（最短路径）

### 1) 克隆并阅读总览

```bash
git clone https://github.com/shanraisshan/claude-code-best-practice.git
cd claude-code-best-practice
```

先看 `README.md` 与 `CLAUDE.md`，明确仓库的角色分层。

### 2) 先复用再改造

优先挑一条现成工作流（例如命令编排示例）在你的仓库复制试运行，再按团队习惯改写提示模板与权限边界。

### 3) 把“可执行约束”前置

把代码规范、测试门槛、审阅要求写入命令/技能入口，减少任务执行中的语义歧义。

## 核心原理

1. 将“流程知识”从个人经验转成仓库资产。
2. 用命令模板做入口编排，用子代理隔离上下文，用技能沉淀稳定操作。
3. 通过文件结构把“会话行为”映射到“可版本化配置”。

## 适用场景

1. 团队想统一 AI 开发协作规范。
2. 复杂任务需要拆分角色并行推进。
3. 需要复盘和审计 Agent 的执行路径。

## 价值与风险

价值：
- 让 AI 协作从“临场发挥”转向“标准流程”。
- 新成员可以更快复用既有实践。

风险：
- 过度模板化可能抑制探索型任务效率。
- 若不定期维护，规则会与真实项目演进脱节。

## 我认为有价值的补充材料

1. 建立“失败样例库”，记录哪些任务不适合强编排。
2. 给每条工作流定义 DORA 风格指标（交付时长、返工率等）。
3. 将关键规则同步到 CI 检查，避免只停留在文档层。

## 参考来源

- https://github.com/shanraisshan/claude-code-best-practice
- https://github.com/shanraisshan/claude-code-best-practice/blob/main/CLAUDE.md
- https://ossinsight.io/trending
