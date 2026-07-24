# job-search-workflow

## 定位

`job-search-workflow` 是本地优先的 AI 辅助求职框架，把职位分诊、匹配打分、申请材料、决策记录和申请追踪组织成工程化流程。截至 2026-07-25，仓库创建于 2026-07-24，约 24 stars、3 forks；README 标注为 alpha，许可证为 PolyForm Noncommercial。

## 用法

克隆后复制 `templates/user-data-skeleton/` 为被 gitignore 的个人数据目录，按项目文档准备 Python 3.10+、AI coding assistant；若需生成 PDF/DOCX，再安装 TeX 与 Pandoc。用其 modes/prompt contracts 让 Codex、Claude Code、Cursor 等协助分诊和起草，但所有提交动作应由本人执行。

## 原理

项目将职位信息、个人标准、评估结果和申请物料保存在本地文件中。它先做匹配和风险分诊，再生成针对性简历/求职信，并以 ledger 和决策记录保存过程；提示契约约束 agent 不编造履历、指标或职位信息。

## 价值

- 将零散的求职浏览变成可回顾、可比较的本地决策流程。
- “先分诊后投入”可减少把时间花在低匹配或可疑职位上的概率。
- 对个人敏感履历而言，本地数据目录和显式提交动作比黑箱 SaaS 更可控。

## 风险边界

- AI 的职位判断和文书草稿可能误读岗位、夸大经历或复制偏见，必须人工复核。
- 本地优先不等于模型调用私密；发送给模型提供商的内容仍受其数据条款约束。
- PolyForm Noncommercial 限制使其不宜直接嵌入商业招聘服务；项目尚处 alpha。

## 补充建议

将原始职位链接、抓取时间和人工判断一起记录，不要让 agent 代为投递或绕过站点限制。对简历与证件信息实施最小化上传，并定期清理本地生成的含敏感数据 PDF。

## 参考资料

- GitHub：<https://github.com/rcnsnr/job-search-workflow>
- 快速开始：<https://github.com/rcnsnr/job-search-workflow/tree/main/docs/getting-started>
