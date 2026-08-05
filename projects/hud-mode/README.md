# hud-mode

- 仓库：[adrida/hud-mode](https://github.com/adrida/hud-mode)
- 快照：2026-08-06 抓取；GitHub API 显示其创建于 2026-08-05，约 8 stars、0 forks，MIT。数字会随时间变化。
- 分类：Coding Agents 与终端助手

## 定位

面向 OpenCode、Claude Code 和 Codex 的零依赖终端 heads-up display。它用紧凑仪表显示 agent 的状态、模型、token、耗时与上下文，并允许在运行中排队消息或中断会话。

## 用法

需 Node.js 18+ 及至少一个受支持 CLI。按 README 执行 `npm install -g adrida/hud-mode && hud install` 后，用 `hud "fix the failing CI"` 开启会话，`hud -r` 恢复当前目录的最近会话；在面板中可用 `/gauges` 控制仪表，`/hud` 或对应 handoff 入口返回原 CLI。

## 原理

工具以各 CLI 的 JSON/stream 事件流更新统一面板，使用各自的原生 resume 机制维持会话；全屏 CLI 与 HUD 之间通过本地 handoff 文件、hook 或命令模板切换。它不修改 agent 的模型推理，只改变会话可视化与交互入口。

## 价值

适合多轮终端任务中减少滚屏、观察 agent 是否卡在权限/工具/上下文问题，并在不中断主任务的情况下投递后续指令。会话链接账本和状态仪表也能辅助人工回看。

## 风险边界

安装会修改 `~/.claude`、`~/.codex` 与 OpenCode 的用户级配置，并保存 handoff、链接及部分会话元数据；`--danger` 会跳过底层 CLI 的部分安全机制。HUD 的“状态正常”不能替代测试、代码审查或权限审计。

## 补充建议

先在临时用户目录审阅 `hud install` 的 diff 与备份/卸载行为；避免让链接账本记录含 token 的 URL。将仪表用于定位和排障，而把验收仍放在独立构建、测试、diff 和人工批准上。

## 参考资料

- [项目 README](https://github.com/adrida/hud-mode)
- [演示 GIF](https://raw.githubusercontent.com/adrida/hud-mode/main/docs/hud-demo.gif)
- [GitHub API 元数据快照](https://api.github.com/repos/adrida/hud-mode)
