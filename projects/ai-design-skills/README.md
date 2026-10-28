<!-- markdownlint-disable MD013 -->

# ai-design-skills

## 定位

ai-design-skills 是供 Claude Code、Cursor、Codex、Windsurf 等读取的 Markdown 设计规则集合。2026-10-29 的 README 仍列一个核心技能 `landing-page-design`，覆盖需求收集、页面结构、转化文案以及字体、间距、动效；已有站点改版是另一个关联仓库的方向。

本页在原 2026-07-30 页面上刷新。今日综合 daily 榜 +1,938 stars；API 11,054 stars / 793 forks / 7 open issues（含 PR），MIT。核读主线 `ded7efc9d5c0` 的 README、技能正文与 LICENSE；发行 API 本轮为空。增星不等于转化率、审美或可访问性已验证。

## 用法

先阅读技能正文，按品牌、中文排版、组件库和目标用户裁剪，再限定到项目加载。Claude Code 的上游安装路径为：

```bash
mkdir -p .claude/skills
git clone https://github.com/elayadesign/ai-design-skills.git /tmp/ai-design-skills
cp -r /tmp/ai-design-skills/skills/landing-page-design .claude/skills/
```

实际采用时先固定已审阅的 commit。对于已有 Codex 项目，应把适用设计约束合并进既有 AGENTS.md，审查 diff 并保留原规则；README 的“复制到规则文件”不应理解成覆盖原文件。Cursor 等入口以实际宿主支持为准。本轮未安装或生成网页。

## 原理

Part A 先确定主要行动、受众、证据和页面论证，再选择布局与文案；Part B 给出具体视觉 token 和动效规范。技能同时约束 build order，要求按 section 更新。它提供的是 Agent 上下文与决策约束，不包含验证这些规则效果的独立 UI 运行时。

## 价值

- 将隐含的设计偏好写成可审阅、可版本管理的项目资产。
- 在生成前明确受众、主要 CTA 和证明材料，减少反复重建整页。
- token 表与动效规则可作为团队讨论起点，但仍需结合现有设计系统。

## 风险边界

- 技能说明把适用范围扩展到所有 Web UI；硬性字体选择、禁止斜体 / 背景渐变、固定字号和必需动效段落属于该作者的风格政策，并非普适可用性标准。
- 禁用若干西文字体不解决中文字体回退；字号向下吸附也可能影响阅读，需要真实设备、缩放和可访问性检查。
- 虽要求遵守 prefers-reduced-motion，但仅有规则文本不能证明实现已满足键盘操作、对比度或 WCAG。
- 转化文案示例、统计、客户 logo、评价和退款承诺必须有真实依据，不能由“高转化页面”目标诱导虚构。
- README 称无需署名，而实际 MIT LICENSE 要求在软件副本或重要部分保留版权 / 许可通知；复制分发技能时应遵从许可正文，生成站点所用素材另核许可。
- 规则质量和模型执行质量不同；安装第三方 skill 不代表宿主权限被收窄。

## 补充建议

保留符合品牌的部分，并明确哪些条款可覆盖、哪些由项目或用户要求决定。以同内容的基线页 / 技能页比较任务完成率、移动端、键盘、阅读与加载表现；没有实验时不报告转化提升。所有商业陈述逐条关联真实来源。

## 参考资料

- [上游仓库](https://github.com/elayadesign/ai-design-skills)、[GitHub API](https://api.github.com/repos/elayadesign/ai-design-skills)。
- [固定 README：范围与安装](https://github.com/elayadesign/ai-design-skills/blob/ded7efc9d5c02761c41a03caf3b78f9259ab8828/README.md)。
- [固定技能：策略、视觉系统与 credits](https://github.com/elayadesign/ai-design-skills/blob/ded7efc9d5c02761c41a03caf3b78f9259ab8828/skills/landing-page-design/SKILL.md)。
- [MIT 许可正文](https://github.com/elayadesign/ai-design-skills/blob/ded7efc9d5c02761c41a03caf3b78f9259ab8828/LICENSE)。
