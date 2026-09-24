<!-- markdownlint-disable MD013 -->

# Zeron（zeronsh/zeron）

- GitHub：<https://github.com/zeronsh/zeron>
- 抓取快照：2026-09-25，2,210 stars、212 forks、135 open issues
- 热度信号：GitHub Rust Trending 抓取时约 +129 当日 stars
- 版本与许可：MIT；latest GitHub Release / tag 为 `v0.2.88`

## 定位

Zeron 是 Claude Code、Codex、Cursor、Devin、Grok、Hermes、Pi、Antigravity 等 coding agents 的原生控制面。新安装默认 local-only、无需账户；可选登录后在多设备之间查看、启动和控制远端 workspace 中的 Agent。

## 用法

Linux 可运行官方安装脚本并用 `zeron status`、`zeron update` 与 daemon 子命令管理；macOS 使用桌面构建或从源码安装 launchd 服务，Windows 提供 portable release。local-only 使用本机 profile；需要同步时必须先停 daemon、登录、再启动，退出同步也采用同样的 profile 切换边界。

## 原理

每台设备运行本地 engine 保存 sessions，并通过桌面 / CLI 控制真实 Agent process、branch diff 与 workspace。可选 sync 将同一账户下设备视为互信节点，使一个设备能够读取和写入另一设备的 workspace；本地 session 不会因登录而自动迁移到同步 profile。

## 价值

它把多个 coding-agent harness 的会话、运行状态和代码差异统一到一个本地优先界面，降低在不同终端和设备之间切换的认知成本。明确区分 local-only 与 synced profile，也比默认上传所有历史更容易建立分层采用策略。

## 风险边界

- 登录同步后，同账户设备可列出、读取和写入远端 workspace；启用 `Show ignored files` 还会暴露 `.env` 等 gitignored 文件，必须把每台设备视为完整 workspace trust peer。
- “本地 session 不自动上传”不代表后续远程控制零数据交换；同步协议、edge 服务、身份撤销、传输 / 静态加密与审计仍需单独核验。
- Zeron 只是控制面，不收窄底层 Agent 的 shell、文件、网络、MCP 和凭据权限；daemon 常驻还扩大了本地攻击面。
- 官方一行安装脚本会启动并注册 daemon，生产环境应先下载、校验、固定版本并审查 service / update 行为。
- MIT 覆盖仓库代码，不自动覆盖可选同步服务条款、第三方 Agent、模型 provider 或 workspace 内依赖。

## 补充建议

先在可丢弃仓库和 local-only profile 验证 session、diff、stop / resume 与升级回滚；不要启用 `Show ignored files`。若需要多设备同步，使用独立测试账户、最少设备和无 secret workspace，测试设备撤销、网络中断、并发写入与 profile 切换，再决定真实仓库的允许范围。

## 参考资料

- [GitHub 仓库](https://github.com/zeronsh/zeron)
- [GitHub REST API](https://api.github.com/repos/zeronsh/zeron)
- [v0.2.88 Release](https://github.com/zeronsh/zeron/releases/tag/v0.2.88)
- [架构说明](https://github.com/zeronsh/zeron/blob/main/ARCHITECTURE.md)
- [Linux browser runtime](https://github.com/zeronsh/zeron/blob/main/docs/reference/linux-browser.md)
- [第三方声明](https://github.com/zeronsh/zeron/blob/main/THIRD_PARTY_NOTICES.md)
- [LICENSE](https://github.com/zeronsh/zeron/blob/main/LICENSE)
