<!-- markdownlint-disable MD013 -->

# oh-my-claudecode

## 定位

oh-my-claudecode（OMC）为 Claude Code 增加任务分工、技能、hooks、状态与验证循环。仓库推荐 Team 分阶段编排，也提供由终端启动的 tmux CLI workers。两种入口需要区分，不能把插件安装和 CLI 安装视作同一个操作。

2026-10-29 快照：TypeScript daily +35 stars；API 40,364 stars / 3,604 forks / 10 open issues（含 PR），MIT。主线 `e10206d8789b` 与 package 均为 5.7.19；发行首项 v5.7.19（2026-10-27 UTC）。本文为文档与 manifest 核读，没有安装插件、派发 workers 或调用模型。

## 用法

在 Claude Code 中逐条输入以下 slash commands，完成后再执行 setup；它们不是 shell 命令。

```text
/plugin marketplace add https://github.com/Yeachan-Heo/oh-my-claudecode
/plugin install oh-my-claudecode
/omc-setup
```

如使用终端 CLI，发行说明给出独立 npm 包：

```bash
npm install -g oh-my-claude-sisyphus@5.7.19
omc setup
```

先在无生产凭据的测试仓库审阅安装 diff，再以单个只读任务验证。`/team` 使用会话内原生团队；`omc team` 启动真实 CLI 进程。Node 版本按固定 package 的 engines 核对；两条安装轨道并用时需分别维护版本。

## 原理

Team 将任务拆为 plan、prd、exec、verify、fix 阶段，以共享任务状态和消息协调执行。skills 与 hooks 影响何时规划、委派和检查，CLI workers 通过 tmux 暴露真实进程。专用 worktree 模式的文档仍标为 opt-in / config-gated，面向 runtime-v2；不能推断所有会话默认各自隔离目录。

## 价值

- 为多执行者开发提供任务生命周期、状态查询和恢复线索。
- 将验证结果与修改关联起来，便于人工检查是否达到明确验收条件。
- 同时保留原生会话和终端 worker 两种工作方式，适合比较不同协作成本。

## 风险边界

- SECURITY 明确列出没有 OS 级沙箱、agents 之间没有安全边界。共享文件系统、MCP 和权限不因任务分工而隔离，worktree 也只隔离 checkout。
- 安全文档说明无人值守的外部 CLI worker 使用自动批准参数；其中 Codex 参数绕过其批准与 sandbox。部署前应核对应 provider 的实际启动方式。
- 文档提供 `OMC_SECURITY=strict` 关闭远端 MCP / 外部 LLM、自动更新并收紧循环等选项；AST 路径限制和 Python blocklist 各有范围，不能扩写成“所有工具已安全”。
- 主线 README 的 provider 列表已有 Antigravity / Cursor，而安全指南重点描述 Codex / Gemini / Grok；对未覆盖 provider 必须另核当前实现。
- setup、hooks 和用户级 skills 会影响其他会话；云端模型仍会接收任务内容，多 worker 也可能放大费用与冲突。

## 补充建议

固定安装轨道与版本，记录 setup 前后配置 diff、provider / MCP 出口、预算和停止条件。用“只读分析 → 单文件修改 → 双执行者互斥修改”逐步验收，检查中断恢复、重复工具动作及真实测试输出。不要以任务状态显示完成替代独立验收。

## 参考资料

- [上游仓库](https://github.com/Yeachan-Heo/oh-my-claudecode)、[GitHub API](https://api.github.com/repos/Yeachan-Heo/oh-my-claudecode)。
- [固定 README：安装与 Team](https://github.com/Yeachan-Heo/oh-my-claudecode/blob/e10206d8789b0ac4e5214eddbfbd203c1b757dea/README.md)、[版本与 Node engines](https://github.com/Yeachan-Heo/oh-my-claudecode/blob/e10206d8789b0ac4e5214eddbfbd203c1b757dea/package.json)。
- [安全配置与自动批准边界](https://github.com/Yeachan-Heo/oh-my-claudecode/blob/e10206d8789b0ac4e5214eddbfbd203c1b757dea/SECURITY.md)、[opt-in worktree 模式](https://github.com/Yeachan-Heo/oh-my-claudecode/blob/e10206d8789b0ac4e5214eddbfbd203c1b757dea/docs/TEAM-WORKTREE-MODE.md)。
- [v5.7.19 发行说明](https://github.com/Yeachan-Heo/oh-my-claudecode/releases/tag/v5.7.19)、[MIT 许可](https://github.com/Yeachan-Heo/oh-my-claudecode/blob/e10206d8789b0ac4e5214eddbfbd203c1b757dea/LICENSE)。
