# ax（Necmttn/ax）

- GitHub: https://github.com/Necmttn/ax
- 文档: https://ax.necmttn.com/docs
- 记录日期: 2026-06-23 (Asia/Shanghai)

## 定位

`ax` 是一个面向 AI coding agent 的本地体验层，重点不在“再包一层聊天 UI”，而是在会话结束前做结构化复盘，把 Claude Code、Codex 等工具的历史会话、技能使用、工具失败、成本和改进建议沉淀进本地知识图谱。

## 热度信号

1. GitHub API 在 2026-06-23 抓取时显示约 `50 stars`、`6 forks`，`updated_at` 为 `2026-06-22T23:21:20Z`。
2. GitHub Trending Developers 的 TypeScript 日榜在 2026-06-23 抓取时把作者 `Necmttn` 的热门仓库标成 `ax`，说明它已经开始被 agent 工程圈注意到。
3. 官方 README 把定位写得很直白：`the agent experience layer`，核心关键词是 `observability + memory for AI coding agents`、`local-first`、`typed graph`。

## 用法

### 1) 先安装 CLI

官方推荐安装方式是：

```bash
curl -fsSL ax.necmttn.com/install | sh
PATH="$HOME/.local/bin:$PATH" ax setup
```

README 也提供了适合直接丢给 Claude Code / Codex 的长提示词，目标是让 agent 自动完成安装、初始 ingest、`doctor` 检查和 skills 分类。

### 2) 导入已有会话与工具历史

项目的主入口不是“立刻问答”，而是先把历史会话导入本地图谱。README 明确提到它会 ingest：

- Claude Code transcript
- Codex transcript
- Pi / OpenCode / Cursor 会话数据
- 已安装 skills
- 本地 git 历史
- GitHub PR、review 与 checks

### 3) 用查询和 dashboard 回看自己的 agent 工作流

常见入口包括：

```bash
ax recall "auth bug"
ax skills taste
ax costs for --branch main
ax sessions metrics
ax serve
```

其中 `ax serve` 会启动本地 dashboard，默认跑在 `127.0.0.1`，把 transcript、成本、friction、改进建议放在同一个本地控制面里。

## 原理

1. 会话结束时通过 hook 触发结构化 retro，把“尝试过什么 / 哪些有效 / 哪些失败 / 下次怎么做”写成本地实验记录。
2. 项目把多种 agent harness 的事件标准化后写入本地 `SurrealDB` 图谱，形成统一的 session、turn、tool call、skill、plan、commit、friction 数据层。
3. 在图谱之上再做 recall、成本统计、routing 建议、skills 加权、improvement proposal 等派生查询。
4. 它强调所有 ingest 和本地分析都运行在本机，只有显式执行分享命令时才会对外发布聚合后的会话摘要。

## 价值

- 它切中的是真实痛点：sub-agent 做完就消失，经验无法复用，下一轮又从头踩坑。
- 对经常并行调度多个 coding agent 的用户，`ax` 提供的是“把经验沉淀为本地工作流资产”的能力，而不是一次性生成结果。
- 如果你正在关注记忆层赛道，`ax` 的差异在于它把“记忆”直接绑定到了 agent 运行成本、失败模式和技能使用效果上。

## 风险边界

- 项目会读取本地 transcript、git 历史和工具调用记录，属于高敏感本地数据；虽强调不出网，但仍应先审阅数据范围。
- 当前热度还早期，星标体量很小，很多结论更适合作为方向观察，而不是稳定生产基座判断。
- 它依赖 hooks、会话采集和图谱建模；如果你的 agent 运行环境非常分散，接入和数据一致性会是首要问题。

## 补充建议

1. 最适合先在个人仓库或单团队环境试用，验证 ingest 成功率、查询可用性和隐私边界。
2. 可以把它与 `codebase-memory-mcp`、`cognee` 一起比较：前者更偏代码知识图谱，后者更偏通用记忆平台，`ax` 则更偏 agent 操作史与复盘层。
3. 真正有价值的指标不是 dashboard 漂不漂亮，而是它能不能减少重复失败、降低高价模型浪费和改进子任务调度质量。

## 参考资料

- https://github.com/Necmttn/ax
- https://ax.necmttn.com/docs
- https://github.com/trending/developers/typescript?since=daily
