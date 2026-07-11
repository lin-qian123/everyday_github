# loopy

<!-- markdownlint-disable MD013 -->

## 定位

`loopy` 是 Forward Future 的 AI-agent loop library 与 installable skill。它关注的不是“单次 prompt 怎么写”，而是把可重复执行、可度量、可复盘的工作流程写成 loop，让 agent 根据反馈继续下一步。

截至 2026-07-12，GitHub API 显示该仓库约 2649 stars、226 forks，创建于 2026-06-12，许可证为 MIT。README 将仓库拆成两部分：公开 Loop Library 网站，以及可安装的 Loopy skill。

## 用法

不安装也可以直接让 agent 读取公开目录：

- Agent guide：<https://signals.forwardfuture.com/loop-library/agents/>
- `llms.txt`：<https://signals.forwardfuture.com/loop-library/llms.txt>
- JSON catalog：<https://signals.forwardfuture.com/loop-library/catalog.json>
- Text catalog：<https://signals.forwardfuture.com/loop-library/catalog.txt>

安装 Loopy skill 后，agent 可按向导发现、审计、修复、设计、运行、复盘和发布 loop。

## 原理

loop 是带反馈的 playbook。它通常回答四个问题：目标是什么、如何判断本轮是否有效、下一步如何利用反馈、什么时候停止。相比一次性提示词，loop 更适合性能优化、测试覆盖、生产事故、文档更新、产品评审等需要多轮收敛的任务。

Loopy skill 的作用是帮助 agent 在 loop catalog 中选择或改写流程，而不是直接替代测试和业务判断。

## 价值

- 把 agent 工作从“凭感觉多试几次”变成有停止条件的重复流程。
- 适合和 `loopkit`、`loop-engineering`、`awesome-harness-engineering` 横向比较。
- 可公开浏览目录，便于团队在不安装工具的情况下先评审流程质量。
- 对每日自动化这类重复任务有启发：每次运行后应写入反馈和下次观察点。

## 风险边界

- loop 质量取决于停止条件和度量设计，弱指标会让 agent 重复无效动作。
- skill 本身不能保证 agent 遵守权限边界，仍需宿主工具的 sandbox 和审批。
- 公开 catalog 的内容会更新，生产流程最好 pin 到具体版本或复制到仓库内。

## 补充建议

- 用它整理“每日热点抓取 -> 去重 -> 建档 -> 验证 -> 推送”的自动化闭环。
- 与 `self-learning-skills` 搭配观察：一个偏流程目录，一个偏从会话沉淀经验。
- 若引入团队，先从低风险流程开始，如文档更新、测试补齐和 issue triage。

## 参考资料

- GitHub 仓库：<https://github.com/Forward-Future/loopy>
- Loop Library：<https://signals.forwardfuture.com/loop-library/>
- Agent guide：<https://signals.forwardfuture.com/loop-library/agents/>
