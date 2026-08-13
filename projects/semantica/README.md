<!-- markdownlint-disable MD013 -->

# Semantica

> 面向 AI 系统上下文、知识图谱与决策可追溯性的开源基础设施：将企业数据、抽取结果和 agent 决策组织为可查询、可审计的 Context Graph。

- 上游仓库：[semantica-agi/semantica](https://github.com/semantica-agi/semantica)
- 许可证：MIT
- 本轮快照：2026-08-14，GitHub REST API 约 `6.6k` stars、`693` forks；GitHub Trending 页面抓取时显示约 `727` stars/day。以上计数会随时间变化。
- 分类：RAG、检索与知识处理

## 定位

Semantica 不是只保存 embedding 的向量库。它把数据接入、解析、实体/关系抽取、冲突与重复检测、知识图谱、向量检索、决策记录和 provenance 组织成一条可自托管管线，并以 REST、CLI、MCP 等形式提供接口。项目将其重点放在“为何得出某个决策、依赖了哪些前提、后续受到什么影响”的追溯问题，适合需要把 agent 上下文与审计记录一起管理的团队。

## 用法

上游给出的 Python 最小入口如下；实际接入企业数据前应先在脱敏样本上验证 schema 和保留策略：

```bash
pip install semantica
semantica doctor
```

```python
from semantica.context import ContextGraph

graph = ContextGraph(advanced_analytics=True)
decision_id = graph.record_decision(
    category="vendor_selection",
    scenario="Choose cloud provider for HIPAA workload",
    reasoning="Documented evaluation record",
    outcome="selected_aws",
    confidence=0.93,
)
chain = graph.trace_decision_chain(decision_id)
```

先将 `record_decision` 的字段映射为团队实际的任务、来源和审批信息；再用 `trace_decision_chain`、相似决策检索及规则检查做审阅。不要把示例中的置信度值当成合规或事实正确性的证明。

## 原理

1. 从文件、网页、数据库、云盘、邮件、Git 或 MCP 等来源接入数据，解析并规范化文本与实体；
2. 将切分、实体/关系/事件抽取、冲突检测和去重结果构建为知识图谱，同时保存 provenance；
3. 将向量存储与 RDF/LPG 图存储并置，支持语义检索、图查询与分析；
4. 把 agent 的决策、理由、结果及其因果关联记入 Context Graph，供规则检查、影响分析和回溯使用。

图谱和向量检索能改善“找到相关证据”的能力，但不能自动保证抽取正确、因果成立或来源具备授权。

## 价值

- 将 RAG 上下文、知识模型和 agent 决策轨迹放进同一个可查询对象，便于复盘而不只生成答案。
- 面对冲突事实、版本变化和跨系统数据时，能把来源与处理过程显式保留，降低不可解释的上下文拼接。
- 提供可自托管、MIT 许可的工程起点，适合从小范围、可审阅的知识域逐步验证。

## 风险边界

- 接入邮件、云盘、数据库和 MCP 会扩大敏感数据与凭据的流动面；应按源系统最小权限、数据分级、脱敏、访问日志和撤销路径逐项配置。
- 自动实体抽取、冲突消解和关系推理会产生误连、漏连或过期结论；关键决策必须回到原始证据和人工审批，不能由图查询结果自动执行。
- 图谱中的历史决策、人员关系或业务元数据本身可能敏感；删除、保留期限、跨境传输和导出权限需在部署前定义。
- “可审计”取决于输入与日志是否完整、是否可篡改和审阅流程是否真实运行；项目功能不能替代组织的合规控制。

## 补充建议

- 先选一个边界清晰、低风险的 corpus，建立来源 ID、时间、许可证/访问级别和人工纠错回写的最小 schema。
- 为每条 agent 决策记录原始证据 URI、模型/提示词版本、工具调用摘要和审批人；将这些字段与业务写操作分离。
- 以人工标注的关系与问答集合测试抽取准确度、检索召回和冲突处理，再评估成本与是否扩展到生产数据。

## 参考资料

- [项目 README：安装、架构与 Context Graph 示例](https://github.com/semantica-agi/semantica#readme)
- [Semantica 文档](https://docs.getsemantica.ai/)
- [GitHub 仓库元数据](https://api.github.com/repos/semantica-agi/semantica)
- [GitHub Trending 观察入口](https://github.com/trending)
