# codebase-memory-mcp（DeusData/codebase-memory-mcp）

- GitHub: https://github.com/DeusData/codebase-memory-mcp
- 官网: https://deusdata.github.io/codebase-memory-mcp/
- 记录日期: 2026-06-18 (Asia/Shanghai)

## 定位

`codebase-memory-mcp` 是一个面向 AI coding agent 的本地代码智能与持久记忆层。它把代码仓库索引成可查询的知识图谱，并通过 MCP 暴露给 Claude Code、Codex、Gemini CLI、Aider、OpenCode 等工具，用来替代反复 `grep + read file` 的低效逐文件探索流程。

## 热度信号

1. GitHub API 在 2026-06-18 抓取时显示约 `5.3k stars`、`489 forks`。
2. GitHub 通用 Trending 页面在 2026-06-18 抓取时出现该项目，说明“代码记忆层 / MCP 代码索引”已经从小众技巧走向热点基础设施。
3. 官方 README 把卖点直接写成 `persistent knowledge graph`、`14 MCP tools`、`158 languages`、`single static binary`，定位非常明确，不是普通代码搜索脚本。

## 用法

### 1) 直接安装预编译二进制

官方提供 macOS、Linux、Windows 的静态二进制包，也提供带图谱 UI 的变体。

### 2) 用官方脚本安装

```bash
curl -fsSL https://raw.githubusercontent.com/DeusData/codebase-memory-mcp/main/scripts/setup.sh | bash
```

安装后按 README 指引执行 `install`，它会自动检测并写入多个 agent 的 MCP 配置。

### 3) 交给 agent 接入

项目 README 直接给出自然语言安装方式，例如让 Claude Code 安装该 MCP server。接入完成后，agent 就能通过结构化查询访问仓库知识图谱，而不是只靠文件名搜索。

## 原理

1. 用 `tree-sitter` 对多语言仓库做 AST 级结构解析，并构建函数、类、调用链、HTTP 路由和跨服务链接等图谱关系。
2. 对部分语言加入 Hybrid LSP 语义类型解析，补强单纯语法树不够表达的类型和符号信息。
3. 把索引结果持久化为本地图存储，并通过 `14` 个 MCP 工具暴露给 agent。
4. 项目强调“静态二进制 + 零运行时依赖 + 本地处理”，目标是把接入成本压到极低，同时避免代码离开本机。

## 价值

- 对大型仓库、单体仓库和多服务仓库特别有价值，因为 agent 最常见的浪费就在盲目翻文件和重复读取上下文。
- 它代表一种更工程化的 agent 增强路径：不是只升级模型，而是给模型一个稳定、可复用、可缓存的仓库认知层。
- 如果官方给出的 benchmark 趋势大致成立，这类工具能同时改善 token 消耗、工具调用次数和定位速度。

## 风险边界

- 项目会读取代码仓库并修改 agent 配置文件，这本身就是高权限操作，正式接入前应先审阅安装脚本与配置变更范围。
- README 中的速度、token 节省和回答质量数据来自作者论文预印本与自建评测，适合当方向性证据，不应直接当作你自己仓库的生产结论。
- “统一知识图谱”也会带来索引过期、误链接和大仓库增量同步成本等现实问题，不能假设它天然完全正确。

## 补充建议

1. 先在一个中型真实仓库做对照试验，比较启用前后的 token、定位时间和误判率，再决定是否大范围接入。
2. 若团队同时使用多个 agent，优先把它当共享代码认知底座，而不是只给某一个 CLI 独占。
3. 对安全敏感仓库，保留“只允许本地索引、不允许额外联网、不自动改全局配置”的审计策略。

## 参考资料

- https://github.com/DeusData/codebase-memory-mcp
- https://deusdata.github.io/codebase-memory-mcp/
- https://arxiv.org/abs/2603.27277
- https://github.com/trending
