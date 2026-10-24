<!-- markdownlint-disable MD013 -->

# hallmark：面向 Coding Agent 的网页设计技能

- 主上游：[Nutlope/hallmark](https://github.com/Nutlope/hallmark)；repository ID `1222917575`。
- 采样日期：2026-10-25（Asia/Shanghai）；分类：前端、UI 与 Agent 交互层。
- API 累计快照：32,081 stars / 1,647 forks / 49 open issues（含 PR 口径）；与榜单日增分开。
- 默认分支 `main`，本页静态依据固定在 `7ec868225c6caa040558c321ee0fefa0e73f83a8`。公开 Release 列表为空，不据此推断没有 tag 或包发行。
- 核验层级：直接读取上游文档、许可、元数据和下列部分实现；未安装运行、调用模型或复现性能。

## 定位

Hallmark 是供 Claude Code、Codex、Cursor、OpenCode 等宿主读取的设计技能，不是独立生成模型。当前 README 宣称提供 48 种主题、重新设计与审计入口；主题数量与视觉质量属于上游描述，本轮没有逐主题渲染或做用户测试。

## 用法

先审阅技能及脚本，优先在测试项目局部安装；上游安装入口如下，本轮未执行：

```bash
npx skills add nutlope/hallmark
```

README 中的 `-g` 会安装到用户级目录，省略则面向当前项目。Claude Code 可用 `/hallmark audit ./index.html`，Codex 可显式点名 `$hallmark`。上游要求 Node 18+；浏览器检查另需 puppeteer-core 和 Chrome，缺失时只能做静态检查。应先固定 commit，避免将滚动安装内容与本页快照混用。

## 原理

技能先读取项目设计约束，按任务选择主题或自定义方向，再先做首屏、后做整页。Floor 约束对比度、焦点、移动布局和事实真实性，Reflex 规则允许记载理由后豁免，Finish 是细节复核。sloplint 脚本配合真实浏览器检查；README 还要求独立上下文审阅。这是提示、脚本与宿主工具的组合流程，本身不会提供 OS 隔离。

## 价值

适合把设计要求变成可审阅的交付检查：已有网站可先 audit，再决定是否 redesign；改版前后可对照链接、表单与交互是否保留。可复用的价值主要是约束与检查过程，不应由模板数量推断业务转化提升。

## 风险边界

“不像 AI”是审美主张，规则通过也不能证明品牌适配、可访问性全面达标或表单真实送达。技能会读取工程、调用浏览器和可能的外部工具，权限与数据出口取决于宿主。代码为 MIT；照片索引涉及 Wikimedia 的多种许可，使用某张图仍需核署名与共享要求，不能由根许可证一并授权。上游关于其他图库条款的概括未在本轮独立核查。

## 补充建议

选真实页面做同输入前后对照：固定视口、键盘操作、可访问性、表单回执及布局截图，分开记录自动检查和人工判断。先保存原页面与资源来源，对自定义豁免逐项写理由；不要为凑风格删掉必要导航、内容或产品功能。

## 参考资料

- [README.md](https://github.com/Nutlope/hallmark/blob/7ec868225c6caa040558c321ee0fefa0e73f83a8/README.md)。
- [skills/hallmark/SKILL.md](https://github.com/Nutlope/hallmark/blob/7ec868225c6caa040558c321ee0fefa0e73f83a8/skills/hallmark/SKILL.md)。
- [skills/hallmark/scripts/sloplint.mjs](https://github.com/Nutlope/hallmark/blob/7ec868225c6caa040558c321ee0fefa0e73f83a8/skills/hallmark/scripts/sloplint.mjs)。
- [package.json](https://github.com/Nutlope/hallmark/blob/7ec868225c6caa040558c321ee0fefa0e73f83a8/package.json)。
- [LICENSE](https://github.com/Nutlope/hallmark/blob/7ec868225c6caa040558c321ee0fefa0e73f83a8/LICENSE)。
- [仓库 API](https://api.github.com/repos/Nutlope/hallmark)、[发行 API](https://api.github.com/repos/Nutlope/hallmark/releases?per_page=3)；动态元数据只代表本轮采样。
- 事实来源为以上固定文件；价值、风险评估和验证建议为本库工程判断，未作为上游实测结果。
