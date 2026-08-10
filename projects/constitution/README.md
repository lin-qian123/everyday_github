<!-- markdownlint-disable MD013 -->

# constitution（Clanker Constitution）

- 仓库：[kenn-io/constitution](https://github.com/kenn-io/constitution)
- 快照：2026-08-11 抓取；GitHub API 显示其创建于 2026-08-10，约 23 stars、1 fork，CC-BY-4.0。数字会随时间变化。
- 分类：Agent 框架与技能生态

## 定位

一份可版本化的 coding-agent 默认工作原则。它用于为 Codex、Claude Code 等宿主提供一层通用行为约束，并明确用户指令和更具体的仓库指令优先于该文件。

## 用法

可将已审阅、固定版本的 `CONSTITUTION.md` 复制到仓库根目录，再让 `AGENTS.md` 或 `CLAUDE.md` 显式引用它；作者也给出用户级链接方式。应保留原有配置，手工合并规则而非盲目覆盖；下游副本建议固定到 release tag 后按普通 PR 评审更新。

## 原理

该项目把高层行为原则写入独立文本，并以不可变的日历版本 tag 管理演进。其作用类似一份可复核的 policy 输入：宿主自己的指令优先级和加载机制决定了它实际能否生效，文本本身不会提供沙箱、权限拦截或执行隔离。

## 价值

团队能把跨仓库重复的工程纪律集中维护，同时保留仓库局部规则的优先级。固定版本和归因要求也有助于审查“agent 是依据哪套规则工作的”。

## 风险边界

符号链接或用户级规则会影响多个项目；与已有 `AGENTS.md`、安全策略或团队流程冲突时可能改变 agent 行为。CC BY 4.0 要求保留归因；它不等同于安全控制、法律合规或任务结果保证。

## 补充建议

先在单一低风险仓库以固定 tag 试行，明确与本地指令的优先级、冲突处理和升级责任人。不要把远端 `main` 在 agent 启动时自动拉取为运行时规则；将变更纳入 code review，并用真实任务验证规则可执行性。

## 参考资料

- [项目 README 与版本说明](https://github.com/kenn-io/constitution)
- [GitHub API 元数据快照](https://api.github.com/repos/kenn-io/constitution)
