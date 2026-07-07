<!-- markdownlint-disable MD013 -->

# oh-my-openagent

## 定位

`oh-my-openagent` 是一个面向复杂代码库的开源 coding agent / harness 项目，README 中同时使用 `omo` 与 `lazycodex` 概念，强调低 token 消耗、多工具接入和面向 Codex、OpenCode 等宿主的 agent 工程体验。

它反映了当前 coding agent 赛道的一个分支：不只比模型能力，而是比上下文压缩、任务编排、TUI/IDE 体验、权限和多模型路由。

## 用法

项目以 TypeScript 为主，适合在本地开发环境中作为 agent harness 使用。它面向 Claude、Codex、OpenCode、Gemini、Cursor 等工具生态，提供命令行 / TUI、编排、技能和复杂代码库支持。

由于项目仍在快速变化，实际接入前应以仓库 README、安装脚本和 release 说明为准，先在非关键仓库验证安装、权限、模型配置和回滚方式。

## 原理

从项目描述和代码结构看，它把 coding agent 工作流拆成几个层次：

- 模型与 provider 接入。
- 面向大代码库的上下文选择与压缩。
- agent task loop 与工具调用。
- TUI / IDE 交互界面。
- skills、规则和 orchestration 配置。
- 与 OpenCode、Codex 等工具链的兼容层。

核心目标是让 agent 在复杂仓库中减少无效上下文、减少工具调用浪费，并保持更强的交互控制。

## 价值

- **token 预算导向**：把“少花 token 做长任务”作为产品卖点，切中真实开发痛点。
- **多宿主兼容**：不是绑定单一模型或单一 IDE，而是接入 Codex、OpenCode、Claude 等生态。
- **复杂代码库场景**：更关注真实仓库导航、上下文管理和持续协作。
- **开源可改造**：适合研究 coding agent harness 如何组织前端、运行时和工具层。

## 风险边界

- 项目定位和命名较激进，实际成熟度需要通过真实仓库任务验证。
- 多模型、多工具兼容会带来配置复杂度、权限暴露和行为差异。
- 若缺少稳定测试和安全边界，agent harness 可能放大错误命令和错误代码修改。
- 目前更适合技术用户试验，不宜直接接入生产仓库的自动合并流程。

## 补充建议

- 与 `opencode`、`qwen-code`、`dao-code`、`Godcoder` 对照，关注它是否能证明更低 token 消耗和更稳定上下文选择。
- 在团队试用时，应强制只读模式、diff 审查和 CI 验证，逐步开放写权限。
- 如果后续项目文档稳定，应补充安装路径、配置样例和真实 benchmark。

## 参考资料

- GitHub 仓库：<https://github.com/code-yeongyu/oh-my-openagent>
- OpenCode：<https://github.com/sst/opencode>
- OpenAI Codex：<https://github.com/openai/codex>
