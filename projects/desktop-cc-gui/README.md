<!-- markdownlint-disable MD013 -->

# Desktop CC GUI（zhukunpenglinyutong/desktop-cc-gui）

> 上游仓库：<https://github.com/zhukunpenglinyutong/desktop-cc-gui> · 归类：Coding Agents 与终端助手 · 本页基于 2026-09-26 的 GitHub API、README、Release、package 与公开文档静态整理，未下载安装包、登录 provider 或在真实代码仓库中运行。

- 抓取快照：4,383 stars、396 forks、310 open issues。
- 热度信号：GitHub TypeScript Trending 抓取时约 +16 当日 stars。
- 版本与许可：latest Release / tag 为 `v1.0.9`，根 package 为 `1.1.0`；README 声称 MIT，但 API 未识别 SPDX，根目录快照未见 LICENSE 文件。

## 定位

Desktop CC GUI 是基于 Tauri 2、React、TypeScript 与 Rust 的跨平台 coding-agent 桌面客户端，把 Claude Code、Codex、Kimi、Grok、Pi、OpenCode、DeepSeek Harness 等 CLI 的会话、流式事件、工具调用、权限提示和 Git 操作集中到图形界面。

## 用法

普通用户可从 GitHub Releases 下载 macOS、Windows 或 Linux 安装包，打开后选择已有 CLI 登录或配置 provider channel，再添加项目目录并创建会话。开发者需要 pnpm 10、Rust stable 与平台构建工具，执行 `pnpm install`、`pnpm tauri dev`；交付前至少运行 `pnpm build`、`pnpm test`，Rust 改动还需 `cargo test`。

## 原理

Rust backend 为不同 CLI 提供专用协议 adapter，解析原生流式事件、session history、permission mode 与 provider channel，而不是抓取终端屏幕。前端提供会话、diff、终端、Git、文件和 plugin 面板；状态持久化在本机，并复用各 CLI 自己的配置与凭据文件。不同引擎的权限、plan mode、图片、MCP 和 channel 能力并不对等。

## 价值

它降低了多 CLI 并用的可视化和切换成本，特别适合希望看到 thinking / tool call、保留 session、比较 provider，并在一个桌面界面处理 diff 与 Git 的用户。专用 adapter 比简单 PTY 文本抓取更容易建立一致 UI，也为 plugin manifest 与权限提示提供统一入口。

## 风险边界

- GUI 只转呈底层 CLI 权限，不构成额外 sandbox；部分引擎只支持 `bypass` 或 `auto`，误选模式会让文件、shell、Git 和网络动作直接继承用户权限。
- 应用会读取各 CLI 原生 session 与配置，并能写 provider channel；“本地持久化”不代表 prompt、源码、图片或工具结果不会发送给所选 provider。
- plugin 能扩展 UI 和执行能力，必须把 manifest、权限、更新来源和签名作为供应链边界审计。
- Release `v1.0.9` 与根 package `1.1.0` 存在发布平面时差；安装包、源码和文档能力应按精确 commit / artifact 对齐。
- README 写 MIT，但本轮根目录未见 LICENSE 且 API 返回无 SPDX；在复制、分发或商用前应等待上游补齐明确许可证文件。

## 补充建议

用无敏感凭据的专用 OS 用户试用，每个引擎只配置一个测试账号和副本仓库，记录 GUI 选择最终映射到的 CLI flags、配置 diff、允许目录和网络端点。建立同一任务在 Claude / Codex / OpenCode 的 permission-deny、cancel、resume 与 crash-recovery 矩阵，并在启用任何 plugin 前核验其代码、权限和更新机制。

## 参考资料

- [GitHub 仓库](https://github.com/zhukunpenglinyutong/desktop-cc-gui)
- [GitHub REST API](https://api.github.com/repos/zhukunpenglinyutong/desktop-cc-gui)
- [v1.0.9 Release](https://github.com/zhukunpenglinyutong/desktop-cc-gui/releases/tag/v1.0.9)
- [中文 README](https://github.com/zhukunpenglinyutong/desktop-cc-gui/blob/main/README.zh-CN.md)
- [Plugin 开发与信任边界](https://github.com/zhukunpenglinyutong/desktop-cc-gui/blob/main/docs/plugin-development-guide.zh-CN.md)
- [根 package](https://github.com/zhukunpenglinyutong/desktop-cc-gui/blob/main/package.json)
