<!-- markdownlint-disable MD013 -->

# improve：让强模型调查代码，把计划交给执行者

- 上游：[`shadcn/improve`](https://github.com/shadcn/improve)；仓库 ID：`1264986626`。
- 核读：2026-11-12（Asia/Shanghai）；主线固定于 [`cac56e1ebd3c`](https://github.com/shadcn/improve/tree/cac56e1ebd3c279aa9153616cfeac7b174ab90f9)。
- 热度快照：10,810 stars / 441 forks / 18 open issues（含 PR）；来自 [GitHub API](https://api.github.com/repos/shadcn/improve)，不代表采用量或质量。

## 定位

一个 Agent Skills 格式的代码顾问技能。它把理解仓库、筛选问题、写自包含实施计划交给较强模型，再把具体改动交给其他模型或人。默认产物是 Markdown 计划，并非新的模型、独立 CLI 或自动发布系统。当前技能元数据为 1.0.0，发行列表为空；今天在官方综合 daily 页 +333。

## 用法

上游安装命令（本轮未执行）：

```bash
npx skills add shadcn/improve
```

在支持 Agent Skills 的宿主中运行 `/improve quick` 做有限扫描，或 `/improve branch` 只看当前分支；完整审查用 `/improve`。先看 findings，再选择要展开的计划。默认写入 `plans/`；若该目录已有其他用途，改用 `advisor-plans/`。

后续可用 `/improve review-plan <file>` 收紧验收标准，`/improve reconcile` 检查旧计划漂移。`/improve execute <plan>` 会另行调度执行者，不再只是写计划；`--issues` 还会创建 GitHub issue，使用前须明确授权外部写入。

## 原理

流程是仓库摸底 → 按正确性、安全、性能、测试、架构等类别审查 → 顾问重读引用位置、剔除误报 → 按影响、成本和置信度排序 → 写计划。计划包含当前 SHA、范围、依赖、实际验证命令和停止条件，目标是让没有聊天上下文的执行者也能接续。

顾问禁止修改源码，但允许写计划文件；这是一条提示词规则。`execute` 使用独立 Git worktree 中的执行者，顾问重跑验收、看完整 diff 与测试有效性，再给 APPROVE / REVISE / BLOCK；最多两轮返修。上游规定顾问不把结果合并、推送或提交到用户分支。

## 价值

适合代码已能运行、但需要判断下一步做什么或如何交接的仓库。比起一条泛化建议，自包含计划、拒绝原因和漂移检查更利于审阅，也能让高成本调查供多次实施复用。

“强模型规划、便宜模型执行”是作者提出的成本策略；本轮没有同条件费用、耗时或修复正确率实验，不能保证总成本降低。

## 风险边界

- 技能文字不能强制只读、限制 shell 或形成 OS 隔离；真正权限取决于宿主。Git worktree 只隔离工作文件，不隔离凭据、网络或进程。
- 静态 findings、置信度和测试通过各有边界；顾问与执行者可能共享错误假设，模型间换手也可能增加返工。
- 上游明确把被审仓库内容当数据，并禁止复制 secret 值。仍需限制可读范围，审查计划中的代码摘录和外发内容。
- 漂移检查和依赖门控会阻止某些旧计划执行；不能为了让状态变 DONE 而弱化验收或绕过停止条件。
- 许可为 MIT；模型服务、安装器及被审仓库有各自的许可和数据处理规则。

## 补充建议

先选一个能复现的小问题，检查计划是否包含可失败的验收、准确的文件位置、依赖顺序和当前 SHA。记录调查、执行、返修的实际费用，再比较直接实现的基线。对安全结论补独立验证，对较小文档修改避免全仓重审。

本页为固定文件静态核读；未安装技能、调度模型或执行仓库审计。

## 参考资料

- [README 与命令](https://github.com/shadcn/improve/blob/cac56e1ebd3c279aa9153616cfeac7b174ab90f9/README.md)。
- [技能规则](https://github.com/shadcn/improve/blob/cac56e1ebd3c279aa9153616cfeac7b174ab90f9/skills/improve/SKILL.md)。
- [执行、返修与漂移处理](https://github.com/shadcn/improve/blob/cac56e1ebd3c279aa9153616cfeac7b174ab90f9/skills/improve/references/closing-the-loop.md)。
- [计划模板](https://github.com/shadcn/improve/blob/cac56e1ebd3c279aa9153616cfeac7b174ab90f9/skills/improve/references/plan-template.md)。
- [MIT 许可](https://github.com/shadcn/improve/blob/cac56e1ebd3c279aa9153616cfeac7b174ab90f9/LICENSE.md)。
