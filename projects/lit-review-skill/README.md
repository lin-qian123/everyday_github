# lit-review-skill

## 定位

`lit-review-skill` 是给 Claude、Codex 等 agent 使用的文献检索与引文审计技能。它把工作分为找文献、核验引文和基于检索结果写作三条路径，并声明从 Semantic Scholar、OpenAlex、arXiv、Crossref 获取书目信息，而非由模型记忆补全。

截至 2026-07-30，GitHub API 显示仓库创建于 2026-07-29，约 15 stars、MIT 许可证；这是早期开发者信号，作者的“实战验证”不构成独立准确率评测。

## 用法

按宿主安装为 skill；也可在 Codex 等工具的项目指令中要求 agent 先读其 `SKILL.md`。典型请求包括 `check` 审计章节引文、`find` 为段落找文献、`write` 做检索后写作；可选 `.env` 支持 API 额度与礼貌池配置，绝不能提交密钥。

```bash
git clone https://github.com/Zachariah9420/lit-review-skill.git ~/.claude/skills/lit-review
# 例如：check chapter2.docx
```

## 原理

技能将引用存在性、书目字段、撤稿、主张支持度和证据等级拆开检查，并用新上下文审计者复核生成结果。它还在上游 API 限流时切换数据源，避免把“未找到”直接说成“伪造”。

## 价值

- 为 agent 文献工作流提供可追溯的 API 来源、审计报告和 RIS/BibTeX 输出。
- 明确区分摘要级、全文页码级与无法判断的证据，降低“有引用但不支持主张”的风险。

## 风险边界

- 摘要不足以裁决复杂主张；付费墙、中文文献、图书和行业会议仍可能只能标为待人工核验。
- 数据库覆盖、API 时效与撤稿记录均非完备；自动结论不能替代作者逐篇阅读与原文核对。
- 外部检索内容是不可信输入，应隔离提示注入与恶意 PDF/网页内容。

## 补充建议

在论文提交或重要决策前，对关键引用复查 DOI、出版社页面和全文具体页码。把自动审计报告存进项目证据链，但保留人工对研究问题、纳入标准和解释边界的决定权。

## 参考资料

- GitHub：<https://github.com/Zachariah9420/lit-review-skill>
- GitHub API 快照：<https://api.github.com/repos/Zachariah9420/lit-review-skill>
- Crossref：<https://www.crossref.org/>
