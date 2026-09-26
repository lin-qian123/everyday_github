<!-- markdownlint-disable MD013 -->

# Interface Design（Dammyjay93/interface-design）

> 上游仓库：<https://github.com/Dammyjay93/interface-design> · 归类：前端、UI 与 Agent 交互层 · 本页基于 2026-09-27 的 GitHub API、README、skill 内容、Release 与 LICENSE 静态整理，未安装 skill、生成界面或验证示例前后对比。

- 抓取快照：5,734 stars、370 forks、8 open issues。
- 热度信号：GitHub Shell Trending 抓取时约 +6 当日 stars。
- 版本与许可：MIT；latest Release / tag 为 `v2026.6.12.1248`，默认分支最后推送时间为 2026-06-20。

## 定位

Interface Design 是面向 Claude Code、Codex 等 coding agent 的产品界面设计 skill，聚焦 dashboard、app、tool 和 admin panel，而非营销站点。它用原则、审查流程和 `.interface-design/system.md` 记住 spacing、color、surface、depth 与 component pattern，降低跨会话设计漂移。

## 用法

上游推荐用 `npx skills add https://github.com/dammyjay93/interface-design --skill interface-design` 安装，并可指定 Codex / Claude Code 或全局 scope。使用时显式调用 skill，让 Agent 先读取项目与已有 system 文件、提出视觉方向，再在确认后构建或执行 `design-review` / `design-deslop`。安装前应先用 `--list` 预览并审查 skill 文件。

## 原理

skill 把 craft principles、视觉方向探索、review criteria 与持久设计 token 串成工作流。首次会话从项目上下文提出方向，用户确认后生成一致组件，并可把决策写入 `.interface-design/system.md`；后续会话读取该文件复用 spacing、surface、border 与 pattern。若宿主有 image-generation tool，还可生成方向板和 critique paintover。

## 价值

它把“让 Agent 做好看一点”改成可记录、可复用、可审查的设计决策，尤其适合已有产品 UI 的持续迭代。持久 system 文件有助于减少按钮高度、spacing、色阶和深度策略漂移，review / deslop 模式也能形成比一次性 prompt 更稳定的检查清单。

## 风险边界

- README 明确 skill 继承 coding agent 的全部权限；skill 不是只读 style guide，安装器和 Agent 都可能修改用户级配置与项目文件。
- `.interface-design/system.md` 只是项目约定，可能固化早期错误、过时 brand token 或不可访问的颜色 / motion；跨会话一致不等于正确。
- “专业”“视觉层级”和 before / after 主要是上游主张，本轮未做用户研究、专家盲评或可用性实验。
- 生成方向板、字体、图像与第三方参考会带来网络、版权、品牌和隐私边界；代码 MIT 不覆盖外部素材。
- 默认审美规则不能替代 WCAG、responsive、internationalization、loading / error / empty states、真实数据密度和性能验证。

## 补充建议

把 skill 固定到 commit，在副本项目中审查安装 diff 和首次 `system.md`。将 design tokens 与现有组件库 / brand source 对齐，并在每次改动后跑 keyboard、screen reader、contrast、zoom、mobile viewport、reduced-motion 与 performance 检查；任何持久新 pattern 都由人工确认后再写入系统文件。

## 参考资料

- [GitHub 仓库](https://github.com/Dammyjay93/interface-design)
- [GitHub REST API](https://api.github.com/repos/Dammyjay93/interface-design)
- [项目站点与示例](https://interface-design.dev)
- [v2026.6.12.1248 Release](https://github.com/Dammyjay93/interface-design/releases/tag/v2026.6.12.1248)
- [核心 skill](https://github.com/Dammyjay93/interface-design/tree/main/.claude/skills/interface-design)
- [LICENSE](https://github.com/Dammyjay93/interface-design/blob/main/LICENSE)
