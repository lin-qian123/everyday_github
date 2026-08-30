<!-- markdownlint-disable MD013 -->

# 中国专利.skill

> 上游仓库：[handsomestWei/patent-disclosure-skill](https://github.com/handsomestWei/patent-disclosure-skill) · 归类：办公、商业与行业应用 · 本页基于 2026-08-31 的 GitHub Trending、REST API 与上游 README 快照整理。

## 定位

这是一个面向中文专利工作的 Agent Skill，覆盖专利点挖掘、发明/实用新型/外观设计交底书、公开专利通俗解读、政策动向观察和审查答复草稿。官方 Trending 抓取时显示约 +38 当日 stars；REST API 快照为 5,628 stars、696 forks、8 个开放 issue，最近推送于 2026-08-30，API 许可证为 MIT。它更像一套带模板、提示词、工具和 Obsidian 入口的工作流，而不是专利法律意见系统。

## 用法

先阅读上游 [INSTALL.md](https://github.com/handsomestWei/patent-disclosure-skill/blob/main/INSTALL.md) 与 [SKILL.md](https://github.com/handsomestWei/patent-disclosure-skill/blob/main/SKILL.md)，再在副本目录中提供已授权的项目材料或公开专利 PDF。自然语言入口包括“按发明写交底”“读专利”“政策雷达”和“审查答复”；可选配置 `PATENT_READER_OBSIDIAN_VAULT` 将笔记、Canvas、术语和双链写入指定 vault。没有 Obsidian 时，流程可降级到 `outputs/`。

典型输入应明确专利类型、项目路径/公开号、允许的材料范围和交付格式。生成的 Markdown、Mermaid/SVG 图、Word 文档、检索清单或审查答复都应先作为草稿审阅，不直接递交或公开。

## 原理

- 项目扫描按优先级读取文档和代码，`.docx`/`.pptx` 可先转 Markdown；STEP/CAD 默认不解析，避免材料不足时假装理解工程结构。
- 交底流程把类型判断、专利点讨论、查新、脱敏、图示计划和成文分开；发明使用 Mermaid 框图，实用新型/外观设计按 `figure_plan.yaml` 组织视图和部件序号。
- 专利解读流程抽取全文/PDF，形成权要树、术语表、特征—说明书—附图对照和 Canvas 图谱；公开线索只作为行业语境，不替代权要和说明书证据。
- 审查答复模块可把历史案件脱敏入库，以标签或可选本地轻量向量检索召回相似案例，再输出待人工修改的意见陈述草稿。

## 价值

- 将研发材料、专利点、图示和可编辑交底书连接起来，降低从技术贡献到初稿的整理成本。
- 把单篇专利阅读沉淀为 Obsidian 中可检索、可关联的私有知识库，便于同族、术语和技术路线比较。
- 明确区分类型模板、材料扫描、检索、成文和迭代另存，有利于保留版本和修改追踪。
- 对科研或工程团队而言，`project_scan.md`、`prior_art_search.md`、图示 schema 与对话记录可作为内部复盘凭据，而不是只保留一份不可追踪的成稿。

## 风险边界

- 生成的专利点、查新判断、权利要求解释和审查答复均不是法律意见；新颖性、创造性、权利要求范围和授权前景必须由合格专利代理师/律师与发明人核验。
- LLM 可能漏读附图、误解结构关系、混淆同族专利或把公开线索写成权要证据；检索结果必须回到原始公报、说明书和附图。
- 项目扫描与 Obsidian 入库可能暴露源代码、商业秘密、未公开发明、客户材料和历史案件；应使用脱敏副本、最小权限 vault、固定网络出口和可删除留痕。
- 图生图、文生图和自动生成线稿只能辅助表达，不能证明外观视图、结构尺寸或法律上的必要特征正确。
- 上游 README 与 API 为 MIT，但第三方工具、国知局服务、Obsidian 插件和模型/provider 可能有额外许可、访问限制与数据条款。

## 补充建议

1. 先用虚构或已公开案件验证扫描范围、输出命名、版本另存、图示编号、Obsidian 写入和清理路径。
2. 为每条关键结论保留“原始证据位置—模型摘要—人工判断”三列；查新报告单独记录检索式、日期、数据库和失败情况。
3. 将最终交底书锁定在人工签发流程中，禁止 agent 直接向国知局、客户或外部协作者提交文件。
4. 审查答复只把案例 RAG 当作候选参考；法律条文、期限、审查意见原文和答复策略须由专业人员重新确认。

## 参考资料

- [上游 README、功能与示例](https://github.com/handsomestWei/patent-disclosure-skill)
- [技能入口与 Agent 流程](https://github.com/handsomestWei/patent-disclosure-skill/blob/main/SKILL.md)
- [安装说明](https://github.com/handsomestWei/patent-disclosure-skill/blob/main/INSTALL.md)
- [国知局中国专利公布公告](http://epub.cnipa.gov.cn/)
- [REST API 元数据](https://api.github.com/repos/handsomestWei/patent-disclosure-skill)
- [GitHub Trending](https://github.com/trending)
