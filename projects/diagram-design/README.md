<!-- markdownlint-disable MD013 -->

# diagram-design

## 定位

[`cathrynlavery/diagram-design`](https://github.com/cathrynlavery/diagram-design) 是一个可安装给 Claude Code、Codex、Pi 等 coding agent 的图表设计 skill/插件。上游提供 27 种静态 HTML/SVG 图表类型、可选动效、品牌 token 提取和 Mermaid/draw.io 重绘。它的核心是将“图表类型、信息密度、色彩与排版”显式写成 agent 可读规则，而不是把任何文本直接交给通用图片生成模型。

## 用法

上游给出的 Codex marketplace 安装方式为：

```bash
codex plugin marketplace add cathrynlavery/diagram-design
codex plugin add diagram-design@diagram-design
```

随后用自然语言说明图表目的、读者、事实来源、尺寸和可访问性要求。对于已有 Mermaid 或 draw.io 文件，先在副本上导入/重绘，并把生成的 HTML/SVG 纳入代码审查；不要让 skill 直接覆盖正式设计源文件。

## 原理

- 仓库将架构、流程、序列、状态机、数据模型、时间线、数据流等固定为若干视觉类型，并提供浅色、深色和 editorial 静态变体。
- 其“semantic patterns”将信任边界、策略轨迹、队列等行为语义与具体版式分开，使 agent 优先复用既有图形而非无限增加新模板。
- 品牌 onboarding 会读取用户指定网站的颜色、字体和布局 token，映射为纸张、正文、弱化色、强调色等角色；之后生成前检查对比度。该流程会访问外部 URL，样本范围及输出变更应由用户确认。

## 价值

- 适合把可读性、密度、层级和静态交付约束前置到 agent 工作流，降低“生成一个看似完整但无法编辑的图”风险。
- HTML/SVG 优先，利于版本控制、代码审查和在文档站/报告中复用；图库可在本地打开。
- GitHub API 于 2026-08-16 的快照为约 18.6k stars、1.1k forks、MIT；GitHub Trending 当时显示约 +1.6k stars/day。其反映短期可见度，不代表对每个品牌、语言或无障碍需求都适配。

## 风险边界

- 图表可视化不会核验内容事实、数字口径、架构安全性或流程合规性；这些仍须由领域负责人审阅。
- 外部网站品牌抽取可能收集 URL 内容、字体或样式信息；对内网、客户站、未授权站点及含敏感标识的页面应禁用，或改用手工提供的 token。
- 第三方 marketplace 自动更新可能改变 skill 行为或覆盖本地修改。上游也提示 editable install 的直接改动可能被更新替换。
- Mermaid/draw.io 重绘可能遗漏注释、交互、语义或版权标记；应保留原文件并做视觉与内容 diff。

## 补充建议

1. 在仓库内固定插件版本或提交使用的 skill revision，并在 CI 中对关键图导出的 SVG/HTML 进行快照检查。
2. 每张图先建立“事实表—读者—主结论—允许的视觉类型”简报；将文本、数字和引用的核验与绘图分离。
3. 若需品牌化，优先显式提供色彩/字体 token，并先审阅拟议 diff；不要把私有站点 URL 交给自动提取流程。
4. 对图中的色彩、文字大小、阅读顺序和动效偏好做独立无障碍测试；静态 fallback 应始终可用。

## 参考资料

- [GitHub 仓库](https://github.com/cathrynlavery/diagram-design)
- [上游安装说明](https://github.com/cathrynlavery/diagram-design#install)
- [在线图库](https://cathrynlavery.github.io/diagram-design/)
- [图表 style guide](https://github.com/cathrynlavery/diagram-design/blob/main/skills/diagram-design/references/style-guide.md)
- [GitHub REST API 元数据快照](https://api.github.com/repos/cathrynlavery/diagram-design)
