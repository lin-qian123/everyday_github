# ConferenceWatch

- GitHub：<https://github.com/Zsun79/ConferenceWatch>
- 抓取时间：2026-07-05（Asia/Shanghai）
- 今日信号：GitHub API 显示该仓库创建于 2026-07-02，抓取时约
  `122 stars / 0 forks`，README 定位为跟踪 AI/ML 会议 deadline 的 Agent Skill。

## 定位

`ConferenceWatch` 是一个给 Codex、Claude Code 等 agent 使用的会议跟踪 skill。
它让 agent 按固定流程搜索 AI/ML 会议 deadline、地点、special session、
call for papers、官方链接和近五年录用率趋势，并输出结构化 JSON 与 Markdown 报告。

它不是会议数据库本体，而是一个“让 agent 正确查会议”的工作流包。

## 用法

README 推荐把仓库安装到 agent 的 skills 目录：

```bash
git clone https://github.com/Zsun79/ConferenceWatch.git ~/.codex/skills/conference-watch
```

或安装到 Claude skills 目录：

```bash
git clone https://github.com/Zsun79/ConferenceWatch.git ~/.claude/skills/conference-watch
```

使用时可直接询问：

- 未来 6 个月 NLP 顶会 deadline。
- 跟踪 NeurIPS、ICML、ICLR 2026。
- 比较 CV 顶会地点、截稿和 special sessions。

## 原理

该 skill 要求 agent 生成两类产物：

1. `conferences.<date>.json`：结构化事实源，按会议 acronym 存储 deadline、
   location、special sessions、links 和 acceptance-rate trend。
2. `conference-report.<date>.md`：面向人阅读的报告，包含最近 deadline 表、
   单会议信息和单独标出的 approximate / inferred 内容。

仓库还提供 JSON schema、会议 catalog 和报告模板，以减少 agent 临时发挥。

## 价值

- 对研究者：把会议信息查询从散乱网页搜索变成可复核报告。
- 对实验室和学生：适合做定期 deadline digest 或投稿规划。
- 对 agent skill 生态：展示了“领域任务 + schema + 模板 + 不确定性标注”的实用封装方式。

## 风险边界

- 会议 deadline 会频繁变化，必须以官方 CFP / OpenReview / 会议官网为最终准据。
- 录用率趋势常来自历史页面或第三方整理，缺失年份需要明确标注。
- 该 skill 依赖宿主 agent 的 web search / fetch 能力；没有联网能力时无法保证新鲜度。
- 研究者不能只依赖 agent 汇总，关键投稿节点仍应人工复核。

## 补充建议

- 可与 `academic-research-skills`、`scientific-agent-skills`、`open-science`
  一起观察，判断科研 agent 是否会从“写作辅助”扩展到“流程跟踪”。
- 如果用于实验室内部，应把常投会议列表固化到本地 catalog，并保存每次报告的证据链接。
- 后续关注它是否加入自动更新、差异检测和日历导出。

## 参考资料

- GitHub 仓库：<https://github.com/Zsun79/ConferenceWatch>
- Skill 入口：<https://github.com/Zsun79/ConferenceWatch/blob/main/SKILL.md>
- JSON schema：<https://github.com/Zsun79/ConferenceWatch/blob/main/references/json-schema.md>
