<!-- markdownlint-disable MD013 MD034 -->

# no-ai-slop：用可点名的模式审阅 AI 写作腔

> 上游仓库：https://github.com/petergyang/no-ai-slop · 归类：办公、商业与行业应用 · 本页基于 2026-09-15 的 README、`SKILL.md`、eval、plugin metadata、release、LICENSE 与 GitHub REST API 静态整理；未对不同模型做盲评。

## 定位

`no-ai-slop` 是一个跨 ChatGPT、Claude Code、Codex 等宿主使用的写作编辑 skill。它把二元对照、空洞开场、伪洞见铺垫、重要性拔高、机械节奏、假深刻收尾等 20 多类模式写成可读规则，支持“最小改写”和“只检测不改写”两种任务。

2026-09-15 的 GitHub 官方 Python Trending 抓取显示约 `+448 stars today`；REST API 快照为 `9,528 stars / 687 forks / 22 open issues`，MIT，最新 release 为 `v1.0.6`（2026-08-01），main 最近 push 快照为 2026-09-02。

## 用法

上游推荐通过 Skills CLI 全局安装，也可以先只阅读 `skills/no-ai-slop/SKILL.md`，再复制到项目级 skill 目录：

```sh
npx skills add petergyang/no-ai-slop --skill no-ai-slop --global --yes
```

安装后可把草稿交给 `/no-ai-slop` 做编辑；若只想审计，可明确要求 `is this slop?`。检测模式应列出规则名、原句与简短修改方向，不改写、不打总分，也不猜文本是否由 AI 生成。

## 原理

- `SKILL.md` 先要求识别文章目的、受众和作者原有词汇、节奏、幽默与不确定性。
- 默认编辑以“最小有效改动”为原则，删除空洞套话、无来源归因、同义词轮换和不必要的结构装饰。
- 检测模式只报告可观察的文本模式；上游明确把“判断作者是不是 AI”排除在能力之外。
- 改写后按 `eval.md` 自检，重点保持事实、含义、声口和格式，而不是追求统一的“漂亮文风”。
- 仓库还含 Codex / ChatGPT plugin metadata 与打包验证脚本，但核心行为仍是宿主模型解释自然语言规则。

## 价值

- 将“读起来像 AI”拆成具体、可引用、可争论的句法与修辞问题，审稿反馈更可操作。
- 明确禁止臆测 AI 作者身份，避免把不可靠的检测概率当作证据。
- 强调保留作者声口与最小修改，适合用作人工编辑前的第一轮问题清单。
- 规则、eval 和 plugin metadata 都在仓库内，可版本化、分叉并加入团队自己的例外。

## 风险边界

- 这是风格启发式，不是 AI 检测器、抄袭检测器、事实核验器或原创性证明。
- 对二元句、片段、重复和固定术语的一刀切清理，可能损伤文学表达、演讲节奏、法律/学术精度或作者刻意风格。
- “更像人”不等于更准确、更有证据或符合机构 AI 辅助披露政策；事实、引文和数据仍需逐项回读。
- 第三方 skill 会改变宿主输出，且全局安装会影响多个项目；更新前应审查规则 diff 与安装范围。
- README 列举的模式和自身 eval 不能证明在所有语言、文化、文体与模型上保持语义。
- 本页没有运行跨模型盲测，也没有验证对中文长文、论文、代码块或引用格式的误改率。

## 补充建议

1. 先在项目级安装，用带数字、引文、否定、术语、代码和个人口头禅的金标文本做语义回归。
2. 将“删模板腔”“保留事实”“保留声口”“不改变立场”分成独立验收项，不使用单一自然度分数。
3. 保留原稿、修改稿和 diff；论文、法律材料、新闻和对外声明必须人工逐句确认。
4. 与仓库已有 `humanizer`、`kill-ai-slop` 做同稿盲评，比较误删、漏报、事实漂移和主观偏好，而不是只比较输出流畅度。

## 参考资料

- 上游 README：https://github.com/petergyang/no-ai-slop
- Skill 源文件：https://github.com/petergyang/no-ai-slop/blob/main/skills/no-ai-slop/SKILL.md
- Eval 说明：https://github.com/petergyang/no-ai-slop/blob/main/skills/no-ai-slop/eval.md
- `v1.0.6` release：https://github.com/petergyang/no-ai-slop/releases/tag/v1.0.6
- GitHub REST API：https://api.github.com/repos/petergyang/no-ai-slop
- LICENSE：https://github.com/petergyang/no-ai-slop/blob/main/LICENSE
