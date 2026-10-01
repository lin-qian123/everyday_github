<!-- markdownlint-disable MD013 -->

# Planning with Files（OthmanAdi/planning-with-files）

> 上游仓库：<https://github.com/OthmanAdi/planning-with-files> · 归类：Agent 框架与技能生态 · 本页基于 2026-10-02 的 GitHub API、README、host integration docs、plugin manifest、security policy、Release 与 LICENSE 静态整理，未安装 hook、读取本机会话或复跑项目方评测。

- 抓取快照：27,249 stars、2,265 forks、7 open issues。
- 热度信号：GitHub Shell Trending 抓取时约 +36 当日 stars。
- 版本与许可：MIT；latest Release / tag 与 Claude plugin manifest 均为 `v3.22.0`。

## 定位

Planning with Files 是给长时程 coding-agent 任务使用的持久计划 Skill / plugin。它把当前任务拆成 `task_plan.md`、`findings.md`、`progress.md`，再通过不同宿主的 lifecycle hook 重注入选定计划，使 `/clear`、compaction、崩溃或换会话后仍能从项目文件恢复执行状态。

## 用法

通用入口是 `npx skills add OthmanAdi/planning-with-files --skill planning-with-files -g`；Claude Code、Codex、Pi、Hermes、OpenCode、DeepSeek Harness 等还有专用 plugin / hook 指南。单任务可在项目根使用三文件；并行任务写入 `.planning/YYYY-MM-DD-slug/` 并由 `.active_plan` 选择。中文和其他语言版本使用独立 Skill 名称。

## 原理

每轮开始时 hook 从 active plan 读取有限上下文并注入模型，tool write 后提醒更新 progress，compaction 前要求落盘，停止阶段检查计划状态。可选 attestation 以 SHA-256 固定计划内容，slug mode 做并行隔离；自动恢复只读项目计划，显式 `session-catchup --metadata` / `--replay` 才会读取同项目的本地 Agent session 记录。

## 价值

三份 Markdown 是可见、可 diff、可人工纠正的工作记忆，降低任务依赖单个 context window 的风险，也让阶段、失败、验证与下一步有稳定交接面。多宿主 adapter 使团队不必为每个 coding agent 重新设计一套计划格式。

## 风险边界

- 计划会被重新放入模型上下文；从网页、issue 或其他不可信来源复制的文字可能形成持久 prompt injection，也可能随宿主模型配置外发。
- hook 运行和 stop / completion gate 会改变 Agent 的每轮行为；版本不匹配、错误 active pointer 或未完成状态可能造成噪声、阻塞或错误恢复。
- 显式 replay 能读取同项目 session 摘要 / 片段；“同项目”不是数据最小化保证，使用前应审查路径、nonce framing 与输出内容。
- SHA attestation 只证明计划未被意外修改，不证明计划正确、安全或仍符合最新用户意图。
- 项目方 96.7% assertion、3 / 3 blind A/B 与 re-orientation turn 数据未由本轮独立复跑，不能泛化到所有 Agent、任务和模型。
- `npx skills add`、plugin marketplace 与后续升级都是高权限供应链入口；MIT 不覆盖宿主、provider、安装器和计划中引用的第三方内容。

## 补充建议

先在无 secret 的测试仓库固定 `v3.22.0`，审阅对应宿主的 hook 与脚本，只启用一种安装路径。对外部内容先摘要 / 标注再写入 findings；将计划文件设为工作态而非事实源，任务关键决策同步到正式文档或 commit。用一次真实 compaction、并行计划、失败恢复和正常结束测试验证不会跨项目读取、不会误阻塞，并记录可随时关闭的开关。

## 参考资料

- [GitHub 仓库](https://github.com/OthmanAdi/planning-with-files)
- [GitHub REST API](https://api.github.com/repos/OthmanAdi/planning-with-files)
- [README 与三文件模式](https://github.com/OthmanAdi/planning-with-files/blob/master/README.md)
- [安装指南](https://github.com/OthmanAdi/planning-with-files/blob/master/docs/installation.md)
- [Codex 集成](https://github.com/OthmanAdi/planning-with-files/blob/master/docs/codex.md)
- [评测说明](https://github.com/OthmanAdi/planning-with-files/blob/master/docs/evals.md)
- [SECURITY](https://github.com/OthmanAdi/planning-with-files/blob/master/SECURITY.md)
- [v3.22.0 Release](https://github.com/OthmanAdi/planning-with-files/releases/tag/v3.22.0)
- [LICENSE](https://github.com/OthmanAdi/planning-with-files/blob/master/LICENSE)
