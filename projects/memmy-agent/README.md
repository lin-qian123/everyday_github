<!-- markdownlint-disable MD013 -->

# memmy-agent

## 定位

`memmy-agent` 是 MemTensor 的个人 AI 记忆中心和本地 agent runtime，目标是在 Cursor、Claude Code、Codex、OpenCode、OpenClaw 等不同 agent 之间共享同一套长期记忆、偏好和项目经验。它把“每个会话重新介绍自己”的问题抽象成跨 agent 的记忆层。

## 用法

- 通过官方桌面应用、CLI/TUI 或 OpenAI-compatible API 使用。
- 导入现有 AI agent 的历史会话，把项目上下文、用户偏好和工作习惯转成可检索长期记忆。
- 通过 MCP、skills 和工具连接扩展到聊天、办公、GitHub、Slack、Notion 等工作流。

## 原理

项目宣称使用 MemOS-powered memory engine 自动收集、理解并结构化用户知识、偏好和项目经验。记忆和 agent runtime 以本地优先方式运行，不同入口共享同一套 agents、memory 和配置；当记忆服务不可用时，系统应显式报错，而不是编造不存在的记忆。

## 价值

- 代表“跨 agent 个人记忆层”从概念走向产品化的路线。
- 对同时使用 Codex、Claude Code、Cursor 的用户有现实价值，可减少上下文重复输入。
- 与 `mem0`、`deja-vu`、`engram`、`personal-model` 等项目形成可比较样本。

## 风险边界

- 记忆导入会读取本地 AI 会话历史，隐私和权限边界必须重点审查。
- “自动结构化偏好”容易把偶然行为固化为长期偏见，需要人工审查和删除机制。
- 项目仍新，跨 agent 格式兼容性、冲突处理和长期迁移能力需要验证。
- 若使用云端模型路由或连接第三方工具，应复核数据上传路径。

## 补充建议

- 第一次使用建议只导入少量低敏项目历史，观察生成记忆是否准确。
- 应建立记忆审计习惯：定期删除过时偏好、错误事实和敏感信息。
- 对团队使用，个人记忆与项目共享记忆应分离，避免把私人上下文注入工作仓库。

## 参考资料

- GitHub：<https://github.com/MemTensor/memmy-agent>
- 项目主页：<https://memmy.bot>
- 文档：<https://memmy.bot/docs/>
