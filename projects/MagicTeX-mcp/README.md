# MagicTeX-mcp

## 定位

`MagicTeX-mcp` 是为 AI agent 设计的 LaTeX 编辑工作区与 MCP server：在一个类似 Overleaf 的窗口内提供源文件、可视化编辑、实时 PDF 预览、版本历史以及锚定 PDF 评论到 agent 编辑指令的闭环。截至 2026-07-26，仓库创建于 2026-07-25，约 2 stars、0 forks，采用 AGPL-3.0。

## 用法

无需本地 TeX 安装；可通过 `npx magictex-mcp` 配置 MCP，或在 Claude Code 中执行 `/plugin install magictex`。先用非机密的短文档验证 PDF 预览、评论定位、接受/拒绝改动、导出 PDF 与 ZIP，再把 agent 写作接入实际论文或 Beamer 工程。

## 原理

默认编译后端是运行在 headless browser 中的 WASM TeX Live 2026 引擎。MCP 把工作区能力暴露为工具，渲染 PDF 上的评论被转换成有位置上下文的编辑任务；视觉模式和历史记录提供人与 agent 的校对与回滚表面。

## 价值

- 将“agent 改 TeX 源码”与“人在渲染结果上批注”放进同一反馈回路。
- 避免初次试用下载完整 TeX 发行版，适合教学、原型和远程协作。
- PDF 锚点让修改请求比纯文本描述更精确。

## 风险边界

- WASM 引擎与浏览器环境不保证覆盖本地 TeX Live 的全部宏包、字体和复杂构建链。
- AGPL-3.0 对网络部署、修改分发有明确义务；敏感论文不应默认交给第三方 MCP/浏览器环境。
- PDF 评论到编辑指令仍可能被 agent 误解，数学、参考文献和图表必须人工复核。

## 补充建议

用现有 CI 的 LaTeX 构建结果做对照，测试 bib、CJK、TikZ、shell-escape 禁用和大图编译；将导出的 `.tex`、PDF 与 agent 改动 diff 一起进入 Git 审查，并明确谁有权接受最终改稿。

## 参考资料

- GitHub：<https://github.com/ZoeLinUTS/MagicTeX-mcp>
- npm：<https://www.npmjs.com/package/magictex-mcp>
- MCP Registry：<https://registry.modelcontextprotocol.io>
