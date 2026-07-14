<!-- markdownlint-disable MD013 MD034 -->

# graphiti

`getzep/graphiti` 是 Zep 团队开源的 temporal context graph 引擎，用于为 AI agents 构建会随时间变化的上下文图谱。它强调事实的时间有效性、来源 provenance、增量更新和混合检索。

- GitHub：https://github.com/getzep/graphiti
- 文档：https://help.getzep.com/graphiti
- 论文：https://arxiv.org/abs/2501.13956
- 分类：RAG、检索与知识处理
- 许可证：Apache-2.0

## 热度信号

- 2026-07-15 通过 GitHub API 抓取时约 `28.7k stars`、`2.9k forks`。
- 仓库在 2026-07-09 仍有 push，topics 包含 `agents`、`graph`、`llms`、`rag`。
- README 提示新增 Graphiti MCP server，可给 Claude、Cursor 等 MCP client 提供基于 context graph 的 memory。

## 定位

Graphiti 不是传统“文档切块 + 向量 top-k”的 RAG。它试图把 agent 交互、结构化数据、非结构化数据和外部信息持续写入图谱，并记录事实何时成立、何时被更新、来自哪里。

适合的问题是：

- 用户偏好、组织关系、项目状态会变化。
- agent 需要知道“当前事实”和“历史事实”的区别。
- 检索结果需要 provenance，而不是只返回相似文本片段。

## 用法

使用方式通常包括：

1. 安装 Graphiti Python 包或部署其服务组件。
2. 把交互、文档、业务记录等作为 episodes 写入。
3. 让 Graphiti 抽取 entities、relationships、facts 和时间窗口。
4. 通过语义、关键词和图遍历混合查询上下文。
5. 通过 MCP server 把图谱记忆接入支持 MCP 的 agent 客户端。

具体命令应以仓库和文档的当前版本为准。

## 原理

Graphiti 的关键概念包括：

- entities：人物、产品、政策、概念等节点。
- facts / relationships：带时间有效窗口的关系边。
- episodes：原始输入数据，是后续事实的来源依据。
- ontology：可由开发者定义，也可由系统学习。
- hybrid retrieval：组合语义检索、关键词检索和图遍历。

相比静态知识图谱，它更关注“事实变化”和“上下文连续性”。

## 价值

- 对长期运行 agent，能减少只靠聊天历史或向量库带来的上下文漂移。
- 对企业场景，provenance 和时间窗口有助于审计。
- 对个性化 agent，可以保留用户偏好演化，而不是覆盖成单一摘要。
- 对 GraphRAG 研究，是一个可运行的工程实现样本。

## 风险边界

- 图谱抽取质量仍依赖模型和 schema，错误事实会被结构化放大。
- 时间有效性很有价值，但也会增加写入和查询复杂度。
- 图数据库和检索栈的运维成本高于普通向量库。
- 个人记忆场景要特别注意隐私、删除权和敏感事实误抽取。

## 补充建议

- 先在一个明确领域试点，如客户支持、项目知识库或个人偏好记忆。
- 为抽取结果保留人工校验和纠错入口。
- 对高风险事实保留原文引用，不只信结构化三元组。
- 与 `mem0`、`mempalace`、`codebase-memory-mcp`、`cognee` 对比时，重点看是否需要时间图谱。

## 参考资料

- GitHub 仓库：https://github.com/getzep/graphiti
- Graphiti 文档：https://help.getzep.com/graphiti
- Graphiti MCP server：https://github.com/getzep/graphiti/tree/main/mcp_server
- arXiv：https://arxiv.org/abs/2501.13956
