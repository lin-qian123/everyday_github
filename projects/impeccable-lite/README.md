# impeccable-lite

## 定位

`impeccable-lite` 是面向 coding agent 的单文件前端设计 skill。它从 `pbakaus/impeccable` 的设计判断层提炼出排版、色彩、布局、交互、无障碍和验收约束，刻意不包含插件、hook、CLI 或在线编辑器。截至 2026-08-02 的 GitHub API 快照：项目创建于 2026-08-01，约 41 stars、0 forks，Apache-2.0。

## 用法

将仓库的 `SKILL.md` 放入所用 agent 的技能目录（例如 Codex 的 `.agents/skills/impeccable-lite/`），重开会话后用 `$impeccable-lite` 显式调用，或在前端任务中让 agent 自动路由。没有 skills 支持的工具可把内容放入项目指令；这会变成常驻规则，应先评估是否会干扰非 UI 任务。

## 原理

它把“避免模板化 AI UI”的经验写成可加载文本约束：先确定明确视觉方向，再约束字体、颜色、层级、响应式、状态与验证。它是提示与审查框架，不会生成运行时 lint、浏览器证据或自动修复。

## 价值

- 单文件、低依赖，适合不需要完整插件生态的团队做设计基线试验。
- 将审美判断与可访问性、性能、边界状态一并纳入 agent 的实现提示。

## 风险边界

- 这是独立衍生项目；功能和维护节奏不等同于原版 `impeccable`。
- skill 的文字建议不能取代真实设备测试、可访问性审计或设计评审。
- 不要让“视觉更好”掩盖表单校验、隐私提示和业务错误态缺失。

## 补充建议

用一个小页面对照测试，保留截图、Lighthouse/axe 结果和人工评审意见；若需要确定性检测、浏览器编辑或生命周期 hook，再评估原版项目。

## 参考资料

- GitHub：<https://github.com/ilindaniel/impeccable-lite>
- 上游项目：<https://github.com/pbakaus/impeccable>
- GitHub API 快照：<https://api.github.com/repos/ilindaniel/impeccable-lite>
