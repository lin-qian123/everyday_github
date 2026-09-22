<!-- markdownlint-disable MD013 -->

# univer（dream-num/univer）

- GitHub：<https://github.com/dream-num/univer>
- 抓取快照：2026-09-23，15,346 stars、1,368 forks、138 open issues
- 热度信号：GitHub TypeScript Trending 抓取时约 +202 当日 stars
- 版本与许可：API 标示 Apache-2.0；最新稳定 GitHub Release 为 `v0.25.2`，仓库 tags 已出现 `v1.0.0-rc.0`

## 定位

Univer 是可嵌入产品的 Office SDK，覆盖表格、文档、演示文稿模型、公式、Canvas 渲染、插件系统和浏览器 / Node.js 运行时。上游把它定位为 “The Office Harness for AI Agents”，但本仓库本身首先是通用 Office SDK；Agent 侧能力通过结构化 API、Headless 处理、截图 / 布局诊断和同组织的 Workspace、CLI、MCP、skills 等项目组合起来。

## 用法

前端可按需安装 `@univerjs/*` 核心、设计、Docs、Sheets、公式和 UI 包，也可用 presets 快速组合；Node.js Headless 路径用于服务端计算和自动化。需要先按官方兼容矩阵选择浏览器 / Node 版本，并让同一协调发布线的 SDK 包保持一致。协作、导入导出、打印、图表、数据连接、服务端计算等能力部分属于 Univer Pro，不能从开源核心的安装成功推断为可用。

## 原理

核心以 plugin-first 架构组合数据模型、命令、服务、渲染、公式引擎和 Facade API。浏览器侧用 Canvas 承载大编辑面；Headless 模式在 Node.js 复用工作簿 / 文档逻辑。Agent 通过 Facade 等结构化接口读取和修改内容，再用内容检查、渲染截图和 layout diagnostics 复核；worktree / 实时协作则依赖相应产品与许可层。

## 价值

它把 Agent 写 Office 文件从坐标点击推进到可测试的数据模型和命令接口，并允许人类在交互式编辑器里审阅结果。对于 SaaS、BI、内部工具和文档自动化，复用同一模型处理前端编辑与服务端计算，可减少自建公式、渲染和多框架适配层的成本。

## 风险边界

- Headless 计算、截图和 layout diagnostics 只能覆盖部分结构 / 视觉错误，不能证明公式语义、业务事实、版式或无障碍全面正确。
- 开源核心与 Pro 的能力边界明确存在；实时协作、导入导出、图表、服务端功能和 AI 集成需要逐项核对包、版本及商业许可。
- `curl | bash`、MCP、CLI 或 skills 等配套入口不应在生产账号或敏感文档环境中直接试装；应固定版本并审阅写入范围。
- `v0.25.2` 稳定 Release 与 `v1.0.0-rc.0` tag 并存，升级前需要按稳定性政策、迁移说明和实际包版本验证。

## 补充建议

先用一套无敏感数据的公式、样式、合并单元格、批注、导入导出和多语言金标文件建立回归；分别测试浏览器显示、Headless 结果和导出文件回读。若接入 Agent，默认生成副本 / worktree，记录结构化 diff，并把事实、公式与最终视觉验收拆成独立 gate。

## 参考资料

- [GitHub 仓库](https://github.com/dream-num/univer)
- [GitHub REST API](https://api.github.com/repos/dream-num/univer)
- [官方文档](https://docs.univer.ai)
- [AI SDK 文档](https://docs.univer.ai/ai)
- [v0.25.2 Release](https://github.com/dream-num/univer/releases/tag/v0.25.2)
- [开源与 Pro 边界](https://github.com/dream-num/univer#-open-source-and-pro)
- [LICENSE](https://github.com/dream-num/univer/blob/dev/LICENSE)
