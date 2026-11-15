<!-- markdownlint-disable MD013 -->

# univer（dream-num/univer）

- GitHub：<https://github.com/dream-num/univer>
- 更新核查：2026-11-16（Asia/Shanghai）07 时段；25,567 stars / 2,333 forks / 175 open issues（含 PR）；同一仓库 ID `543101941`，原页刷新。
- 热度：官方综合 / TypeScript daily +1,041。
- 版本：稳定 [v1.5.0](https://github.com/dream-num/univer/releases/tag/v1.5.0)，UTC 11-14；npm `@univerjs/core` latest 1.5.0；固定 dev `0d7923dd7a26e6bea56f1bc791a03618235a4618`。替换 09-23 的 0.25.2 / 1.0 RC 观察。
- 证据：固定 README、API 稳定政策、清单、许可与发行说明相关段落静态核读；未运行编辑器、AI SDK、导出或兼容性测试。

## 定位

Univer 是把 Office 编辑、计算与文件处理嵌入产品的 SDK。产品家族包括 Web、Server 和 AI SDK；本仓库开源部分提供模型 / snapshot、插件 / 命令、公式 / 渲染引擎、Facade 和 Sheets / Docs 编辑基础。商业 Web 插件、Server SDK 及扩展 AI SDK 分开分发，不能从产品总览推出所有能力都包含在 Apache-2.0 核心中。[固定 README](https://github.com/dream-num/univer/blob/0d7923dd7a26e6bea56f1bc791a03618235a4618/README.md)

## 用法

最小表格从 `@univerjs/presets` 与 `@univerjs/preset-sheets-core` 开始，提供容器并调用 `createUniver`，以 Facade 修改单元格、计算公式和保存 JSON snapshot。应用自己负责持久化；snapshot 的保存 / 恢复与 XLSX 导入导出是不同路径。

Node.js Headless 运行要求 `>=18.17.0`，开发整个 monorepo 要求 `>=22.18`；React 18 / 19 为支持范围，旧版仅有限兼容，缺少 `Intl.Segmenter` 的环境需 polyfill。协调发布的 `@univerjs/*` 包应保持相同精确版本；Pro 选择对应发布线，icons 等独立版本包按其依赖约束处理。[稳定政策](https://github.com/dream-num/univer/blob/0d7923dd7a26e6bea56f1bc791a03618235a4618/docs/API_STABILITY.md)

从旧版升级必须逐版核迁移。1.5.0 删除部分根 Worker 导出，自定义 Worker 改从 `/worker` 子路径加载；内置 presets 已使用新入口。该迁移是发行说明的明确事实，不能只根据 minor 版本猜测无需改代码。

## 原理

核心以 plugin-first 架构把内容规则与 UI 交互分开。命令编排正向 / 逆向 mutations，配合 undo/redo；Facade 是应用接入层，扩展由对应 feature 插件和 `/facade` 入口组成。Headless 复用内容模型与计算，UI 相关功能仍需适配运行环境。

AI SDK 在此基础上提供结构化读取 / 修改、截图与布局诊断及协作 Worktree 评审；模型与工具编排、目标选择和授权归应用。JSON snapshot、协作 changeset 和 Office Exchange 是关联但不同的数据路径。[架构与产品边界](https://github.com/dream-num/univer/blob/0d7923dd7a26e6bea56f1bc791a03618235a4618/README.md)

## 价值

人和 Agent 可以围绕同一份可编辑模型处理数据，减少只生成静态图片或靠坐标操作的工作。1.5.0 的 chart sheet、误差棒、Board 布局和 Slides 保存前提交编辑草稿，有助于形成可复核的科研与商业文档流程；相关模块、原生绑定和许可仍需逐项确认。[1.5.0 说明](https://github.com/dream-num/univer/releases/tag/v1.5.0)

## 风险边界

- **API 稳定承诺与实际迁移表一起看。** 当前政策称稳定 API 在同一 major 保持兼容，但 1.5.0 发行列明 Worker 及若干导出迁移。export 或自动 API 页面本身不证明 stable，`@internal` / experimental 优先；本轮未裁定每个被删导出的稳定等级。
- **免费不等于开源或无限。** 1.5.0 原生导出说明允许每月 10 次成功无水印后继续带水印导出；需要更新 adapters，按转换开始时的已完成计数决定，并发可多出无水印文件。这是发行记录的行为边界，费用与计划仍需当前商业条款，不外推为所有功能免费。
- 新 chart sheet 等数据写入前，协调升级 SDK、协作、渲染和 native Exchange；旧 reader 可能误读。导出 / 公式 / PDF 修复也需对应原生组件，不凭 npm core 版本断言已生效。
- Slides 自定义保存前，加载对应 Pro Facade，等待 `endTextEditingAsync()` 返回 true；false 可能是草稿未提交或 IME 组合仍进行，不能忽略后保存。
- 截图、layout lint 与可撤销 Worktree 只覆盖部分质量；仍需核公式、事实、字体、导出回读及真实人审。Worktree 评审也不等于宿主进程隔离或服务端授权。
- Apache-2.0 仅覆盖本仓库开源包；商业模块及其他参考应用的许可独立。[固定许可](https://github.com/dream-num/univer/blob/0d7923dd7a26e6bea56f1bc791a03618235a4618/LICENSE)

## 补充建议

先用无敏感金标文件测试公式、合并单元格、误差棒、编辑草稿、撤销和重开；导出另测 Word / Excel / PDF 实际回读与视觉结果。保留 snapshot schema、锁文件、原生绑定和服务版本；升级旧文档时保留原件，必要时按发行指引重导入源文件。Agent 先交可编辑草稿和结构化 diff，再验最终文件。

## 参考资料

- [仓库 API](https://api.github.com/repos/dream-num/univer)、[1.5.0 发行](https://github.com/dream-num/univer/releases/tag/v1.5.0)、[npm core latest](https://registry.npmjs.org/@univerjs%2Fcore/latest)。
- [固定 README](https://github.com/dream-num/univer/blob/0d7923dd7a26e6bea56f1bc791a03618235a4618/README.md)、[API 稳定政策](https://github.com/dream-num/univer/blob/0d7923dd7a26e6bea56f1bc791a03618235a4618/docs/API_STABILITY.md)、[根清单](https://github.com/dream-num/univer/blob/0d7923dd7a26e6bea56f1bc791a03618235a4618/package.json)、[许可](https://github.com/dream-num/univer/blob/0d7923dd7a26e6bea56f1bc791a03618235a4618/LICENSE)。
- [官方文档](https://docs.univer.ai/)、[功能对照](https://univer.ai/compare/)。
