<!-- markdownlint-disable MD013 -->

# T3 Code（pingdotgg/t3code）

> 上游仓库：<https://github.com/pingdotgg/t3code> · 归类：Coding Agents 与终端助手 · 本页基于 2026-10-04 的 GitHub API、README、权限 / 远程访问 / 架构文档、隐私政策、Release 与 LICENSE 静态整理，未安装客户端、连接真实 Agent、登录 provider、开启远程访问或执行代码。

- 抓取快照：24,660 stars、6,436 forks、1,975 open issues。
- 热度信号：GitHub 综合 / TypeScript Trending 抓取时约 +251 当日 stars。
- 版本与许可：MIT；latest stable Release 为 `v0.0.45`，首个 tag 为预览版 `v0.0.46-preview.20261002.2598`。

## 定位

T3 Code 是本地 Agent harness 的跨端控制面：server 驱动机器上的 Codex、Claude Code、Cursor、Grok Build、OpenCode 与 Antigravity，用户通过 Web、Electron、iOS 或 Android 查看线程、审批、终端、Git 和远程环境。它复用各 provider 已有订阅与登录，而不是提供一个新模型。

## 用法

上游提供安装脚本、`npx t3@latest`、Homebrew、winget、deb 与 AUR；安装至少一个 provider CLI 并先完成登录，再运行 `t3` 启动本地 server / Web UI。`t3 service install` 可常驻后台，T3 Connect、LAN / Tailscale pairing 或 desktop-managed SSH 可让手机和其他客户端控制远端环境。

## 原理

工作区文件、Git、终端、provider 进程与凭据归 server 所在环境所有；客户端通过 authenticated RPC 订阅状态和发命令。provider adapter 把不同 Agent 的事件、审批与能力归一化，event log / projection 保存运行状态，effect worker 在意图提交后执行外部副作用；因此“命令已确认”不代表 provider 或后续 checkpoint 已完成。

## 价值

它把多种 coding agent、多个环境和多端监督放到同一界面，并保留 provider 原生执行位置。对同时管理本机、SSH 主机和移动端审批的用户，统一线程、连接、Git 与通知状态能降低在多个 CLI 之间切换的成本。

## 风险边界

- 权限文档写明新线程初始默认是 `Full access`，命令和编辑可不经审批；`Supervised`、`Auto` 等模式又因 provider 能力不同而行为不同，UI 标签不能替代底层 sandbox 与实际回调核验。
- 远程客户端控制的是拥有真实工作区、Git、终端和 provider 凭据的环境；pairing、T3 Connect 或 SSH 连通后，失陷客户端的影响范围取决于 server 权限和 provider 登录态。
- T3 Connect、推送和托管 Web 属于可选云服务；隐私政策列出身份、连接、设备 / 应用版本及服务日志等数据，并说明第三方模型与身份 provider 受各自条款约束。
- 安装脚本、自动更新、AUR / package manager 与 server 下载形成多条供应链；stable Release 与 preview tag 已有版本时差，应固定具体制品与校验值。
- 项目 README 明确仍非常早期、应预期 bug；高 issue 数与公开热度不证明跨平台、恢复、权限或远程连接已达到生产可靠性。
- 本轮未验证 approval、Git rollback、T3 Connect、mobile notification、SSH reconnect 或多客户端版本协商的真实行为。

## 补充建议

先在无生产凭据的专用 OS 用户和可丢弃仓库中固定 `v0.0.45`，把默认权限改为 `Supervised`，只启用一个 provider；逐项测试文件越界、shell、Git push、审批失效、客户端撤销与断线恢复。确需远程访问时优先私有网络，记录已配对设备并定期撤销闲置 session；上线前再审阅 T3 Connect 数据流、更新签名与 provider 独立条款。

## 参考资料

- [GitHub 仓库](https://github.com/pingdotgg/t3code)
- [GitHub REST API](https://api.github.com/repos/pingdotgg/t3code)
- [README 与安装说明](https://github.com/pingdotgg/t3code/blob/main/README.md)
- [权限模式](https://github.com/pingdotgg/t3code/blob/main/docs/user/permission-modes.md)
- [架构与所有权边界](https://github.com/pingdotgg/t3code/blob/main/docs/internals/overview.md)
- [远程访问](https://github.com/pingdotgg/t3code/blob/main/docs/user/remote-access.md)
- [隐私政策源码](https://github.com/pingdotgg/t3code/blob/main/apps/marketing/src/pages/privacy-policy.astro)
- [v0.0.45 Release](https://github.com/pingdotgg/t3code/releases/tag/v0.0.45)
- [LICENSE](https://github.com/pingdotgg/t3code/blob/main/LICENSE)
