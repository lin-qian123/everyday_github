# gzh-design-skill

<!-- markdownlint-disable MD013 MD012 -->

## 定位

`gzh-design-skill` 是一个面向 Claude Code、Codex、Cursor 等 AI agent 的微信公众号排版 skill。它把已经写好的 Markdown 长文转换成可直接粘贴到微信公众号编辑器的内联 HTML，并内置主题、组件和质量校验脚本。

这个项目的重点不是“让 AI 写文章”，而是把公众号平台的样式限制、HTML 过滤规则、中文长文排版和富文本复制流程沉淀成 agent 可复用的技能包。

## 用法

推荐安装方式：

```bash
npx skills add https://github.com/isjiamu/gzh-design-skill
```

也可以让支持 skill 安装的 agent 直接安装该仓库，或手动 clone 到本地 skills 目录。使用时先准备 Markdown，再让 agent 选择主题并生成公众号 HTML，例如：

```text
用摸鱼绿把 article.md 排成公众号 HTML，并运行校验脚本。
```

项目提供 6 套精选主题，包括摸鱼绿、红白、石墨极简、留白禅意、摸鱼票据和橄榄手记，并支持通过主题生成器扩展新的组件库。

## 原理

项目把公众号排版拆成三层：

- 主题层：每套主题定义颜色、视觉层级、组件风格和适用题材。
- 转换层：由 agent 按 skill 规则把 Markdown 编排成内联 HTML，处理章节编号、关键词标记、引用卡、图片、代码块和作者签名。
- 校验层：通过 `component_lint.py` 与 `validate_gzh_html.py` 检查组件库和最终 HTML，避免 `<style>`、`class`、复杂布局等被公众号编辑器过滤后掉格式。

它的工程价值在于把“审美口径 + 平台限制 + 可验证输出”写成可复用规则，而不是每次靠提示词临场发挥。

## 价值

- 对内容团队：减少公众号排版的重复劳动，尤其适合教程、测评、产品盘点和深度长文。
- 对 agent 工作流：展示了 skill 如何把平台约束封装成稳定交付能力。
- 对设计自动化：主题生成器把“参考图/一句话风格”转成可复用组件库，是 AI-assisted design system 的轻量样本。
- 对中文内容生产：处理全角标点、关键词标记、章节结构和长文视觉层级，贴近中文公众号场景。

## 风险边界

- 项目专注排版，不应被当成自动生成事实内容或代写文章的工具。
- 公众号编辑器规则可能变化，生成结果仍需要人工在目标平台预览。
- 主题生成器输出的新组件库需要跑校验并人工看样，不能只看模型描述。
- 许可证为 AGPL-3.0，商业集成和二次分发前需要确认合规。

## 补充建议

- 与内容生产链路结合时，把“事实核查”和“排版生成”分成两个步骤。
- 对团队使用，建议固定 2-3 套主主题，并把品牌色、署名、免责声明写进团队私有主题。
- 可与 PDF/Word 转 Markdown 工具组合，但复杂表格和图片说明需要人工抽检。
- 后续重点观察它是否能支持更多中文内容平台，而不只服务微信公众号。

## 参考资料

- GitHub 仓库：<https://github.com/isjiamu/gzh-design-skill>
- 主题索引：<https://github.com/isjiamu/gzh-design-skill/blob/main/references/theme-index.md>
- 主题生成器说明：<https://github.com/isjiamu/gzh-design-skill/blob/main/references/theme-generator.md>
