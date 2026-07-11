# tau

<!-- markdownlint-disable MD013 -->

## 定位

`tau` 是 Hugging Face 组织下的极简终端 coding agent，也是一个“教你如何构建 coding agent”的可读实现。它可以读文件、改代码、运行命令、保持会话历史，并把 provider、agent brain、coding session 和 TUI 分层。

截至 2026-07-12，GitHub API 显示该仓库约 1416 stars、147 forks，创建于 2026-06-11，许可证为 MIT。README 强调 `tau_ai -> tau_agent -> tau_coding` 的分层边界。

## 用法

Tau 发布在 PyPI，命令名为 `tau`，要求 Python 3.12+。

```bash
uv tool install tau-ai
tau --version
```

也可以用 `pipx` 或 `python -m pip`：

```bash
pipx install tau-ai
```

进入项目目录后运行：

```bash
cd my-project
tau
```

一次性 print 模式：

```bash
tau -p "summarize the repository"
```

## 原理

Tau 重点在可读架构：`tau_ai` 抽象模型 provider 流，`tau_agent` 负责消息、工具、事件、loop、harness 和 session，`tau_coding` 把这些包装成真实 coding app，包括 CLI、TUI、文件 / shell 工具、配置、skills 和落盘会话。

它不是最大而全的 coding agent，而是适合学习 agent loop 与宿主工程边界的参考实现。

## 价值

- 适合教学、二次开发和理解 coding agent 内部结构。
- Hugging Face 组织背书让它在 agent 教程项目中更值得关注。
- 分层清楚，便于比较 `AgentHarness`、`CodingSession`、`TUI` 的职责。
- MIT 许可证，适合拿来做实验型 agent harness。

## 风险边界

- 生产能力不能按 Claude Code、Codex、OpenHands 等成熟工具预期。
- Python 3.12+、provider 配置和本地命令权限需要用户自行处理。
- 教学型架构不代表安全沙箱、长期任务调度和团队协作已经成熟。

## 补充建议

- 与 `learn-agent` 横向比较：`learn-agent` 更像教程路线，Tau 更像可运行且分层清楚的参考实现。
- 适合作为“如何写一个 coding agent”的课程或内部分享样本。
- 后续观察其是否扩展 MCP、skills、sandbox 和 provider-neutral 评测。

## 参考资料

- GitHub 仓库：<https://github.com/huggingface/tau>
- 文档：<http://twotimespi.dev/>
- PyPI：<https://pypi.org/project/tau-ai/>
