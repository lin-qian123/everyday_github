# pm-skills

## 项目定位
`pm-skills` 是一个面向 AI agent 的产品管理技能库，试图把 PRD、北极星指标、假设验证、路线图、发布规划、设计冲刺等 PM 工作流封装成可安装、可复用的技能与命令，而不是让每次产品文档都从零 prompt。

- GitHub：https://github.com/phuryn/pm-skills
- 适用人群：产品经理、创始人、AI PM 工具开发者，以及希望把 PM 方法论固化进 agent 工作流的团队。

## 用法

从仓库主页公开信息看，它的入口很偏“技能市场化”：

1. 按仓库 README 指引安装到目标 agent。
2. 通过类似 `/discover`、`/strategy`、`/write-prd`、`/plan-launch`、`/north-star` 的命令调用对应技能。
3. 在技能引导下完成需求发现、战略澄清、PRD 生成、指标定义和发布规划。

项目首页直接把定位讲得很清楚：不是让 AI 多写一点文字，而是让 AI 按固定 PM 框架产出结构化结果。对团队来说，这比“每个人都写一套自己的提示词”更容易形成统一方法。

## 原理

`pm-skills` 背后的工程思路是把产品管理流程做成 agent 可加载的“方法层”：

- 技能化方法论：把 discovery、strategy、execution、launch、growth 等 PM 阶段拆成独立 skill。
- 命令化入口：通过固定 slash command 或等价调用方式减少 prompt 漂移。
- 链式工作流：不仅有单个技能，还强调多步 workflow，把“发现问题 -> 写 PRD -> 定义指标 -> 规划发布”串起来。
- 多代理兼容：README 明确说面向 Claude Code、Cowork，并兼容其他 AI assistant。

这说明它卖的不是一个模板包，而是“把 PM 的结构化思考过程装进 agent”的使用方式。

## 价值

- 对没有成熟 PM 模板的小团队，它可以快速给出一套足够统一的产出结构。
- 对已有方法论但缺少执行一致性的团队，它适合作为“PM 规范的可执行分发层”。
- 对 AI PM 工具开发者，它展示了一个很明确的方向：竞争点不只在模型，而在方法能否被重复调用和持续迭代。

## 风险边界

- 技能库能提升结构一致性，但不保证战略判断本身正确。
- PM 框架越丰富，越容易让团队“流程看起来很完整”，却掩盖真实用户洞察不足的问题。
- 如果团队业务节奏快、文档轻，完整技能链可能偏重，反而增加操作摩擦。

## 补充建议

- 评估这类项目时，先看它是否真的减少了反复 prompt 和返工，而不是只看技能数量。
- 最值得验证的是：输出是否足够贴合你所在行业和团队协作习惯，而不是是否覆盖了所有 PM 术语。
- 从近期热度看，`pm-skills` 代表的是 AI agent 不再只卷“编码”，而开始向产品、策略、文档和组织流程层扩张。

## 参考资料

- 仓库主页：https://github.com/phuryn/pm-skills
- GitHub Trending：https://github.com/trending
- GitHub Topic / agentic-skills 聚合页：https://github.com/topics/agentic-skills
