# Crush 项目速览与上手指南

> 更新日期：2026-03-11（Asia/Shanghai）
> 项目地址：https://github.com/charmbracelet/crush

## 这是什么
`charmbracelet/crush` 是一个终端内的 AI 编码 Agent，目标是把「模型能力 + 本地代码上下文 + 终端工作流」整合到同一条开发路径里。它支持多模型切换、会话管理、LSP 上下文增强、MCP 扩展，并且支持 macOS/Linux/Windows/Android/FreeBSD 等多平台终端。

## 为什么今天值得关注
- GitHub Trending（Go）快照里，`crush` 处于当日热门，显示约 `17,281 stars`、`1,039 forks`、`158 stars today`。
- GitHub 仓库页快照显示已到 `21.2k stars`、`1.3k forks`，说明过去一段时间增长仍在持续。
- 它承接了早期 `opencode` 的演进路线（`opencode` 仓库已归档并指向 `Crush`），社区迁移路径比较清晰。

## 快速上手（最短路径）

## 1) 安装
```bash
# macOS / Linux
brew install charmbracelet/tap/crush

# Node 用户
npm install -g @charmland/crush

# Windows
winget install charmbracelet.crush
```

## 2) 准备模型密钥（任选）
```bash
export OPENAI_API_KEY="..."
# 或
export ANTHROPIC_API_KEY="..."
# 或 GEMINI / GROQ / OPENROUTER / Bedrock / Azure OpenAI 等
```

## 3) 启动
```bash
crush
```
首次进入后，先让它在一个小仓库里做 2 件事：
1. 解释某个模块结构；
2. 只修改一个小函数并展示 diff。

这样可以先验证「上下文理解 + 工具调用 + 变更可控性」。

## 原理（工程视角）

## 1) Agent 执行闭环
Crush 的核心不是“聊天”，而是“可执行循环”：
- 读取当前项目上下文（文件、会话、可用工具）；
- 模型做任务分解与行动选择；
- 调用工具（如文件查看、编辑、命令、MCP）；
- 根据结果继续规划，直到完成或等待人工确认。

## 2) LSP 上下文增强
与纯文本补全不同，Crush 可接入语言服务器（LSP），把类型信息、符号关系、跳转信息引入决策，减少“只靠字符串猜代码”的错误。

## 3) MCP 扩展机制
支持 `stdio/http/sse` 三种 MCP 传输。你可以把内部平台能力（检索、工单、知识库、部署系统）以 MCP 方式接入，让 Agent 不只改代码，还能跨系统执行任务。

## 4) 会话与配置分层
配置优先级（仓库本地 -> 用户全局）便于团队统一默认策略，同时允许个人覆盖。典型做法是：
- 仓库放最小可复用配置（LSP、允许工具白名单）；
- 开发者本机放私有密钥与偏好。

## 与同类工具的差异（简评）
- 强项：终端原生体验好、跨模型灵活、与 Charm TUI 生态结合紧。
- 风险：工具权限放开后，误操作半径会增大；`--yolo` 模式要慎用。
- 实践建议：默认启用人工确认，逐步白名单化高频安全工具。

## 推荐的团队落地方式
1. 先定义“允许自动执行”的工具列表（只读优先）。
2. 给高风险操作加二次确认（写文件、执行 shell、外部调用）。
3. 每周复盘失败样例，更新 `crush.json` 和提示词规范。

## 参考来源
- Crush 仓库：https://github.com/charmbracelet/crush
- GitHub Trending（Go）快照：https://github.com/trending/go
- OpenCode 仓库（已归档并指向 Crush）：https://github.com/opencode-ai/opencode
- GitHub Changelog（Copilot 支持 OpenCode）：https://github.blog/changelog/2026-01-16-github-copilot-now-supports-opencode/
