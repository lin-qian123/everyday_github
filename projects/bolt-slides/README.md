# bolt-slides

## 定位

`bolt-slides` 是 StackBlitz 发布的 agent 友好型演示文稿框架：每一页 slide 都是可运行的 React/Web 页面，支持 3D、实时数据、产品原型、响应式布局和可分享链接。它把“AI 做 PPT”从静态模板推进到交互式 Web deck。

截至 2026-07-18 抓取时，仓库约 `299` stars、`45` forks，主要语言为 TypeScript，许可证为 `MIT`。

## 用法

最直接的方式是在 Bolt 中打开仓库，然后提示 agent 生成面向特定受众的 deck。手动运行：

```bash
git clone https://github.com/stackblitz/bolt-slides
cd bolt-slides
npm install
npm run dev
```

项目自带 26 页 demo。删除或改写 `src/App.tsx` 中的 demo slides 即可创作自己的 deck。

## 原理

Deck 由 React 组件组成：`<Deck>` 下每个顶层子元素是一页 slide。项目提供 Cover、Agenda、Section、Bento、Charts、Table、Timeline、CodeWindow、BrowserFrame、Pricing、Globe 等组件，并包含 `.bolt/skills/slides/SKILL.md`，指导 agent 进行主题、排版和内容组织。

演示层支持缩略图侧栏、grid overview、click builds、annotation、presenter mode、URL hash deep link 和响应式布局。

## 价值

- 将 presentation 变成真实 Web app，适合产品演示、数据报告和交互原型。
- 给 coding agent 明确的 slide authoring skill，降低生成低质幻灯片的概率。
- 与 `presenton`、`ppt-master`、`dashiAI-ppt-skill` 形成互补：一个偏 Web deck，一个偏原生 PPTX/办公格式。

## 风险边界

- Web deck 不等于企业常用 PPTX 格式，交付给传统办公流程时可能需要另行导出或改造。
- 高自由度会让 agent 过度设计，仍需要主题约束和视觉验收。
- 交互式 deck 的可访问性、打印和离线兼容需要具体测试。

## 补充建议

- 后续观察 StackBlitz / Bolt 是否把该项目进一步产品化为 agent slide 工作流。
- 可作为本仓库“前端、UI 与 Agent 交互层”与“办公应用”之间的桥接样本。

## 参考资料

- GitHub: <https://github.com/stackblitz/bolt-slides>
- StackBlitz: <https://stackblitz.com/github/stackblitz/bolt-slides>
- Bolt: <https://bolt.new/github.com/stackblitz/bolt-slides>
