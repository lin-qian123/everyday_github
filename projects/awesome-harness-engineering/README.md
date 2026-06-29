# awesome-harness-engineering（ai-boost/awesome-harness-engineering）

> GitHub: https://github.com/ai-boost/awesome-harness-engineering  
> 定位：面向 AI agent harness engineering 的资源、模式、模板与案例索引。

## 项目定位

`awesome-harness-engineering` 是一个围绕“agent harness 工程”的资料库。它收集的不是模型榜单，而是围绕 agent 可靠执行所需的脚手架：上下文交付、工具接口、规划产物、验证回路、记忆系统、沙箱、权限、可观测性和人机协作。

这个仓库的出现说明 2026 年的 AI 工程热点正在从“哪个模型更强”转向“怎样设计模型周围的执行环境”。对于 coding agent、browser agent、computer-use agent 或企业内部 agent 平台，它都可以作为架构阅读清单。

## 用法

最直接的使用方式是把它当作索引：

```bash
git clone https://github.com/ai-boost/awesome-harness-engineering.git
cd awesome-harness-engineering
```

然后按主题查阅：

- Foundations：harness engineering 的概念文章和生产实践；
- Design Primitives：agent loop、planning、context delivery、tool design、skills、MCP、memory、permissions；
- Reference Implementations：可参考的 agent harness、教程和模板；
- Security / Sandbox / Permissions：隔离、授权和安全边界；
- Evals / Verification：如何为 agent 行为做测试与评估。

## 核心原理

这个项目的核心不是代码，而是“分类框架”。它把 agent harness 拆成一组可设计、可替换、可验证的工程部件：

- **上下文层**：哪些文件、规范、历史、检索结果应该进入模型；
- **工具层**：工具名、参数、错误面和权限如何影响 agent 行为；
- **状态层**：文件系统、记忆、checkpoint 和任务计划如何延续长任务；
- **执行层**：sandbox、runner、CI 和验证命令如何约束输出质量；
- **治理层**：human-in-the-loop、审计日志、权限提示和风险评分如何降低误操作。

## 价值

它的价值在于给 agent 工程提供共同语言。很多团队已经在做类似事情：写 `AGENTS.md`、建 sandbox、封装 MCP、设计 permission prompt、做 eval、保存任务计划。但如果没有分类框架，这些实践容易散落成“经验贴”。这个项目把它们组织成可复用的工程地图。

对本仓库来说，它值得收录的原因是：它能解释最近一批项目的共同趋势，包括 `codex`、`claude-code`、`skills`、`nvidia-skills`、`SkillSpector`、`background-agents`、`ai-maestro`、`orca` 等。

## 风险边界

- 这是 awesome list，不是可直接部署的生产系统。
- 收录链接的质量不完全一致，需要按来源、日期和适用场景二次筛选。
- “harness engineering” 仍在快速演化，今天的最佳实践可能会被更强模型或新工具抽象替代。
- 资料密集但不保证闭环，真正落地仍需要结合具体仓库、CI、权限系统和数据合规要求。

## 补充建议

- 用它做团队内部 agent 平台设计评审清单，而不是逐条照抄。
- 每次引入新的 coding agent，都按 context、tool、memory、permission、verification 五个维度做一次 harness 审计。
- 对安全相关条目保持高优先级，尤其是工具权限、沙箱逃逸、提示注入和供应链风险。
- 结合本仓库已有 `design-md`、`skills`、`SkillSpector`、`nvidia-skills` 条目看 agent 生态从“工具”向“工程 discipline”的迁移。

## 参考资料

- GitHub 仓库：https://github.com/ai-boost/awesome-harness-engineering
- OpenAI Harness Engineering：https://openai.com/index/harness-engineering/
- Anthropic Building Effective Agents：https://www.anthropic.com/research/building-effective-agents
- Martin Fowler Harness Engineering：https://martinfowler.com/articles/harness-engineering.html
- GitHub API 元数据：https://api.github.com/repos/ai-boost/awesome-harness-engineering
