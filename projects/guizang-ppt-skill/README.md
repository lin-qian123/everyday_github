# Guizang PPT Skill（op7418/guizang-ppt-skill）

- GitHub: https://github.com/op7418/guizang-ppt-skill
- 记录日期: 2026-04-29 (Asia/Shanghai)

## 这是什么

`guizang-ppt-skill` 是面向 Claude Code/Codex 等 Agent 的演示稿技能包，目标是把提示词转换成“电子杂志风”的横向翻页单文件 HTML 演示。

## 热度信号

1. GitHub 仓库约 `3.8k stars`（2026-04-29 抓取）。
2. GitTrend（2026-04-25）显示其当日增长处于前列（+227/day 量级）。

## 怎么用（最短路径）

```bash
npx skills add https://github.com/op7418/guizang-ppt-skill --skill guizang-ppt-skill
```

然后直接在 Agent 中用自然语言触发：
1. “帮我做一份杂志风 PPT”
2. “生成一个 horizontal swipe deck”

## 核心原理

1. 模板驱动：`assets/template.html` 提供完整视觉与交互骨架。
2. 工作流约束：通过 `SKILL.md` 把需求澄清、布局选择、自检流程标准化。
3. 质量门禁：`references/checklist.md` 按 P0/P1/P2/P3 分级校验，减少视觉回归。

## 适用场景

1. Demo Day、产品发布、内部分享等高视觉表达场景。
2. 需要快速输出单文件可分发演示稿的场景。

## 价值与风险

价值：
- 非设计背景用户也能快速得到高完成度页面。
- Agent 可复用模板与流程，产出一致性高。

风险：
- 静态 HTML 在多人协作和复杂数据演示上受限。
- 风格强约束下，自定义自由度有限。

## 我认为有价值的补充材料

1. 增加“数据密集型”布局变体（表格、长图、注释层）。
2. 建立主题 A/B 检查脚本，自动发现对比度和可读性问题。
3. 给配图流程补充版权与来源标注模板。

## 参考来源

- https://github.com/op7418/guizang-ppt-skill
- https://gittrend.io/
