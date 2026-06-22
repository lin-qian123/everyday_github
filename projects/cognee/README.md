# cognee（topoteretes/cognee）

- GitHub: https://github.com/topoteretes/cognee
- 官网: https://www.cognee.ai
- 文档: https://docs.cognee.ai/
- 论文: https://arxiv.org/abs/2505.24478
- 记录日期: 2026-06-22 (Asia/Shanghai)

## 定位

`cognee` 是一个面向 agent 的开源记忆平台，核心目标是把文档、工具调用和会话上下文持续沉淀为可查询的长期记忆，而不是只在一次提示词窗口里临时拼上下文。

## 热度信号

1. GitHub API 在 2026-06-22 抓取时显示约 `18.6k stars`、`2.0k forks`，`updated_at` 为 `2026-06-22T01:01:29Z`。
2. GitHub Trending Python 榜单在 2026-06-22 抓取时出现 `cognee`。
3. 官方 README 把项目直接定义为 `The Open-Source AI Memory Platform for Agents`，并强调 `persistent long-term memory`、`self-hosted knowledge graph`、`vector embeddings` 与 `graph reasoning`。

## 用法

### 1) 先安装 SDK

README 给出的最直接入口是：

```bash
uv pip install cognee
```

然后配置 `LLM_API_KEY` 等环境变量。

### 2) 把信息写入长期记忆

README 的核心示例是：

```python
import cognee

await cognee.remember("Cognee turns documents into AI memory.")
results = await cognee.recall("what happened?")
```

它同时支持会话记忆和持久图谱记忆。

### 3) 用 Docker 或 MCP 方式接到 agent

README 提供了 `docker compose up`、`cognee/cognee-mcp` 容器、Claude Code 插件和 MCP 服务入口，说明它并不只想做 Python 库，而是想成为 agent 记忆底座。

## 原理

1. 它把非结构化输入持续转换成图谱化、向量化的知识表示，让 agent 可以按语义和关系双路径检索。
2. 会话级短期记忆与后台同步的长期图谱结合，试图解决“当前对话记得住，跨会话就忘掉”的问题。
3. 从 README 和论文入口看，它强调的不只是检索召回，还包括知识关系建模和随知识增长而演化的本体结构。

## 价值

- 对长期运行的 coding agent、研究代理和企业知识助手，`cognee` 代表了“记忆层产品化”的更完整路线。
- 它把 SDK、Docker、MCP、插件和云服务同时铺开，说明记忆层正在从实验性概念往基础设施形态走。
- 如果你正在比较 `mem0`、`memsearch`、`codebase-memory-mcp` 这类路线，`cognee` 是必须放进横向对照的一项。

## 风险边界

- 记忆层一旦接入真实业务数据，数据治理、删除策略、权限继承和错误召回会比 demo 难很多。
- 图谱和向量的双重堆栈意味着部署复杂度高于纯向量库或纯缓存层。
- “记住更多”不等于“回答更准”；如果抽取质量差，错误关系也会被长期固化。

## 补充建议

1. 试用时先限定一个知识域，比如代码库、客户 FAQ 或研究文档，不要一上来灌全量公司数据。
2. 评估重点应放在：跨会话召回质量、错误记忆的清理机制、权限隔离和运维成本。
3. 如果你更关心 coding agent 记忆，建议把它与 `codebase-memory-mcp`、`memsearch` 和 `claude-mem` 一起看，判断它更偏“通用记忆平台”还是“工程记忆底层”。

## 参考资料

- https://github.com/topoteretes/cognee
- https://www.cognee.ai
- https://docs.cognee.ai/
- https://arxiv.org/abs/2505.24478
- https://github.com/trending/python?since=daily
