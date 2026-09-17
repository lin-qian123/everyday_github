<!-- markdownlint-disable MD013 MD034 -->

# QuantMind：面向量化金融的可追溯知识加工与检索框架

> 上游仓库：https://github.com/LLMQuant/quant-mind · 归类：RAG、检索与知识处理 · 本页基于 2026-09-18 的 README、contexts、`pyproject.toml`、测试与 LICENSE 静态整理；未运行论文 / 新闻 pipeline，也不构成投资建议。

## 定位

QuantMind 把论文、新闻和未来的 filings 等原始金融信息转换为带类型、时间戳和来源引用的知识对象，并提供 BM25 / similarity、library 与 agentic retrieval。仓库还把 AGENTS、contexts、skills、hooks 和确定性 verify 当成“harness engineering”产品面。

2026-09-18 的 GitHub 官方 Python Trending 抓取显示约 `+94 stars today`；REST API 快照为 `2,978 stars / 481 forks / 32 open issues`，MIT，主包版本 `0.2.0`，无 GitHub Release，main 最近 push 为 2026-08-15。

## 用法

上游推荐让 coding agent 在 checkout 内按项目 contract 构建 pipeline，也可作为普通 Python `>=3.10` library 使用：

```sh
git clone https://github.com/LLMQuant/quant-mind.git
cd quant-mind
uv venv && source .venv/bin/activate
uv pip install -e .
```

`PaperFlow` 可把 arXiv 输入变成 page-cited structure tree 或 semantic chunks + cited summary；`collect_news` 和 `batch_run` 处理可重放时间窗与批量任务。

## 原理

- `fetch / parse / format / clean` 的确定性预处理保留 source-faithful 内容与 provenance，再由模型执行需要语义判断的步骤。
- `Paper`、`News`、`Earnings`、`Factor`、`Thesis` 等对象自带 `as_of` 与轻量来源引用，支持 point-in-time 查询。
- `rag/`、`library/` 与 `mind/` 分别承担 chunk / BM25 / similarity、本地持久化与 agentic reasoning retrieval。
- 仓库级 AGENTS / CLAUDE contracts、progressive contexts、portable skills 与 shared hooks 约束 coding agent；`scripts/verify.sh` 统一 lint、types、边界与 tests。
- README 明确 `quantmind-bench` 和知识质量 benchmark 尚在设计，当前没有发布 A/B 数字。

## 价值

- 把“来源、时间和类型”设为知识对象的一部分，比只存 embedding 更适合金融历史状态和可审计研究。
- 确定性预处理与模型步骤分开，有利于复现抓取、定位幻觉发生在哪一层。
- repo-as-harness 让开发规则、上下文与验证和代码同版本，适合团队积累领域工作流。
- 同时提供 library 与 agent-driven contributor 路径，既可嵌入应用，也可作为可编辑 pipeline 基础。

## 风险边界

- 金融新闻、论文、公司材料与模型摘要都可能错误、过时或受版权 / 数据供应条款限制；citation 存在不等于 claim 被来源支持。
- `as_of` 只有在抓取时间、来源修订、时区、去重和回填都正确时才支持 point-in-time 结论；幸存者偏差和未来信息泄漏需单测。
- README 明确 eval 仍在设计，不能把“agent-native”或 verify 通过写成知识准确率、投资收益或生产成熟度证明。
- 代码示例会调用外部模型和 arXiv / 新闻源，需治理 API key、成本、网络、数据留存与不可用重试。
- 量化金融知识框架不是交易系统；任何因子、thesis 或检索答案都需独立数据、统计和风险验证。
- 本页未运行 `0.2.0`，没有验证 PDF 解析、citation precision、time query、provider drift 或 batch recovery。

## 补充建议

1. 用固定文档、固定模型与冻结时间窗建立 citation precision / recall、日期正确性和 source revision 金标。
2. 把原文、解析、模型输出、知识对象和检索结果分别保存 hash 与版本，避免只保留最终卡片。
3. 对新闻回填、重复稿、时区边界、修订公告与 delisted entity 做 point-in-time 防泄漏测试。
4. 在把任何输出用于研究或交易前，加入独立行情 / 公告源、统计显著性、费用、滑点和人工复核。

## 参考资料

- 上游 README：https://github.com/LLMQuant/quant-mind
- 设计 contexts：https://github.com/LLMQuant/quant-mind/tree/master/contexts/design
- `pyproject.toml`：https://github.com/LLMQuant/quant-mind/blob/master/pyproject.toml
- NeurIPS workshop paper：https://arxiv.org/abs/2509.21507
- GitHub REST API：https://api.github.com/repos/LLMQuant/quant-mind
- LICENSE：https://github.com/LLMQuant/quant-mind/blob/master/LICENSE
