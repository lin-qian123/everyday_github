<!-- markdownlint-disable MD013 -->

# Hermes-Relay（Codename-11/hermes-relay）

> 上游仓库：<https://github.com/Codename-11/hermes-relay> · 归类：前端、UI 与 Agent 交互层 · 本页基于 2026-09-29 的 GitHub API、README、remote-access / desktop-tools / security 文档、Release、Security Policy 与 LICENSE 静态整理，未安装 APK、pair 设备、开放远程入口或授予 Accessibility / desktop tools。

- 抓取快照：281 stars、56 forks、44 open issues。
- 热度信号：GitHub Kotlin Trending 抓取时约 +14 当日 stars。
- 版本与许可：MIT；latest GitHub Release 为 `android-v1.18.0`，同批 server track 为 `server-v1.12.0`，Android manifest 与 Python package 分别为 `1.18.0` / `1.12.0`。

## 定位

Hermes-Relay 是 NousResearch Hermes Agent 的 Android companion 与跨平台 desktop CLI / relay：Agent brain 留在用户主机，手机提供 chat、voice、管理和可选 device control，paired CLI 则可向 Agent 暴露文件、终端、搜索、截图、剪贴板与编辑器等本机能力。它不是 Hermes Agent 本体，也不把远程接入自动变成安全 sandbox。

## 用法

基础 Android 路径连接正在运行的 Hermes Dashboard / Gateway，可经可信 LAN、Tailscale 或单独配置的 HTTPS route 使用。要启用 Terminal、notifications、Relay sessions、desktop tools 或 Device Control，需要安装并启用 Hermes-Relay plugin、启动 relay，再通过一次性 QR / invite pairing。Google Play build 不含 sideload 的屏幕读取 / 操作能力；desktop CLI 仍为 beta，工具授权与 remote exposure 需独立配置。

## 原理

标准 chat / manage / voice 走 Hermes Dashboard / Gateway；可选 Direct API 使用 API key；独立 WSS relay 承载 terminal、media enhancements、sessions 与 machine tools。Android 使用 Keystore、TOFU certificate pinning、time-bound grants 与 session TTL；desktop tools 通过 consent gate、patch diff approval、per-host access preset、activity log 和 emergency stop 约束，但最终仍在配对机器上以用户权限执行。

## 价值

它把自托管 Agent 的移动 chat / voice、运行状态与远端机器操作统一到同一配对模型，并明确区分 Play、sideload、Dashboard、API 与 Relay 的能力面。对需要离开桌面监督长任务的用户，这比直接暴露终端端口更容易观察和撤销；开源 threat model 与 release-track 文档也便于逐层评估。

## 风险边界

- sideload Device Control 可读屏、点击、输入、截图、读写剪贴板、SMS、联系人与位置；desktop CLI 又可运行终端和写文件，属于真实设备高权限远控。
- destructive-verb confirmation、app blocklist、diff approval 与 emergency stop 都是应用层 guardrail，不是 OS sandbox，也可能被编码、间接动作或上游 Agent 绕开。
- LAN / Tailscale / TLS 解决部分传输可达性，不能替代 Hermes Dashboard、API key、relay session、provider key 和 host tool 的独立认证授权。
- upstream Hermes、Dashboard 配置与第三方 CUA runtime 不在本项目完整安全保证范围内；组合后的权限以最宽能力为准。
- CLI beta binaries 在上游说明中仍可能触发 SmartScreen / Gatekeeper；Android、server、plugin、desktop 多 release tracks 必须分别固定。

## 补充建议

从无 tools 的 chat-only 路径开始，在专用测试手机、低权限 OS 用户和无 secret workspace 逐项授权。远程访问优先可信 VPN，不公开 raw Dashboard / relay；分别轮换 Dashboard session、API key 与 relay pairing，设置短 TTL。默认禁用 notification、clipboard、SMS、location、Accessibility 与 terminal，所有 write / shell / device action 保留本机人工确认、可回读结果和紧急断开演练。

## 参考资料

- [GitHub 仓库](https://github.com/Codename-11/hermes-relay)
- [GitHub REST API](https://api.github.com/repos/Codename-11/hermes-relay)
- [android-v1.18.0 Release](https://github.com/Codename-11/hermes-relay/releases/tag/android-v1.18.0)
- [server-v1.12.0 Release](https://github.com/Codename-11/hermes-relay/releases/tag/server-v1.12.0)
- [Remote access guide](https://github.com/Codename-11/hermes-relay/blob/main/user-docs/guide/remote-access.md)
- [Desktop tools guide](https://hermes-relay.dev/docs/desktop/tools.html)
- [Security architecture](https://github.com/Codename-11/hermes-relay/blob/main/docs/security.md)
- [Security Policy](https://github.com/Codename-11/hermes-relay/blob/main/SECURITY.md)
- [LICENSE](https://github.com/Codename-11/hermes-relay/blob/main/LICENSE)
