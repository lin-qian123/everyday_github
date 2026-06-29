# ai-maestro（23blocks-OS/ai-maestro）

> GitHub: https://github.com/23blocks-OS/ai-maestro  
> 官网: https://ai-maestro.23blocks.com  
> 定位：面向多终端、多机器、多 agent 协作的 AI agent 控制面与编排系统。

## 项目定位

`ai-maestro` 试图解决一个越来越常见的问题：当团队同时运行 Claude Code、Codex、Aider、Cursor、OpenClaw、Hermes 等多个终端型 agent 时，人会变成“消息中转站”。项目把这些 agent 收到一个 dashboard 中，提供会话可见性、跨机器发现、agent-to-agent messaging、持久记忆和代码图谱能力。

它不是单一 coding agent，而是 agent-first organization 的控制面。换句话说，它关注的不是“模型怎么回答”，而是“几十个 agent 怎么被创建、观察、迁移、协作、记忆和治理”。

## 用法

官方 README 给出的快速安装方式是：

```bash
curl -fsSL https://raw.githubusercontent.com/23blocks-OS/ai-maestro/main/scripts/remote-install.sh | sh
```

安装后会启动本地 dashboard 和服务，默认入口是：

```text
http://localhost:23000
```

基础环境要求包括 Node.js 18+ 与 tmux。项目也支持手工 clone 后用 `yarn install` / `yarn dev` 启动，适合希望审计安装脚本或做二次开发的用户。

## 核心原理

- **统一控制面**：把本地 tmux session、Docker 容器、云端实例和独立 agent 汇总到同一个 dashboard。
- **多机器 mesh**：不是把所有 agent 都塞到一台机器，而是让多台机器互相发现，按机器能力承载不同任务。
- **Agent Messaging Protocol（AMP）**：通过类似邮件/消息的协议让 agent 之间传递上下文、结论和任务请求，降低人工复制粘贴成本。
- **持久记忆与代码图谱**：为 agent 提供跨会话状态、代码结构检索和自动文档能力，减少“每次启动都失忆”的问题。
- **技能与脚本集成**：安装过程会带入 Claude Code plugin、skills 和 CLI scripts，说明它更像一个工作台生态，而不是单点工具。

## 价值

`ai-maestro` 的价值在于把 agent 协作问题从“开更多终端”推进到“需要组织级运行时”。对于每天运行多个 coding agent 的团队，它可以作为观察如下问题的样本：

- agent 如何命名、分组、切换和回收；
- 不同机器上的 agent 如何同步状态；
- agent 之间何时直接通信，何时仍需要人类仲裁；
- 记忆、代码图谱、文档生成是否能减少重复上下文灌入；
- agent 控制面是否会成为 IDE 之外的新入口。

## 风险边界

- 安装脚本会拉起本地服务并改动用户环境，生产机器上应先审计脚本。
- 多 agent 协作容易放大错误传播：一个 agent 的错误结论被另一个 agent 继续执行，会比单 agent 更难定位。
- 持久记忆和跨机器同步涉及项目代码、日志与任务上下文，应明确数据边界与权限策略。
- AMP、mesh、gateway 等机制还在生态早期，不能默认等同于成熟的企业协同协议。
- dashboard 让 agent 更易扩张，但不能替代测试、代码审查和安全门禁。

## 补充建议

- 先用一个低风险仓库验证 tmux / Docker discovery 与消息传递，再接入真实业务仓库。
- 给每个 agent 固定职责、工作目录和可写边界，避免多 agent 同时改同一片代码。
- 对跨 agent 的结论建立“证据链”习惯：消息里应包含文件、命令、日志或测试结果链接。
- 与现有 `codex`、`claude-code`、`orca`、`background-agents` 做横向对照，看它更适合个人多终端管理还是团队级调度。

## 参考资料

- GitHub 仓库：https://github.com/23blocks-OS/ai-maestro
- 项目官网：https://ai-maestro.23blocks.com
- 最新 release v0.35.54：https://github.com/23blocks-OS/ai-maestro/releases/tag/v0.35.54
- GitHub API 元数据：https://api.github.com/repos/23blocks-OS/ai-maestro
