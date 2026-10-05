<!-- markdownlint-disable MD013 -->

# Pi Pocket（TannerMidd/pi-pocket）

> 上游仓库：<https://github.com/TannerMidd/pi-pocket> · 归类：前端、UI 与 Agent 交互层 · 本页基于 2026-10-06 的 GitHub API、README、features / security 文档、Release、manifest 与 LICENSE 静态整理，未安装 Node 依赖、登录 provider、开放远程访问或让 Agent 执行工具。

- 抓取快照：105 stars、5 forks、0 open issues；仓库创建于 2026-10-04 02:29 UTC。
- 热度信号：GitHub Search 按新建仓库 stars 排序的早期开发者信号；不是 GitHub Trending 或社媒互动量。
- 版本与许可：MIT；GitHub Release / tag 与 manifest 均为 `v0.8.0` / `0.8.0`，依赖 Node.js 22.19+。

## 定位

Pi Pocket 是运行在用户设备上的 mobile-first Pi coding-agent Web 控制面。它把持久会话、多人协作、steer / queue、fork、schedule、done-when、模型选择、审批、diff、浏览器、artifact 与 background subagent 放进桌面和手机都能访问的界面。

## 用法

用户先在 Pi 中登录 provider，再 clone 仓库并执行 `npm install && npm start`。Launcher 可选择 loopback、LAN、Cloudflare quick tunnel 或 Tailscale，生成 owner sign-in link / QR；随后可创建会话、邀请 view-only / steer 用户、设置 spend limit，或在 Android Termux 直接运行。

## 原理

Pi Durable 把模型调用、工具调用、任务与会话状态写入 SQLite，服务器通过 SSE 把 committed projection 同步给各浏览器。服务端扩展实现 browser、artifact、subagent、schedule、goal、plan、Lancet Guard 与 codemode；内置 Chromium 页面运行在服务器上，每个会话使用独立 browser context。

## 价值

项目把长任务持久化、移动端审批和多人 side chat 结合起来，适合离开电脑后继续观察本地 Agent，而不必把整个工作区迁到云 VM。README 和 SECURITY 对 steer 权限、browser 网络可达性与 plan / worktree 非隔离边界写得较清楚。

## 风险边界

- 上游明确指出任何拥有 steer 权限的人都能通过 Pi 以服务器用户身份访问文件、设置、token 与代码；单会话 invite 只限制 UI 可见性，不限制 Agent 的 OS 权限。
- Owner link 就是服务器钥匙，Cloudflare quick tunnel 暴露公网入口；link、长期 cookie、push key、invite 和撤权流程都需要按高价值凭据治理。
- Lancet Guard 默认关闭；即使开启，内置 Browser 的网络 / localhost 访问也不经过 Guard，plan mode、worktree 和 spend limit 都不是安全边界。
- Drop-in extension 在服务端以 owner 权限运行；schedule、done-when 与 background subagent 会把权限和费用延伸到无人值守时段。
- built-in browser 可访问服务器所在网络，远程协作者可能触及内网管理面；关闭 Browser 仍不等于限制 Agent 的其他网络工具。
- 本轮未验证认证、token rotation、viewer 隔离、重启恢复、工具幂等、移动通知审批或 `v0.8.0` dependency supply chain。

## 补充建议

只在专用低权限 OS 用户和无生产凭据的测试工作区运行，首轮固定 loopback 或 Tailscale，不使用公开 quick tunnel；默认关闭 Browser、schedule、subagent 与自定义 extension，再按需求逐项开放。Steer 权限只给能直接登录该主机的人，并启用“Approvals need someone else”、短期邀请、日志审计和快速 token rotation 演练。

## 参考资料

- [GitHub 仓库](https://github.com/TannerMidd/pi-pocket)
- [GitHub REST API](https://api.github.com/repos/TannerMidd/pi-pocket)
- [README 与 remote access](https://github.com/TannerMidd/pi-pocket/blob/main/README.md)
- [完整功能说明](https://github.com/TannerMidd/pi-pocket/blob/main/docs/features.md)
- [Security boundary](https://github.com/TannerMidd/pi-pocket/blob/main/SECURITY.md)
- [工程结构](https://github.com/TannerMidd/pi-pocket/blob/main/docs/map.md)
- [`v0.8.0` Release](https://github.com/TannerMidd/pi-pocket/releases/tag/v0.8.0)
- [npm manifest](https://github.com/TannerMidd/pi-pocket/blob/main/package.json)
- [MIT LICENSE](https://github.com/TannerMidd/pi-pocket/blob/main/LICENSE)
