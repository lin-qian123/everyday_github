<!-- markdownlint-disable MD013 -->

# Syrtis（Nanako0129/syrtis）

> 上游仓库：<https://github.com/Nanako0129/syrtis> · 归类：Coding Agents 与终端助手 · 本页基于 2026-09-29 的 GitHub API、README、architecture / verification / release knowledge base、Release 与 LICENSE 静态整理，未安装应用、读取真实 session log 或登录 provider 账号。

- 抓取快照：381 stars、37 forks、7 open issues。
- 热度信号：GitHub Swift Trending 抓取时约 +2 当日 stars。
- 版本与许可：MIT；latest Release 与 tag 均为 `v2.2.0`。

## 定位

Syrtis 是原 TokenBar 的原生 Swift 重写版：在 macOS 菜单栏读取 25+ AI coding tools 已写入磁盘的 session logs，汇总 tokens、费用、quota pace、模型与 Agent 使用情况。核心解析 / 聚合由 Rust `tokscale-core` 提供，SwiftUI 负责菜单栏、图表与 Sparkle 更新；另有共享核心的 Windows sibling。

## 用法

Apple Silicon、macOS 14+ 可通过维护者 Homebrew cask 或 GitHub DMG 安装；应用提供 Overview、Quota、Models、Monthly、Daily、Hourly、Stats 与 Agents 等视图。历史 token / cost 主要来自本地 log，live quota card 则可能需要 provider OAuth / subscription account 与 provider API。发布包由 Developer ID 签名并 notarize，Sparkle 负责更新。

## 原理

`tokscale-core` 负责多工具 session parser、dedup、pricing 与聚合，app-owned FFI 层补充 quota fetch 后把数据交给 Swift。项目公开 knowledge base 记录 Rust / Swift 边界、fixture、verification gate 与 release chain；它宣称无 Syrtis account、无 cloud sync、无 telemetry，但 quota 查询本身仍可能访问 provider 网络。

## 价值

对同时使用 Claude Code、Codex、Cursor、OpenCode、Gemini CLI 等工具的人，统一观察 token、费用与订阅窗口可帮助发现异常成本、失控 sub-agent 和 quota 峰值。公开 parser fixture 与 shared-engine 来源也使口径错误比黑盒菜单栏工具更容易定位。

## 风险边界

- session log 可能含 prompt、路径、仓库名、模型、时间与计费元数据；“本地读取”不代表这些文件天然适合被另一应用聚合。
- provider quota 需要真实 OAuth / subscription state 与网络请求；README 的“no cloud sync”不能解释所有 provider-side access。
- 费用取决于 pricing table、cache token、provider 计费规则和 parser 兼容性；仪表盘数字不是账单权威来源。
- 25+ tools 的日志格式持续变化，parser 可能漏记、重复或错误归因；rename 与旧 TokenBar migration 也需验证历史连续性。
- Sparkle、Homebrew、签名与 notarization降低安装风险但不提供可复现构建；上游 knowledge base明确仍有 toolchain / dependency 被签名的 residual risk。

## 补充建议

先对照少量人工可数的 fixture、provider dashboard 与本地 logs 验证 tokens、cache 和费用，再扩大历史导入。限制应用读取范围，不在共享账号 / 受监管终端中默认聚合敏感 session；对 quota OAuth 单独审查 scope、存储和撤销。固定 release checksum，保留原始日志但设置最短 retention，并把数字用作趋势告警而不是财务结算。

## 参考资料

- [GitHub 仓库](https://github.com/Nanako0129/syrtis)
- [GitHub REST API](https://api.github.com/repos/Nanako0129/syrtis)
- [v2.2.0 Release](https://github.com/Nanako0129/syrtis/releases/tag/v2.2.0)
- [Architecture knowledge](https://github.com/Nanako0129/syrtis/blob/main/docs/knowledge/architecture.md)
- [Verification knowledge](https://github.com/Nanako0129/syrtis/blob/main/docs/knowledge/verification.md)
- [Release and delivery](https://github.com/Nanako0129/syrtis/blob/main/docs/knowledge/release.md)
- [tokscale-core](https://github.com/Nanako0129/tokscale-core)
- [LICENSE](https://github.com/Nanako0129/syrtis/blob/main/LICENSE)
