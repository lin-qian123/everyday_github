# Godcoder

## 1. 定位

`Godcoder` 是一个 local-first 的开源桌面 coding agent，使用 Rust 和 Tauri
构建。它强调代码不经过项目自己的云后端，而是由本机直接调用用户配置的模型
供应商或 OpenAI-compatible API。

与传统“聊天式代码助手”不同，Godcoder 的 README 把重点放在 agent harness
自我改进、内置终端、文件浏览、会话历史、MCP、voice API、graph-aware code
search 和 GUI/OS 自动化模式上。它适合归入 `Coding Agents 与终端助手`。

## 2. 基本用法

项目是桌面应用，使用者需要配置自己的模型密钥或兼容端点。README 描述的典型
流程是启动桌面应用，选择 Ask、Plan、Coding、Freestyle、Harness、CoWork 等
模式，再让 agent 在本机 workspace 中读取、编辑和验证代码。

其中 Harness mode 会创建独立的 `harness-build/` 工作区，CoWork mode 会创建
`cowork-build/` 沙箱，避免直接把实验产物写散到主仓库中。

## 3. 核心原理

Godcoder 的核心思路是把桌面应用、agent loop、本地工具执行和持久记忆结合：

- Tauri/Rust 提供本地桌面壳、文件系统和终端交互。
- 用户自带模型 key 或兼容 API，减少中间平台锁定。
- Harness mode 让 agent 搭建、运行、评估和记录自己的工具链改进。
- ResearchSwarm bridge 提供 `route`、`log`、`recall`、`optimize` 等持久记忆
  接口。
- MCP server 支持把更多外部工具纳入 agent 能力面。

## 4. 工程价值

Godcoder 的价值在于把“本地优先 coding agent”推向更完整的桌面产品形态：
它不只是在终端里跑一个命令，而是提供会话、终端、文件、模式切换、记忆、
回滚和外部工具接入。

对长期 coding agent 工作流来说，本地优先和 BYOK 可以降低代码外泄面，但仍保留
使用主流模型的灵活性。它也提示一个趋势：coding agent 正在从 CLI 命令扩展成
带状态、带权限、带沙箱的桌面工作台。

## 5. 风险边界

本地优先不等于绝对离线。只要接入云模型，代码片段、文件上下文或任务描述仍可能
发送给模型供应商。团队使用时需要确认 provider、日志策略和敏感代码处理方式。

Harness / CoWork 这类自我改进和 GUI 自动化能力也需要明确审批边界。自动点击、
执行命令、发邮件或操作系统级任务都应默认需要人类确认，尤其不能在生产凭据环境中
无隔离运行。

## 6. 补充建议

- 先在非关键仓库试用，观察 diff、日志和回滚能力是否可靠。
- 对接 MCP 前逐个审查 server 权限，避免把本机文件、浏览器或 shell 暴露过宽。
- 将 Harness mode 产物留在单独目录，避免污染主项目。
- 与 `MiMo-Code`、`dao-code`、`learn-agent`、`agterm` 对比，区分桌面 agent、
  终端 agent 和 agent 工作区管理器。

## 7. 参考资料

- GitHub 仓库：<https://github.com/eli-labz/Godcoder>
- 技术栈：Rust、Tauri、MCP、local-first desktop app
- GitHub Topics：`coding-agent`、`desktop-app`、`local-first`、`mcp`
