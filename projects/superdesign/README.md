<!-- markdownlint-disable MD013 -->

# Superdesign 原 IDE 扩展（superdesigndev/superdesign）中文解读

> 上游仓库：<https://github.com/superdesigndev/superdesign> · 归类：前端、UI 与 Agent 交互层 · 证据快照：2026-10-17（Asia/Shanghai）。API：7,428 stars / 767 forks / 75 open issues；无 GitHub Release；最新返回 tag `v0.0.13`，package.json `0.0.14`；API NOASSERTION；根 LICENSE 为主体 AGPLv3 + Enterprise 标记文件商业条款。本页为上游资料与相关代码的静态整理，未安装运行、复测性能或完成全面安全审计。

## 定位

这是 2025 年的 Superdesign IDE 扩展开源仓库。当前 README 顶部明确说明仅保留历史、已不再积极维护，现产品转向 Web app 与单独的 superdesign-skill。虽然本次 TypeScript Trending 仍有增星，也不能把这个旧扩展当作当前托管产品的完整开源实现。

## 用法

若研究历史实现，先固定 tag / commit，在一次性 VS Code / Cursor 配置中审阅扩展与 provider 设置，按 README 打开 sidebar / canvas 并用非敏感提示生成简单组件。README 支持自定义 OpenAI-compatible 服务；是否真正本地推理取决于配置的 endpoint。当前 Web app、Chrome 扩展和独立 skill 应分别阅读各自的安装、数据和许可说明，本页不保证旧安装入口仍提供同版制品。

## 原理

- IDE extension 提供 chat sidebar、canvas 和多种 LLM provider adapter，生成 mockup、wireframe 和组件。
- 初始化可写入 Cursor / Claude Code 设计规则；设计产物按 README 保存于 `.superdesign/`，便于 fork / iterate。
- package.json 暴露 API、Claude CLI 与自定义 URL 等选项；托管 Web app 的当前服务架构不在本仓库证据范围内。

## 价值

它适合研究“IDE 内生成 → 画布预览 → 迭代 → 回填代码”的早期交互设计，也能帮助判断设计技能与扩展 UI 的职责。新项目选型应首先评估维护状态，而不是把历史演示和今日 stars 合成当前能力证明。

## 风险边界

- **维护状态**：README 已明确停止积极维护；旧依赖、provider 名称、API 与商店制品可能漂移，manifest 版本与 tag 也不一致。
- **许可不是单一 AGPL**：根 LICENSE 说明带 `/* @license Enterprise */` 的文件适用商业条款，生产使用需相应有效协议；不能因 README 泛称 open source 就默认全部可自由复用。本次未逐文件清点 Enterprise 标记。
- “设计文件本地保存”不意味着提示、代码与截图不发往 provider；初始化规则、CLI 与 IDE workspace 权限需分别审阅。
- 生成 UI 的视觉相似或单次预览不能证明 accessibility、响应式、授权素材和业务交互达标。

## 补充建议

把历史扩展、当前 Web app 和独立 skill 分别建版本 / 权限清单。用无凭据的小组件验证产物路径和真实 endpoint；采用前先核对依赖维护与文件级许可，再做键盘操作、移动视口及交互验收。

## 参考资料

- 上游仓库：<https://github.com/superdesigndev/superdesign>
- GitHub REST API：<https://api.github.com/repos/superdesigndev/superdesign>
- 停止维护声明与迁移入口：<https://github.com/superdesigndev/superdesign/blob/main/README.md>
- 扩展 manifest：<https://github.com/superdesigndev/superdesign/blob/main/package.json>
- 扩展入口：<https://github.com/superdesigndev/superdesign/blob/main/src/extension.ts>
- 混合许可正文：<https://github.com/superdesigndev/superdesign/blob/main/LICENSE>
- Releases：<https://github.com/superdesigndev/superdesign/releases>
