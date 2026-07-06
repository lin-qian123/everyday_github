<!-- markdownlint-disable MD013 -->

# system_prompts_leaks

## 定位

`system_prompts_leaks` 是一个收集和整理主流 AI 产品系统提示词、工具说明与行为约束的公开资料库。它覆盖 Claude、Claude Code、ChatGPT / Codex、Gemini、Grok、Copilot、Cursor、Perplexity 等产品，并按厂商与产品形态组织。

在今天的 GitHub Trending 中，它的热度来自两个因素：一是提示词透明度本身持续被讨论；二是代码代理、设计代理、浏览器代理开始把大量工具、权限、记忆和安全约束写进系统层，提示词已经从“聊天风格配置”变成 agent 产品架构样本。

## 用法

典型使用方式不是直接复制提示词，而是把它当成研究材料：

1. 对比同一厂商不同模型或产品中的工具声明、拒答边界、隐私约束和任务分解方式。
2. 研究 Claude Code、Codex、Copilot Agent、Gemini CLI 等 coding agent 的工具暴露面。
3. 为自研 agent 的 `AGENTS.md`、system prompt、skill contract、tool policy 提供参考。
4. 审计第三方 agent 产品是否把关键安全边界隐藏在不可见提示中。

## 原理

项目本身不是运行时框架，而是资料库。核心结构是：

- 按厂商目录归档提示词文本。
- 对近期更新项维护时间和链接。
- 对部分版本提供 diff，帮助观察提示词变化。
- 把工具说明、能力声明、策略文本、官方发布文本和社区捕获文本分开归档。

它的工程价值在于可比较性：当不同 agent 都开始暴露 shell、浏览器、文件系统、MCP、skills、长期记忆时，系统提示词是判断产品真实能力边界的重要证据源。

## 价值

- **架构参考**：能看到成熟 AI 产品如何描述工具、权限、记忆、语气、引用和安全策略。
- **安全研究**：适合分析 prompt injection、tool misuse、越权执行和隐藏策略风险。
- **产品研究**：可追踪 Claude Design、GitHub Copilot macOS、Codex、Gemini CLI 等入口的系统层演化。
- **教学价值**：把抽象的“system prompt 设计”变成可阅读案例。

## 风险边界

- 资料来源可能混合官方文本、社区捕获、推断和历史版本，不能默认等同于厂商当前线上实现。
- 公开提示词可能被厂商快速更新，仓库内容具有时效性。
- 直接复制商业产品提示词可能引入版权、合规和品牌风险。
- 对安全策略的研究应限制在防御、审计和产品理解场景，不应帮助绕过线上服务约束。

## 补充建议

- 使用时先看每条提示词的更新日期，再判断是否适合作为当前产品行为证据。
- 做 agent harness 设计时，重点参考工具权限声明、完成定义、用户确认机制和异常处理，而不是照搬人格化文本。
- 和 `SkillSpector`、`bumblebee`、`security-audit-skill` 等项目一起看，可以形成“提示词 + skill + MCP 配置”的完整供应链视角。

## 参考资料

- GitHub 仓库：<https://github.com/asgeirtj/system_prompts_leaks>
- 项目站点：<https://asgeirtj.github.io/system_prompts_leaks/>
- GitHub Trending：<https://github.com/trending>
