<!-- markdownlint-disable MD013 -->

# rag-ci

- 仓库：[Nokimalos/rag-ci](https://github.com/Nokimalos/rag-ci)
- 快照：2026-08-10 抓取；GitHub API 显示其创建于 2026-08-09，约 9 stars、0 forks，MIT。数字会随时间变化。
- 分类：RAG、检索与知识处理

## 定位

面向 RAG 检索回归的 CLI 与 CI action。它将当前管线结果与基线做配对统计比较，在变化既达到最小效应又具统计显著性时才使 PR 失败，避免把小 golden set 的随机波动当回归。

## 用法

项目要求 Python 3.12+，可用 `uvx rag-ci init` 生成 adapter，再以 `golden gen`、`golden review` 建立并人工确认问题集；`rag-ci run` 运行评估，`rag-ci gate --baseline baseline.json` 作为门禁，`sweep` 做配置搜索。生成候选问题是可选能力，README 指定需 `ANTHROPIC_API_KEY`；基础评估不依赖模型。

## 原理

adapter 将任意 RAG 栈接到统一契约，golden ground truth 锚定在文档段落而非具体 chunk。工具对配对结果进行 10,000 次 bootstrap，报告 95% 置信区间；门禁要求统计证据和效应量同时满足，并将不同 golden set、无效运行等“不可信比较”用独立退出码区分。

## 价值

它把 RAG 的评估从单个均值转为带不确定性的 CI 信号，适合在 chunk、reranker、索引和参数频繁调整时降低误报警。框架无关的 adapter 与参数 sweep 也利于将检索质量、延迟和成本放到同一可复核的工程循环中。

## 风险边界

统计显著不等于产品正确、安全、公平或回答真实；golden set 的覆盖、标注质量和数据漂移仍决定结论。启用问题生成会把输入送往所选模型 provider；CI 里的样本、passage、日志和 PR 评论也可能暴露内部知识库内容。9 stars 只是早期观察，尚不能证明其门禁策略适合所有 RAG 业务。

## 补充建议

先用去敏公开数据和固定 adapter 复跑参考示例，再为真实场景建立分层、人工审过的 golden set。将显著性阈值、最小效应和样本规模作为版本化配置，并额外评估答案事实性、拒答、权限与隐私，而不只跟踪 recall。

## 参考资料

- [项目 README](https://github.com/Nokimalos/rag-ci)
- [设计文档](https://github.com/Nokimalos/rag-ci/blob/main/docs/design.md)
- [GitHub API 元数据快照](https://api.github.com/repos/Nokimalos/rag-ci)
