# ky-markdown-rebuilder

- GitHub：<https://github.com/KyrieCheungYep/ky-markdown-rebuilder>
- 抓取时间：2026-07-04（Asia/Shanghai）
- 今日信号：GitHub API 显示该仓库创建于 2026-07-03，抓取时约
  `31 stars / 3 forks`，README 将其定位为 Codex / Claude Code
  的复杂文档重建 skill。

## 定位

`ky-markdown-rebuilder` 是一个面向 Codex / Claude Code 的文档重建
skill，用于把视觉结构复杂的 PDF、PPT、长截图、方案报告等材料，
重建为按页对齐、结构清晰的 Markdown。

它关注的是普通文本抽取难以处理的情况：页面布局、分栏、表格、卡片、流程图、架构图、时间线和视觉阅读顺序都需要被保留下来，而不是简单把文字拼成一大段。

## 用法

安装到 Codex：

```bash
mkdir -p ~/.codex/skills
git clone https://github.com/KyrieCheungYep/ky-markdown-rebuilder.git ~/.codex/skills/ky-markdown-rebuilder
```

安装到 Claude Code：

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/KyrieCheungYep/ky-markdown-rebuilder.git ~/.claude/skills/ky-markdown-rebuilder
```

触发方式可以是显式点名：

```text
[$ky-markdown-rebuilder] 帮我把这个 PPTX 做成 Markdown
```

默认输出通常是 `source.calibrated.md`，需要大纲时可额外生成 `source.outline.md`。

## 原理

项目本质是一套文档重建流程规范：

1. 识别输入资料的页面或 slide 边界。
2. 按视觉层级提取标题、正文、表格、卡片和图示关系。
3. 每页单独成节，避免跨页内容混杂。
4. 对难以结构化的图片、截图和架构关系做必要文字说明。
5. 输出可继续被 agent、知识库或人工编辑使用的 Markdown。

## 价值

- 对知识整理：把视觉资料转成可检索、可引用、可继续加工的文本资产。
- 对 agent 工作流：让 Codex / Claude Code 在处理报告、deck、截图时有明确的重建流程。
- 对本仓库：补上“复杂文档进入 agent 上下文”的 skill 类项目，与 `MinerU`、`markitdown`、`Hyper-Extract` 形成互补。

## 风险边界

- 目前 README 更像 skill 使用说明，未展示大量真实样例和量化准确率。
- 复杂图表、数学公式、扫描件、低分辨率截图仍可能需要 OCR、视觉模型或人工复核。
- 文档重建强调可读和对齐，不等同于法律、财务或科研意义上的逐字校验。
- 未标注许可证时，团队复用前应先确认授权边界。

## 补充建议

- 可与 MinerU 这类解析工具串联：先做机器解析，再用该 skill 校准页面结构和阅读顺序。
- 对 Beamer、PPTX、长截图和产品方案类资料，建议保留原文件路径、页码和重建时间，便于后续追溯。
- 后续观察它是否补充示例集、测试样例和自动化脚本。

## 参考资料

- GitHub 仓库：<https://github.com/KyrieCheungYep/ky-markdown-rebuilder>
- MinerU：<https://github.com/opendatalab/MinerU>
- MarkItDown：<https://github.com/microsoft/markitdown>
