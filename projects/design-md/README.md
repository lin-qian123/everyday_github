# DESIGN.md（google-labs-code/design.md）

- GitHub: https://github.com/google-labs-code/design.md
- 规范页: https://stitch.withgoogle.com/docs/design-md/specification
- 记录日期: 2026-06-26 (Asia/Shanghai)

## 定位

`design.md` 是一个给 coding agent 使用的界面设计规范格式。它试图把设计系统从“截图、口头描述、Figma 链接”变成一份 agent 可长期理解的文本契约，让模型既看到设计 token，也看到背后的风格说明。

## 热度信号

1. GitHub API 在 2026-06-26 抓取时显示约 `19,077 stars`、`1,641 forks`，仓库在 `2026-06-15T22:22:46Z` 仍有近期推送记录。
2. GitHub Trending 全站与 TypeScript 日榜在 2026-06-26 抓取时都出现该项目，Trending 页面显示约 `1,407 stars today`。
3. 官方 README 把定位写得很直接：`A format specification for describing a visual identity to coding agents`。

## 用法

### 1) 在项目里写一个 `DESIGN.md`

README 的基本格式是：YAML front matter 写 token，Markdown 正文写设计原则，例如颜色、字体、间距、组件风格与 Do's / Don'ts。

### 2) 用官方 CLI 校验规范

```bash
npx @google/design.md lint DESIGN.md
```

它会检查结构问题、token 引用、对比度和其他规范性错误，并输出 JSON。

### 3) 比较两个设计版本的差异

```bash
npx @google/design.md diff DESIGN.md DESIGN-v2.md
```

这对 agent 工作流很关键，因为它把“设计变更”也做成了可比较、可审查的文本差异。

## 原理

1. 文件分成两层：上面的 YAML token 提供机器可读的精确值，下面的 Markdown 解释这些值为何存在、应该怎么用。
2. agent 在生成界面时，不再只靠提示词临时猜风格，而是读取一份持久化设计契约。
3. CLI 既能 lint，也能 diff，说明它不是单纯提格式，而是在把设计系统纳入工程工作流。
4. 这条路线和 `stitch-mcp`、`openui` 一样，核心都是把设计上下文转成模型可消费的结构化输入。

## 价值

- 对 AI 驱动前端开发，这是很强的基础设施信号，因为它把“设计语言”从抽象偏好变成了仓库里的可执行上下文。
- 它特别适合多人协作或多 agent 场景，减少“同一品牌风格在不同页面被模型生成得越来越飘”的问题。
- 如果后续更多前端项目把 `DESIGN.md` 当成标准入口，设计系统和代码仓库之间的边界会进一步收敛。

## 风险边界

- 有了 `DESIGN.md` 不代表页面一定好看；它解决的是约束一致性，不是自动提供高质量审美判断。
- 规范能约束 token 和结构，但不能替代真实产品需求、交互逻辑和可访问性审查。
- 若团队没有维护设计 token 的习惯，文件很容易过时，最终变成“看起来规范、实际上失效”的陈旧上下文。

## 补充建议

1. 先在营销页、组件库或内部工具里试点，用它约束颜色、字体、圆角、间距和按钮语义，最容易看出收益。
2. 如果仓库已经在用 `DESIGN.md`、`SPEC.md`、`PRD` 这类文本契约，可以把它放进同一套 agent 上下文管理链里。
3. 建议与 `stitch-mcp`、`openui`、`agent-native` 一起理解：前者偏把设计产物接入开发，`design.md` 偏把设计原则本身结构化。

## 参考资料

- https://github.com/google-labs-code/design.md
- https://stitch.withgoogle.com/docs/design-md/specification
- https://github.com/trending
- https://github.com/trending/typescript
