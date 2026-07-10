# guizang-material-illustration

<!-- markdownlint-disable MD013 -->

## 定位

`guizang-material-illustration` 是一个面向 Claude Code、Codex 等 agent 环境的中文配图 skill，用来生成带中文标签的“歸藏材质插画”。它解决的是文章、PPT、社交卡片、教学材料和工作汇报里的中心解释图问题，而不是完整海报排版或普通装饰图。

截至 2026-07-11，GitHub API 显示该仓库约 524 stars，创建于 2026-07-07，topics 包含 `agent`、`codex`、`claude-code`、`chart-visualization`、`image-generation`、`social-media` 等。它和 `gzh-design-skill`、社交卡片类 skill 共同代表中文内容生产 agent 化的一条路线。

## 用法

推荐安装方式：

```bash
npx skills add https://github.com/op7418/guizang-material-illustration --skill guizang-material-illustration
```

典型请求包括：

- “把这段产品说明做成一张带中文标签的机制图。”
- “把这张柱状图重新画成材质风格，数据和坐标不要改。”
- “先查 PKCE 的参考信息，再做一张流程图。”
- “给小学科学课文做一张杠杆原理解释图。”

## 原理

skill 的流程是先理解材料，再判断图片类型：概念拆解、流程图、循环机制、对比图、架构图、科学机制图、人文意象图或材质化图表。对于冷门概念、品牌、科学装置和历史物件，会先做参考搜索，避免图像生成时凭空画错关键结构。

生成前会把内容压缩成一句说明和 3 到 5 个短标签，再明确比例、安全区、主题色、中文标签、数据标注和 QA 要求。生成后重点检查中文文字、数据、裁切、参考准确性和社交卡片尺寸下的可读性。

## 价值

- 对中文图文内容很实用，尤其适合公众号、小红书、PPT 和知识库配图。
- 明确要求图内有字、箭头、图例和数据标注，不把解释图降级为氛围图。
- 把图表美化定义为“语义重画”，而不是简单给截图换皮。
- 通过 references 目录把视觉风格、提示模式、图表 QA 和参考搜索规则结构化。

## 风险边界

- GitHub API 未识别到标准许可证，公开商用前需要确认授权。
- 生成式图片中的中文标签和数据仍可能出错，严肃报告和科研图不能跳过人工复核。
- 该 skill 不负责完整小红书卡片、PPT 结构或长文海报排版，需要和其他排版 skill 配合。
- 参考搜索不能复制外部图片或品牌素材，只能用于事实和视觉线索校验。

## 补充建议

- 可与 `gzh-design-skill` 分工：本项目负责中心解释图，后者负责整篇公众号 HTML 排版。
- 对团队内容生产，建议把常用主题色、禁止风格、品牌禁区和数据校验规则写入本地补充说明。
- 若用于教育或科学内容，建议把“事实参考链接”和“图像提示词”一起归档。

## 参考资料

- GitHub 仓库：<https://github.com/op7418/guizang-material-illustration>
- SKILL 文件：<https://github.com/op7418/guizang-material-illustration/blob/main/SKILL.md>
- 配套社交卡片 skill：<https://github.com/op7418/guizang-social-card-skill>
- gzh-design-skill：<https://github.com/isjiamu/gzh-design-skill>
