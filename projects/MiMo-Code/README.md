# MiMo-Code

## 1. 项目定位

`MiMo-Code` 是小米 MiMo 团队推出的终端原生 AI coding assistant，主张“模型与 Agent 共同演进”。它面向代码阅读、修改、命令执行、Git 操作、持久记忆、任务追踪和多 agent 协作，试图把 coding agent 从一次性对话工具推进到可长期维护项目上下文的开发运行时。

它适合关注两类问题的用户：一是希望在终端中直接使用 AI coding agent 的开发者；二是希望观察模型、记忆、checkpoint、subagent、goal judge 如何被集成到同一 harness 里的工程团队。

## 2. 基本用法

官方 README 给出的快速入口包括一行安装脚本和 npm 全局安装：

```bash
curl -fsSL https://mimo.xiaomi.com/install | bash
npm install -g @mimo-ai/cli
mimo
```

首次启动会引导配置模型通道。项目支持 MiMo Auto、小米 MiMo 平台 OAuth、从 Claude Code 导入认证，以及配置 OpenAI-compatible 的自定义模型提供方。

## 3. 核心原理

`MiMo-Code` 的核心不只是“在终端调用模型”，而是把多个 agent 工作循环组织在一个上下文系统里：

- 主 agent 负责 build、plan、compose 等模式切换，分别对应全权限开发、只读分析、规格驱动编排。
- 持久记忆基于 SQLite FTS5，包含项目记忆、会话 checkpoint、临时 notes 和任务进度。
- 上下文接近窗口上限时，会从 checkpoint、项目记忆、任务进度和最近消息中重建工作上下文。
- subagent 可按需创建并行工作，生命周期、取消和后台执行由系统跟踪。
- `/goal` 命令把停止条件交给独立 judge 评估，减少 autonomous coding 中过早结束的问题。

## 4. 工程价值

`MiMo-Code` 的价值在于把近期 coding agent 领域的几个关键词放到同一个可运行产品里：持久记忆、checkpoint、任务树、subagent、上下文重建、目标判定和多 provider 接入。

对本仓库的长期跟踪而言，它是“模型厂商直接做 coding harness”的代表样本。相比只发布底模或 API，MiMo 把模型、终端体验和 agent runtime 绑定在一起，更接近开发者实际工作流入口。

## 5. 风险边界

- 终端 agent 具备读写代码和执行命令能力，必须在可信仓库和可回滚环境中使用。
- 持久记忆会保存项目结构、规则和任务状态，团队使用前需要明确敏感信息写入边界。
- 从其他工具导入认证虽然降低迁移成本，但也要求用户理解 token、配置文件和供应商权限。
- 自动 checkpoint 与上下文重建能提升连续性，但不能替代测试、代码审查和明确验收标准。

## 6. 补充建议

- 先在小型仓库试用，重点观察命令执行边界、Git 操作习惯和 checkpoint 可读性。
- 将 `MEMORY.md` 与项目已有 `AGENTS.md`、`README.md`、`TODO.md` 的职责分开，避免重复或冲突。
- 和 `codex`、`claude-code`、`qwen-code`、`kilocode` 横向比较，看它的长期记忆和 goal judge 是否真正改善长任务可靠性。
- 若用于团队协作，应把可执行命令、网络访问、密钥读取和提交推送权限纳入统一治理。

## 7. 参考资料

- GitHub 仓库：https://github.com/XiaomiMiMo/MiMo-Code
- 官方网站：https://mimo.xiaomi.com/mimocode
- MiMo Code 博客：https://mimo.xiaomi.com/en/blog/mimo-code-long-horizon
- npm 包：`@mimo-ai/cli`

