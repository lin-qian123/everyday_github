<!-- markdownlint-disable MD013 -->

# system-prompts-and-models-of-ai-tools

## 定位

`system-prompts-and-models-of-ai-tools` 是一个收集 AI 产品系统提示词、内部工具描述和模型线索的社区仓库，覆盖 Claude Code、Cursor、Devin、Lovable、Manus、Perplexity、Replit、v0、Windsurf、VS Code Agent 等大量工具。

它与 `system_prompts_leaks` 一样，属于“系统提示词透明度 / 逆向观察”热点，但这个仓库覆盖面更宽，传播热度也更高。

## 用法

使用方式主要是研究和对照，不是安装运行：

1. 打开仓库，按产品名称查找对应提示词或工具说明。
2. 观察不同产品如何描述文件系统、shell、浏览器、MCP、记忆、权限、代码编辑和安全约束。
3. 与官方文档、产品实际行为和最新版本交叉验证，避免把社区捕获文本当成当前线上事实。

## 原理

仓库通过社区贡献、公开捕获和整理，把不同 AI 工具的系统层指令集中成可阅读资料。它的价值不在于“复刻某个产品”，而在于暴露 agent 产品常见结构：

- 任务规划与工具选择规则。
- 文件、命令、浏览器和外部 API 权限边界。
- 代码生成、审查、测试和交付流程约束。
- 安全提示、拒答策略和数据泄露防护。
- 不同产品对用户意图、上下文压缩和多步骤任务的处理方式。

## 价值

- **agent 架构研究**：帮助比较不同产品如何组织 system prompt、tool prompt 和安全策略。
- **工程提示词参考**：团队可以学习其中的任务拆解、验证、权限提示和错误处理模式。
- **安全教育**：让开发者意识到 prompt、工具说明和模型路由也属于攻击面。
- **趋势信号**：高 star 和高 fork 说明开发者正在把系统提示词当成 agent 工程材料，而不只是猎奇内容。

## 风险边界

- 来源不是官方当前规范，可能过期、残缺、被伪造或被二次加工。
- 直接复制商业产品 prompt 可能涉及版权、许可、合规和道德风险。
- prompt 文本并不等于完整产品能力；真实效果还依赖模型、工具实现、检索层、权限系统和后端策略。
- 对安全边界的研究应限于防御、审计和教育，不能用于绕过产品限制或攻击线上系统。

## 补充建议

- 与 `system_prompts_leaks` 对照阅读，重点看重复出现的模式，而不是迷信单个泄露文本。
- 建议把它作为“agent harness 设计反例和参考库”，提炼可公开使用的抽象原则。
- 对任何高风险结论都要回到官方文档、实际产品行为和可复现实验。

## 参考资料

- GitHub 仓库：<https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools>
- 相关项目：<https://github.com/asgeirtj/system_prompts_leaks>
- Trendshift 项目页：<https://trendshift.io/repositories/14084>
