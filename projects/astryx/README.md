<!-- markdownlint-disable MD013 -->

# Astryx：让人和 Agent 共用组件文档的 React 设计系统

- 上游：[meta/astryx](https://github.com/meta/astryx)；仓库 ID：`1131202426`。
- 快照：2026-11-08（Asia/Shanghai）；stars / forks / open issues（含 PR）：14,449 / 1,181 / 732；官方 daily 榜 综合 / TypeScript +185，不是自然日结算。
- 分类：前端、UI 与 Agent 交互层；最新发行：[v0.7.11](https://github.com/meta/astryx/releases/tag/v0.7.11)（UTC 2026-11-07 15:00:47，非预发行标记）。
- 核读基线：`main@96df1b8eb80a5bda8bd886f49d9ca1077f14429d`。以下为文档与抽样源码核读，作者声明与本轮运行验证分开。

## 定位

Astryx 是 Meta 公开的 React 设计系统，提供组件、主题、模板与 CLI。Agent 通过同一套类型和文档发现组件、生成页面、查询 token；它提供 UI 构建材料，不负责业务权限、后端数据或自动证明页面正确。当前仍为 Beta，要求 React / React DOM 19+。

## 用法

先在已有 React 19 测试项目中安装；示例按本轮稳定发行固定版本，所有使用的 `@astryxdesign/*` 包保持一致：

```bash
npm install @astryxdesign/core@0.7.11 @astryxdesign/theme-neutral@0.7.11 @stylexjs/stylex
npm install -D @astryxdesign/cli@0.7.11
npx @astryxdesign/cli component Button
npx @astryxdesign/cli template --list
```

按 core 快速入门导入预编译 CSS 并配置主题 provider。需要接入 Agent 时才运行 `init`：它会写入项目的 AGENTS.md / CLAUDE.md。不要在未安装时执行裸 `npx astryx`，上游明确该名字属于另一个 npm 包。本轮没有执行这些命令。

## 原理

组件内部用 StyleX 编写样式，消费者可直接使用预编译 CSS、类型化 React 组件与 CSS 自定义属性主题；自有 className 可与 Tailwind、CSS Modules 等组合。CLI 把组件 API、模板、主题、迁移 codemod 组织为可发现接口；`swizzle` 将组件源码导出到项目，由项目承担后续维护。

## 价值

同一套 API / 文档可减少人工和模型猜测组件属性，主题与模板也便于复用。README 自报 150+ 组件，当前官网写 180+，两者统计口径 / 更新时点不同；“内部 13,000+ 应用”是上游背景声明，不是本轮独立统计或外部项目兼容性证明。

## 风险边界

- Beta 和快速发行可能改变 API；本轮主线 SHA 与 v0.7.11 发行分别记录，主线文档不保证每项都在稳定包中。
- `init`、`swizzle` 和 `upgrade --apply` 会写项目；升级前检查 diff、保留回滚，并核对所有包版本。组件导出后不再自动随上游修复。
- README 说明 lab 未发布到 npm，vega / charts 仅有 canary；不能把目录存在当稳定可安装承诺。
- “accessible”与“agent ready”是设计目标；键盘、读屏、触摸、缩放、中文长文本和生成页面的视觉质量仍需实际验收。
- 根许可为 MIT；第三方依赖、字体和所用素材另核。未安装、构建或运行 UI / 无障碍测试。

## 补充建议

用真实业务中最小的表单和数据表做试点：检查组件 API、暗色主题、焦点恢复、移动端与失败状态。让 Agent 先查组件文档再写代码；迁移先生成可审阅差异，再运行构建和交互检查。对于不稳定图表 / lab 组件，记录使用版本和替代路径。

## 参考资料

- [README.md](https://github.com/meta/astryx/blob/96df1b8eb80a5bda8bd886f49d9ca1077f14429d/README.md)
- [packages/core/README.md](https://github.com/meta/astryx/blob/96df1b8eb80a5bda8bd886f49d9ca1077f14429d/packages/core/README.md)
- [packages/cli/README.md](https://github.com/meta/astryx/blob/96df1b8eb80a5bda8bd886f49d9ca1077f14429d/packages/cli/README.md)
- [LICENSE](https://github.com/meta/astryx/blob/96df1b8eb80a5bda8bd886f49d9ca1077f14429d/LICENSE)
- [GitHub API 快照](https://api.github.com/repos/meta/astryx)；[发行列表](https://github.com/meta/astryx/releases)。
- [官网与组件 / 模板入口](https://astryx.atmeta.com/)。
