<!-- markdownlint-disable MD013 -->

# scroll-craft

> 上游仓库：[nateherkai/scroll-craft](https://github.com/nateherkai/scroll-craft) · 归类：前端、UI 与 Agent 交互层 · 本页基于 2026-08-23 的上游 README 与 GitHub API 快照整理。

## 定位

`scroll-craft`（上游 README 中的插件名为 `scrollcraft`）是一个 Claude Code skill / plugin，面向滚动驱动网页的设计与实现。它把页面叙事、交互、排版、媒体编码和浏览器截图检查串成一个过程，试图避免由同一模板反复生成相似落地页。

API 快照：约 57 stars、9 forks、0 个开放 issue；创建于 2026-08-22；许可证 MIT。这只是早期公开关注信号，并非 GitHub Trending 排名，也不证明设计质量、兼容性或生产成熟度。

## 用法

上游给出的 Claude Code 安装路径如下；先在独立项目和可回滚的工作区验证：

```sh
/plugin marketplace add nateherkai/scroll-craft
/plugin install nateherk-design
/nateherk-design:scrollcraft

# 本地开发模式
claude --plugin-dir ./plugins/nateherk-design
node scripts/doctor.mjs
node scripts/workspace.mjs --ensure
```

项目要求 Node.js 18+；检查环节还需要 `playwright-core` 与 Chrome。需要将视频做成逐帧随滚动变化时，须使用功能完整的 FFmpeg；生成媒体才需要 `KIE_AI_API_KEY`，也可只用自有图片与视频素材。

## 原理

- skill 要求先定义页面叙事和“情绪曲线”，再在八种互斥的页面语法中选择结构，并为每个作品登记 grammar、导航、hero、节奏、结尾和标志性交互等指纹。
- 引擎以 CSS token 与 `--sc-p` 自定义属性驱动交互；上游主张引擎机制不应为单个项目随意改写，以免页面退化为同一 config 模板。
- headless browser 遍历滚动位置，检查无效滚动、永远半透明的提示、合成后的文字对比度及视频解码问题，并输出 contact sheet。该检查是工程信号，不等同于审美、品牌契合或无障碍的最终验收。

## 价值

- 把“网页是否有交互、能否滚动、文字是否看清”变成可重复检查的交付条件，减少只看首屏截图的验收盲区。
- 通过项目级指纹登记，帮助团队发现相似的 AI 产物并保留设计选择的审阅痕迹。
- 自有素材路径可避免为了演示而强制调用生成 API；预检脚本也有助于及早暴露浏览器、FFmpeg 或依赖安装问题。

## 风险边界

- 上游明确称尚未在 macOS 实际构建；跨平台的路径探测不构成兼容性承诺，应先用小页面验证 Chrome、FFmpeg、字体和视频 scrub 行为。
- 截图和规则检查不能衡量叙事、品牌一致性、可访问性、移动端性能、键盘操作或真实用户理解，人工设计与无障碍审查仍不可替代。
- 生成视频会产生 API 费用，也可能传出提示词和媒体；第三方资产的版权、肖像和音乐授权需要单独确认。
- 插件及其脚本会在本地工程运行。安装前应审阅 revision、依赖与路径，避免让生成任务覆盖正式站点或把密钥写入版本库。

## 补充建议

1. 先在一个静态页面和自有素材上跑 `doctor`、截图检查及手机尺寸回归，保存浏览器、FFmpeg 和插件 revision。
2. 把自动检查扩展为键盘焦点、`prefers-reduced-motion`、LCP/CLS、低带宽和无视频回退等质量门。
3. 将指纹表视为设计讨论输入而非硬性美学裁决；每次例外都应留下品牌或用户需求的理由。
4. 对生成媒体设置预算、内容审核、人工版权检查和发布前的可回滚流程。

## 参考资料

- [上游 README / 安装与限制](https://github.com/nateherkai/scroll-craft)
- [GitHub API 元数据](https://api.github.com/repos/nateherkai/scroll-craft)
- [Claude Code plugins 文档](https://docs.anthropic.com/en/docs/claude-code/plugins)
- [Playwright 文档](https://playwright.dev/docs/intro)
