<!-- markdownlint-disable MD013 -->

# StarNet（androoAGI/starnet）

- GitHub：<https://github.com/androoAGI/starnet>
- 抓取快照：2026-09-25，252 stars、64 forks、19 open issues
- 热度信号：GitHub JavaScript Trending 抓取时约 +95 当日 stars
- 版本与许可：代码 MIT；latest GitHub Release / tag 为 `v0.12.4`；名称、logo、station artwork 与 sprites 不随 MIT 授权

## 定位

StarNet 是 local-first 多 Agent 桌面 harness，用像素风空间站把 runtime 状态、团队、能力、交接通道、任务和交付物可视化。其设计把房间解释为 capability-scoped team、走廊解释为授权 handoff lane、摆放对象解释为能力 grant，目标是让 UI 展示和真实执行状态保持一致。

## 用法

可下载 Windows / macOS 签名构建，或从源码运行 Tauri 前端、Rust shell 与本地 Node sidecar；用户配置 OpenRouter 或 OpenAI、Anthropic、Google 等 provider，再为 Agent 分配 workspace、工具、预算、skills、recipes 和 schedule。可选 Discord、Telegram、Slack、Signal、Matrix、MCP 与 Night Shift 扩展远程 / 离席执行，完成物写入可打开的 OUTBOX。

## 原理

桌面 UI 通过 localhost HTTP、NDJSON 与 SSE 消费 sidecar 事件；sidecar 负责 provider 调用、工具、持久化、预算、consent 与 connector。每个 Agent 拥有独立 workspace、transcript、memory 和权限集合，视觉 station 只是同一状态机的投影；release gate 还要求签名、notarization、update artifact 与 QA receipt 绑定候选 commit。

## 价值

它把多 Agent 并发、预算、交接、审批、运行事实和文件交付放在一个可视界面中，适合观察“谁正在做什么、拥有什么权限、花了多少、产物在哪里”。项目公开了隐私文档、QA receipt 与本地数据路径，便于在采用前做比普通产品宣传更细的静态审计。

## 风险边界

- `local-first` 不等于所有数据都加密：transcript、run / cost ledger、memory、voice cache、channel history 和多类状态默认明文落盘；部分 OAuth / sign-in token 也仍是明文。
- provider、chat channel、web fetch、TTS、Spotify、更新检查和可选 StarNet Credits 都会产生网络请求；Credits 路径会通过 StarNet gateway 中继 prompt / reply。
- Night Shift、cron、MCP 与远程频道会扩大无人值守执行面；UI 中的 capability grant 仍需对应 OS、文件、网络和 secret 的真实最小权限。
- README 对“界面不声称无法证明的状态”、签名与 QA gate 的描述是项目方设计 / 流程陈述，本轮未独立运行或验证发行管线。
- MIT 只覆盖代码；品牌、logo、station artwork、sprites 与第三方组件分别适用其他权利，派生发行不能沿用 StarNet 品牌资产。

## 补充建议

在可丢弃系统账户中只配置测试 provider 和空 workspace，先验证 capability、consent、budget、handoff、OUTBOX 与退出后的持久化。关闭 Night Shift、远程频道和不需要的 connectors；检查 app-data 中每类明文文件、OS keychain 与更新请求，再用恶意 MCP、prompt injection、断网和异常退出测试实际 gate 与恢复行为。

## 参考资料

- [GitHub 仓库](https://github.com/androoAGI/starnet)
- [GitHub REST API](https://api.github.com/repos/androoAGI/starnet)
- [v0.12.4 Release](https://github.com/androoAGI/starnet/releases/tag/v0.12.4)
- [安装说明](https://github.com/androoAGI/starnet/blob/feat/harness-backend/INSTALL.md)
- [隐私说明](https://github.com/androoAGI/starnet/blob/feat/harness-backend/PRIVACY.md)
- [安全策略](https://github.com/androoAGI/starnet/blob/feat/harness-backend/SECURITY.md)
- [NOTICE](https://github.com/androoAGI/starnet/blob/feat/harness-backend/NOTICE.md)
- [LICENSE](https://github.com/androoAGI/starnet/blob/feat/harness-backend/LICENSE)
