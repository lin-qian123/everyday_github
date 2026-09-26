<!-- markdownlint-disable MD013 -->

# Navop（feigeCode/navop）

> 上游仓库：<https://github.com/feigeCode/navop> · 归类：Coding Agents 与终端助手 · 本页基于 2026-09-27 的 GitHub API、README、Release、Public MCP 说明与两份许可证静态整理，未安装桌面程序、连接数据库 / SSH 或启用同步与 Agent。

- 抓取快照：1,671 stars、165 forks、55 open issues。
- 热度信号：GitHub Rust Trending 抓取时约 +65 当日 stars。
- 版本与许可：latest Release / tag 为 `v0.19.2`；API 返回 `NOASSERTION`，根 Apache-2.0 之外还叠加限制商业分发、付费平台和竞争产品的 `NAVOP_LICENSE`。

## 定位

Navop 是用 Rust 与 GPUI 构建的原生运维 / 开发工作台，把数据库、Redis / MongoDB、SSH / SFTP / FTP、terminal、RDP / VNC、监控、Markdown、Git 和 AI Agent Hub 放进一个桌面应用。它还可通过 Public MCP / CLI 把选定的宿主工具暴露给 Codex、Claude 等外部 Agent。

## 用法

普通用户可从 GitHub Releases 下载 macOS、Windows 或 Linux artifact，并用 `sha256sums.txt` 核对；开发者可按平台准备依赖后运行 `cargo run -p main`。若需要 Agent 接入，可在 Settings 中启用 loopback MCP server，选择 Safe / Confirm / Auto profile 与 tool groups，再安装 `@navop/cli` 或 stdio bridge。首次试用应只接测试数据库和可丢弃 SSH host。

## 原理

GPUI / Rust 提供无 WebView 的原生界面，各类 database、remote access、terminal 和 extension tool 由 host 统一调度。Public MCP 监听动态 loopback port，以 user-only discovery token 认证客户端；Navop 本体保留 live schema、permission、approval 与 audit 的最终权威。Agent Hub 将终端 Agent、项目文件、Git branch、change 和 diff 投影到同一 workspace。

## 价值

它把日常数据库管理、远程主机、文件传输、terminal 与 coding agent 合并，减少多个客户端之间的上下文切换。Safe / Confirm / Auto、工具分组、audit 与 loopback token 为 Agent 接入提供了可见控制点；跨平台原生 artifact 和 checksum 也比只发布未固定脚本更易做供应链核验。

## 风险边界

- 一个应用集中数据库凭据、SSH key、remote file、terminal、RDP、monitoring 与 Agent，单点失陷或错误自动化的 blast radius 很大。
- AI 可生成 / 解释 SQL、调用 terminal 和 host tools；Safe / Confirm / Auto 是应用策略，不是 OS sandbox，也不能阻止被授权工具内部的危险语义。
- README 宣称 encrypted sync，但本轮未验证加密协议、key custody、tenant isolation、恢复与删除；敏感连接不应因“加密”表述直接上线同步。
- API 无 SPDX 是因为根 Apache-2.0 叠加自定义附加条款；后者禁止付费分发、商业产品捆绑和竞争产品，不能按纯 Apache-2.0 处理。
- 上游支持大量数据库、协议和 extension，版本 / driver / host-key / legacy algorithm 组合很复杂；兼容列表不是数据完整性或安全保证。

## 补充建议

先用专用 OS 用户、测试数据库与短期 SSH key，固定 `v0.19.2` 并核验 checksum。Public MCP 从 Safe + 最小 tool group 开始，记录每个审批与 audit event；对 SQL rollback、host-key change、SFTP overwrite、port forward、extension 安装、sync 断网和 Agent prompt injection 做故障测试。商用或再分发前单独做 `NAVOP_LICENSE` 法务审查。

## 参考资料

- [GitHub 仓库](https://github.com/feigeCode/navop)
- [GitHub REST API](https://api.github.com/repos/feigeCode/navop)
- [v0.19.2 Release](https://github.com/feigeCode/navop/releases/tag/v0.19.2)
- [Public MCP 文档](https://docs.navop.dev/en-US/guide/public-mcp)
- [Apache-2.0 文件](https://github.com/feigeCode/navop/blob/main/LICENSE-APACHE)
- [Navop 附加许可证](https://github.com/feigeCode/navop/blob/main/NAVOP_LICENSE)
- [CHANGELOG](https://github.com/feigeCode/navop/blob/main/CHANGELOG.md)
