<!-- markdownlint-disable MD013 -->

# agent-desktop：以无障碍树观察和操作桌面的 CLI

- 上游：[vercel-labs/agent-desktop](https://github.com/vercel-labs/agent-desktop)；分类：Coding Agents 与终端助手。
- 更新：2026-11-03（Asia/Shanghai）；固定主线 SHA：`060c83af4be63096de33fc22d79fb9c4d02f528e`。
- 热度快照：综合 daily +2,243；API 9,469 stars / 642 forks / 122 open issues（含 PR）。最新发行 v1.0.2，UTC 2026-10-30。
- 证据：官方 Trending / API 与固定源码静态核读；下文用法供复核，不表示本轮已运行。

## 定位

agent-desktop 为 Agent 提供桌面观察与动作 CLI / C 库，主路径是操作系统无障碍树，配合截图、窗口和剪贴板能力。循环由宿主 Agent 负责：观察、按 ref 操作、再次观察。

本页从原 lahfir/agent-desktop 原位更新。旧 API 返回 Moved Permanently 并指向 repository ID 1161958643，新 vercel-labs API 返回同一 ID；v1.0.2 发行记录也明确提及组织迁移，因此没有另建目录。它仍与 Solo.io 的 agentdesktop 不同。

## 用法

```sh
npm install -g agent-desktop
agent-desktop version
agent-desktop skills get desktop
agent-desktop skills get platform
agent-desktop list-apps
agent-desktop snapshot --app Finder -i
```

示例 Finder 适用于 macOS。动作要使用本次快照实际返回的完整 ref，不能复制文档占位 ref；动作后重新 snapshot 回读。macOS 用 permissions --guide 按需授予权限；Windows 受进程 integrity level 限制，Linux 需要用户图形会话和 AT-SPI。官方 Homebrew / Scoop 默认目录包仍在提交，不能照旧假设已经可用。

## 原理

- 每次 CLI 调用独立进程；平台 adapter 将 macOS AX、Windows UIA、Linux AT-SPI 结果归一成 JSON envelope。
- Ref 包含 snapshot 身份。裸 @e8 被拒绝；STALE_REF / AMBIGUOUS_TARGET 要重新观察或指定 window-id。
- 默认 headless 阻止前台激活与合成输入，--headed 才开放物理输入；这是一类副作用约束。
- 当前 README 区分 60 个命令名与 56 个可运行命令；四个持续按住键 / 鼠标的命令要等能够释放输入的 daemon，当前拒绝运行。

## 价值

结构化元素身份、错误 disposition、局部 skeleton 和动作后回读可减少盲点与错误重试。原生 archive 可绕过 JS launcher 的逐次启动开销；实际收益仍需同一应用、任务和日志条件比较。

## 风险边界

- 无障碍、截图、剪贴板和通知可读写真实桌面数据；headless 不构成 OS sandbox 或业务审批。
- 现有 macOS / Windows / Linux 支持表已比旧页完整，但 Linux X11 / Wayland、GNOME 和系统 shell 能力不同，不能视为功能完全一致。
- 快照、trace、截图和 debug HTML 可含私密信息。可选 JEV helper 会将屏幕描述发给配置的模型 provider，不能把原生 CLI 与该 helper 的数据流混为一谈。
- 包括远端 model provider 在内的宿主 Agent 权限不会因 CLI 使用结构化 ref 自动降低。C ABI 还需核版本、内存所有权与线程约定。
- Apache-2.0。本轮没有安装工具、授予权限、操作桌面或测试跨平台行为。

## 补充建议

1. 先用专用测试用户和只读 snapshot 验证目标应用的树覆盖、权限与错误恢复。
2. 对发送、删除、支付、发布等动作保留宿主侧审批，并记录动作前后窗口与状态。
3. 为 trace / screenshot 设访问与保留期限；共享桌面上协调多 Agent，避免焦点和窗口竞争。

## 参考资料

- [README.md](https://github.com/vercel-labs/agent-desktop/blob/060c83af4be63096de33fc22d79fb9c4d02f528e/README.md)。
- [docs/install.md](https://github.com/vercel-labs/agent-desktop/blob/060c83af4be63096de33fc22d79fb9c4d02f528e/docs/install.md)。
- [docs/faq.md](https://github.com/vercel-labs/agent-desktop/blob/060c83af4be63096de33fc22d79fb9c4d02f528e/docs/faq.md)。
- [SECURITY.md](https://github.com/vercel-labs/agent-desktop/blob/060c83af4be63096de33fc22d79fb9c4d02f528e/SECURITY.md)。
- [Cargo.toml](https://github.com/vercel-labs/agent-desktop/blob/060c83af4be63096de33fc22d79fb9c4d02f528e/Cargo.toml)。
- [LICENSE](https://github.com/vercel-labs/agent-desktop/blob/060c83af4be63096de33fc22d79fb9c4d02f528e/LICENSE)。
- [仓库 API](https://api.github.com/repos/vercel-labs/agent-desktop)；[发行记录](https://github.com/vercel-labs/agent-desktop/releases/tag/v1.0.2)。
