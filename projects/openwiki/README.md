# openwiki

<!-- markdownlint-disable MD013 -->

## 定位

`openwiki` 是 LangChain 发布的代码库 / 个人知识库文档生成 CLI。它的目标不是再做一个聊天式问答入口，而是把 agent 需要反复读取的项目说明、目录结构、设计背景和外部知识源整理成可落盘、可持续更新的 wiki。

截至 2026-07-12，GitHub API 显示该仓库约 10564 stars、717 forks，创建于 2026-06-22，许可证为 MIT。README 明确区分两种模式：`personal` 用于本地个人 brain wiki，`code` 用于当前代码库的 `openwiki/` 文档。

## 用法

安装：

```bash
npm install -g openwiki
```

初始化个人知识库：

```bash
openwiki personal --init
```

初始化代码库文档：

```bash
openwiki code --init
```

在 CI 中可使用 `openwiki code --update --print`，配合 GitHub Actions 或 GitLab CI 自动提出文档更新 PR。

## 原理

openwiki 把“给 agent 的长期上下文”从聊天历史里抽出来，写成仓库内或本地目录内的 wiki。它支持本地仓库、git 仓库，以及 Gmail、Notion、Web Search、Hacker News、X/Twitter 等个人来源，最终让 agent 读取结构化 Markdown，而不是每次从零扫描原始资料。

它的工程价值在于把文档维护变成可重复任务：agent 可以根据代码和知识源更新 wiki，开发者再审查 diff。

## 价值

- 适合大型仓库把 onboarding、架构说明和变更背景整理成 agent 可读文档。
- 与 `AGENTS.md`、`README.md`、`TODO.md` 互补：前者偏执行规则，openwiki 偏可更新知识图谱。
- CI 更新模式适合把文档漂移显式变成 PR。
- LangChain 维护背景和较高星数让它成为“agent 文档层”今天的强信号项目。

## 风险边界

- 生成文档仍需人工审查，不能直接视为权威架构说明。
- 连接 Gmail、Notion、X 等个人来源时，需先明确凭据、隐私和数据保留边界。
- 对小项目可能过重；简单项目继续维护 README / TODO 更直接。
- Windows / Bun 安装路径涉及原生依赖构建，团队落地前应固定安装方式。

## 补充建议

- 与 `codebase-memory-mcp`、`memsearch` 区分：openwiki 更偏“写文档”，后两者更偏“检索记忆”。
- 可作为每日自动化仓库的长期候选：把热点项目页、日报和 TODO 汇总成机器可读知识层。
- 建议先在文档不足的大仓库试用，而不是在已有成熟 docs 体系中全量替换。

## 参考资料

- GitHub 仓库：<https://github.com/langchain-ai/openwiki>
- GitHub Actions 示例：<https://github.com/langchain-ai/openwiki/blob/main/examples/openwiki-update.yml>
- LangChain：<https://www.langchain.com/>
