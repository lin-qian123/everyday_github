# IngestReasonCreate

- 仓库：[shinmingh/IngestReasonCreate](https://github.com/shinmingh/IngestReasonCreate)
- 快照：2026-08-05 抓取；GitHub API 显示其创建于 2026-08-04，约 4 stars、0 forks，Apache-2.0。数字会随时间变化。
- 分类：RAG、检索与知识处理

## 定位

本地优先的文档工作流 playbook，约束终端 agent 先本地抽取、以带页码定位的 Markdown 推理、调用真实布局引擎生成输出，再重新打开并与源文件核验。

## 用法

克隆仓库后运行 `python scripts/validate_repo.py` 和 `python scripts/smoke_test.py`；根据首次使用或后续会话提示词驱动 agent。实际 PDF、扫描件、OCR 和渲染器需要用户按文档自行安装与批准，先用非敏感样例校验页码和表格。

## 原理

流程把 PDF/DOCX/扫描件经本地 parser/OCR 转为含定位与不确定性的 Markdown；推理阶段区分事实与推断，输出由 Pandoc、Typst、Mermaid 等真实引擎构建，最终回读产物对照源文档查找矛盾。

## 价值

解决 agent 对文档“看似流畅但数值错误”、抽取顺序混乱和成品无法打开等常见问题。它特别适合保密文档，因为工作流主张不默认把源文件送往云端。

## 风险边界

这是操作规范而非解析器、OCR 或排版器；准确性取决于具体工具、语言、扫描质量与人工复核。OCR、表格和图像仍可能错位，且本地运行不自动等同于满足组织的数据保留与访问政策。

## 补充建议

为每份任务保留源文件哈希、抽取版本、页码引用和复核差异；对关键数字做独立重算。将网络下载、第三方 OCR 和导出外发设为显式审批步骤，并用代表性扫描件做回归测试。

## 参考资料

- [项目 README](https://github.com/shinmingh/IngestReasonCreate)
- [会话提示词](https://github.com/shinmingh/IngestReasonCreate/blob/main/SESSION_PROMPT.md)
- [GitHub API 元数据快照](https://api.github.com/repos/shinmingh/IngestReasonCreate)
