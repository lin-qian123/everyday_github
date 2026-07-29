# ai-design-skills

## 定位

`ai-design-skills` 是一组面向 Claude Code、Cursor、Codex、Windsurf 等文本规则型 coding agent 的设计技能。目前公开的核心技能是 `landing-page-design`：从需求问询、页面结构、转化文案到字体、间距、圆角与动效，提供一份可复制的设计约束。

截至 2026-07-30，GitHub API 显示仓库创建于 2026-07-29，约 154 stars、9 forks，MIT 许可证；这是早期开发者信号，不等同于设计质量或生产可用性的独立评测。

## 用法

按宿主把某一技能文件放入规则目录：Claude Code 可复制到 `.claude/skills/`，Cursor 可复制 `SKILL.md` 到 `.cursor/rules/`；Codex 等工具则应按本机项目规则入口加载。先审阅技能中的品牌、可访问性与动效规则，再在小页面上验证。

```bash
git clone https://github.com/elayadesign/ai-design-skills.git /tmp/ai-design-skills
cp -r /tmp/ai-design-skills/skills/landing-page-design .claude/skills/
```

## 原理

它不是生成 UI 的运行时库，而是把设计决策写进 agent 可读取的 Markdown：先收集目标与受众，再约束信息层级和视觉 token，最后让模型按同一规则产出页面。仓库把每项技能设计为独立目录，便于只安装所需部分。

## 价值

- 为“从提示词到网页”的过程加入可审阅、可版本控制的设计约束。
- 可将团队的字体、间距、色彩和动效偏好沉淀为跨工具复用的轻量资产。

## 风险边界

- Markdown 规则不能替代真实用户研究、品牌审核、可访问性测试或浏览器兼容性测试。
- 将第三方规则直接写入全局 agent 配置可能改变其他仓库的生成行为；应限定到项目级目录并做 diff 审查。
- 当前项目内容仍少，不能据此推断其覆盖复杂设计系统或产品迭代的能力。

## 补充建议

将技能与现有设计 token、组件库和视觉回归测试配套使用。对 agent 生成的页面至少检查对比度、键盘导航、移动端断点、文案真实性及许可来源。

## 参考资料

- GitHub：<https://github.com/elayadesign/ai-design-skills>
- GitHub API 快照：<https://api.github.com/repos/elayadesign/ai-design-skills>
