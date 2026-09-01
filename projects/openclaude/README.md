<!-- markdownlint-disable MD013 MD034 -->

# openclaude：跨云端与本地模型的多提供商 coding agent CLI

## 项目概览

- 上游仓库：https://github.com/Gitlawb/openclaude
- GitHub API 快照（2026-09-02）：31,251 stars、8,945 forks、71 个开放 issue
- 当前 release：`v0.30.0`
- 主要技术：TypeScript、Node.js 22+、终端工具循环、MCP、VS Code 扩展
- 许可证：复合边界；上游 `LICENSE` 声明原始 Claude Code 派生部分受 Anthropic 商业条款约束，仅 OpenClaude 修改与新增部分在“法律允许范围内”按 MIT 提供

## 定位

OpenClaude 是一个把多家云模型、OpenAI-compatible 端点与 Ollama 等本地后端接入同一终端 coding-agent 工作流的 CLI。它提供文件、Shell、检索、subagent、task、MCP、Web 工具、会话恢复和后台任务，并附带 VS Code 启动集成。

它不是 Anthropic 官方 Claude Code，也不是模型本身；“OpenClaude”名称、兼容路径与上游派生关系需要和官方产品明确区分。

## 用法

上游 npm 安装要求 Node.js 22+：

```bash
npm install -g @gitlawb/openclaude@latest
openclaude
```

启动后可用 `/provider` 保存 provider profile，或通过环境变量接入 OpenAI-compatible 服务和本地 Ollama。长任务可以用 `openclaude --bg` 启动本地后台子进程，再用 `ps`、`logs` 和 `kill` 管理。

首次试用应在无敏感凭据的测试仓库中固定版本，只启用一个低额度模型端点，并逐项审阅文件写入、Shell、网络和 MCP 权限。

## 原理

OpenClaude 用统一消息和工具循环连接不同 provider：模型提出工具调用，CLI 在本机执行文件、Shell、检索或 MCP 操作，再把结果送回模型。provider profile、session transcript、后台任务元数据和日志保存在 OpenClaude 配置目录；可选 repo map 会按代码结构与 PageRank 类指标选择上下文。

后台任务只是本机子进程，不是独立 daemon 或 sandbox；`--fork-session` 也只分叉对话记录，不会复制工作树或隔离文件系统。

## 价值

- 用一套 CLI 对比云模型、聚合网关与本地模型的工具调用表现。
- provider profile、会话恢复与后台任务降低多端点切换成本。
- MCP、subagent、repo map 和 VS Code 入口覆盖较完整的 coding-agent 工作流。
- 对工具协议和本地模型兼容性研究有样本价值。

## 风险边界

- CLI 可执行 Shell、改文件和访问网络；provider 切换不等于权限隔离。
- profile、会话与后台日志可能包含 API key 路径、代码、提示词和工具输出，需按敏感开发数据管理。
- 新安装默认网关、第三方 provider 的价格、保留策略、模型身份和工具兼容性必须分别核验。
- 小型或弱工具调用模型可能在多步任务中误用参数、循环或错误宣称完成。
- 派生代码与许可证不是简单的“整个仓库 MIT”；商业分发或再修改前应单独做法律审查。
- 本页依据上游静态资料、release 与 API 快照，未在本机安装，也未验证 provider 兼容率、代码质量或安全性。

## 补充建议

1. 在容器或低权限测试账户中固定 `v0.30.0`，先只开放只读仓库和低额度 key。
2. 对每个 provider 记录真实模型、base URL、计费、日志保留、tool schema 与上下文上限。
3. 明确区分对话 fork、Git 分支/worktree 和 OS sandbox，不把会话分叉当作文件隔离。
4. 对后台任务设置超时、预算、输出目录和人工验收门，定期清理 transcript 与日志。
5. 在生产或再分发前审查 `LICENSE`、Anthropic 条款和第三方依赖，不沿用 GitHub API 的 SPDX 空值作结论。

## 参考资料

- 仓库与 README：https://github.com/Gitlawb/openclaude
- Releases：https://github.com/Gitlawb/openclaude/releases
- 许可证声明：https://github.com/Gitlawb/openclaude/blob/main/LICENSE
- Advanced Setup：https://github.com/Gitlawb/openclaude/blob/main/docs/advanced-setup.md
- Agent routing：https://github.com/Gitlawb/openclaude/blob/main/docs/agent-routing.md
- 官方 X 账号：https://x.com/gitlawb
