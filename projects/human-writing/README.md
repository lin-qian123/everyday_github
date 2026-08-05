# human-writing（活人感写作）

- 仓库：[KKKKhazix/human-writing](https://github.com/KKKKhazix/human-writing)
- 快照：2026-08-06 抓取；GitHub API 显示其创建于 2026-08-05，约 1,013 stars、99 forks，MIT。数字会随时间变化。
- 分类：Agent 框架与技能生态

## 定位

面向中文创作与改稿的 Agent Skill。它把材料充足性、段落推进、口语化中文和成稿自检写成可安装规则，目标是降低空泛、重复和模板化“AI 味”。

## 用法

可让兼容 Agent 直接安装仓库，或将 `human-writing/` 完整复制到本机 skills 目录；随后以“使用 `$human-writing`，把材料写成……”调用。现实题材先提供出处、采访记录或数据，虚构题材则明确人物、场景与冲突；提交前运行仓库的 `check_prose.py` 只作硬规则提示。

## 原理

Skill 先区分现实写作与虚构写作，再要求每段新增事实、动作、例子或后果；修订阶段检查重复解释、句长节奏、连词密度和常见翻案式句型。它是提示词/规则与轻量静态检查，不是事实检索器或文风质量的客观评测器。

## 价值

将“先有材料，再有文风”的流程显式化，适合公众号、博客、评测、科普和口播初稿的可重复审阅；MIT 许可和轻量目录也便于团队按自身语体扩展。

## 风险边界

“像人写”不等于真实、准确或原创；规则可能误伤刻意的修辞与专业文体，也无法核验引语、数据和版权。不要将检查脚本通过视为事实审核、抄袭检测或发布许可。

## 补充建议

把事实核验、引用清单和作者审阅保留为独立 gate；用真实历史文章做盲评，观察误报、编辑返工和读者理解，而非只追求规避某些词式。安装第三方 skill 前仍应审阅脚本与其可读取的本地路径。

## 参考资料

- [项目 README](https://github.com/KKKKhazix/human-writing)
- [SKILL.md](https://github.com/KKKKhazix/human-writing/tree/main/human-writing)
- [GitHub API 元数据快照](https://api.github.com/repos/KKKKhazix/human-writing)
