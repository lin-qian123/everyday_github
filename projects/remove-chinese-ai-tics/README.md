<!-- markdownlint-disable MD013 -->

# remove-chinese-ai-tics

- 仓库：[AAzzAAzzAAzzAA/remove-chinese-ai-tics](https://github.com/AAzzAAzzAAzzAA/remove-chinese-ai-tics)
- 快照：2026-08-09 抓取；GitHub API 显示其创建于 2026-08-08，约 13 stars、2 forks，MIT。数字会随时间变化。
- 分类：Agent 框架与技能生态

## 定位

面向简体中文的 agent skill，用来审计或清理模型化套话、固定句法、客服腔、篇章惯性和格式反射，同时声明要保护事实、数字、术语、引语、语体与人物声口。

## 用法

README 将可安装 skill 放在内层目录：克隆指定 beta tag 后，把该目录复制到 Codex 的 skills 目录，再以 `$remove-chinese-ai-tics` 调用。可要求“只审计不改写”、保守清理、标准/强力改写、严格去口癖或批量处理；安装前若已存在同名 skill 应先备份。

## 原理

规则先锁定不可损坏的信息，再按交互残留、篇章组织、逻辑空转、句法修辞模板和词汇/格式反射分层判断。普通模式依赖局部密度、功能和跨段复现，严格模式处理登记的高置信结构；修复优先删除、合并、具体化和重组，而非机械同义词替换。

## 价值

它把中文生成文本常见的“去模板化”要求转成可复用、带模式区分的指令资产。对需要保留专名、数据与语气的技术文档、编辑流程和创作草稿，先审计再改写的设计可提高人工审稿效率。

## 风险边界

当前为 v0.1.0-beta，规则 ID 与布局仍可能变化。语言流畅不证明事实、版权、引用、风格授权或人物塑造正确；强力改写仍可能改变含义、语气或叙事节奏。不要将其输出直接作为新闻、学术或法律等高风险文本的最终版本。

## 补充建议

先在版本控制下用审计模式抽样，建立领域术语、固定文案、角色语气和不可改数字的回归集；对涉及人名、引语、否定、范围和因果的段落做逐句 diff 审核。把“是否去口癖”保留为作者决策，不以规避检测或伪造人类作者身份为目标。

## 参考资料

- [项目 README](https://github.com/AAzzAAzzAAzzAA/remove-chinese-ai-tics)
- [测试与内容校验说明](https://github.com/AAzzAAzzAAzzAA/remove-chinese-ai-tics/tree/main/tests)
- [GitHub API 元数据快照](https://api.github.com/repos/AAzzAAzzAAzzAA/remove-chinese-ai-tics)
