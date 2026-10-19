<!-- markdownlint-disable MD013 -->

# Codync

> 更新：2026-10-20（Asia/Shanghai）。分类：记忆层与个人 AI 基础设施。上游 `leepokai/Codync`；快照 `97c3b57c6175`（main）。本文基于官方榜单、认证 API 与上游文件静态研究；热度、版本时间与跨平台证据见[当日日报](../../daily/2026-10-20/ai-hotspots.md)。

## 定位

把电脑上的 Claude Code、Codex、Cursor 等 coding agents 包装为可持续聊天的 bot，从 iPhone、桌面或终端分配任务。Rust host 负责 Agent Client Protocol（ACP）、会话 / transcript、设备接入；原生 iPhone 与 Electron 桌面提供客户端。README 的约 40 种 Agent 支持是 registry / 适配声明，不是本轮逐项兼容测试。[README.md](https://github.com/leepokai/Codync/blob/97c3b57c61759cc1fc068939bfe5a12697e57db4/README.md)

## 用法

按 Release 下载匹配系统的包；macOS 也提供 `brew install --cask leepokai/codync/codync`。先安装并登录实际编码 CLI，再打开 Codync 设置 host、项目目录、bot 与审批策略，使用本机确认 / 配对码添加 iPhone。无图形服务器可用 host-only 安装路径及 `codync-host tui`。[README.md](https://github.com/leepokai/Codync/blob/97c3b57c61759cc1fc068939bfe5a12697e57db4/README.md)

本地数据在 `~/.codync`；失窃设备应通过 devices 撤销远程授权，不能只轮换 loopback bearer token。升级 / 重装要保留身份与会话目录，先读恢复说明。本轮没有安装、配对、授权屏幕或启动 CLI。[README.md](https://github.com/leepokai/Codync/blob/97c3b57c61759cc1fc068939bfe5a12697e57db4/README.md)

## 原理

host 与 Agent 用 ACP 通信，SQLite 保存 transcript，全局 revision 用于重连增量同步。远程经直接链路或 Cloudflare relay；文档声明手机与 host 端到端加密，push 内容也密封给设备。组聊 / bot 间请求各有会话，但共享电脑及其账户权限。[README.md](https://github.com/leepokai/Codync/blob/97c3b57c61759cc1fc068939bfe5a12697e57db4/README.md)[docs/reference/remote-relay.md](https://github.com/leepokai/Codync/blob/97c3b57c61759cc1fc068939bfe5a12697e57db4/docs/reference/remote-relay.md)

## 价值

适合把多 Agent 长任务、待审批动作与完成通知集中到手机，减少寻找终端会话的操作负担；也可作为研究远程撤权、状态续接和多 backend 适配的实例。是否提升任务质量仍取决于底层 Agent、代码权限与最终验收。

## 风险边界

- 安全文档明确：已配对设备按主机拥有者信任，可改 bot 启动命令、权限模式、目录并控制屏幕；编码 Agent 默认可执行 shell 而不询问。配对本身就是高权限授予，审批卡不意味着每个 backend 的每个动作都需人工。[SECURITY.md](https://github.com/leepokai/Codync/blob/97c3b57c61759cc1fc068939bfe5a12697e57db4/SECURITY.md)
- relay 加密只说明相关传输链路；Agent 本身会按其配置调用模型 / MCP，语音、屏幕、push 与账户发现也需分别确认。不要把本地保存 transcript 或官网隐私概括外推为模型流量全离线。[README.md](https://github.com/leepokai/Codync/blob/97c3b57c61759cc1fc068939bfe5a12697e57db4/README.md)[docs/reference/remote-relay.md](https://github.com/leepokai/Codync/blob/97c3b57c61759cc1fc068939bfe5a12697e57db4/docs/reference/remote-relay.md)
- 首次使用可能通过 npx / uvx 或下载二进制获取适配器；自动更新、PATH 发现、Claude statusline 包装也会改动本机状态。README 称 macOS 签名 / notarized，Windows 安装器尚未签名；本轮未核二进制签名。[README.md](https://github.com/leepokai/Codync/blob/97c3b57c61759cc1fc068939bfe5a12697e57db4/README.md)
- 仅最新发行获安全修复；iOS 审核可能造成版本滞后。采样 latest 为 `v2.20.0`，代码 Apache-2.0；“免费”不包含底层模型 / 订阅成本。[SECURITY.md](https://github.com/leepokai/Codync/blob/97c3b57c61759cc1fc068939bfe5a12697e57db4/SECURITY.md)[LICENSE](https://github.com/leepokai/Codync/blob/97c3b57c61759cc1fc068939bfe5a12697e57db4/LICENSE)

## 补充建议

先在独立系统账户与测试仓库接一个 bot，测本机 / 远程断线、设备撤权、host 重启、重复请求与审批拒绝；确认旧设备和过期码都失效。保留 CLI / adapter / host / iOS 四者版本，并把执行成功与最终代码通过测试分开记录。

## 参考资料

- [README.md](https://github.com/leepokai/Codync/blob/97c3b57c61759cc1fc068939bfe5a12697e57db4/README.md)
- [LICENSE](https://github.com/leepokai/Codync/blob/97c3b57c61759cc1fc068939bfe5a12697e57db4/LICENSE)
- [SECURITY.md](https://github.com/leepokai/Codync/blob/97c3b57c61759cc1fc068939bfe5a12697e57db4/SECURITY.md)
- [docs/reference/remote-relay.md](https://github.com/leepokai/Codync/blob/97c3b57c61759cc1fc068939bfe5a12697e57db4/docs/reference/remote-relay.md)
- [web/app/components/privacy.tsx](https://github.com/leepokai/Codync/blob/97c3b57c61759cc1fc068939bfe5a12697e57db4/web/app/components/privacy.tsx)
- [仓库 API](https://api.github.com/repos/leepokai/Codync)
- [v2.20.0 Release](https://github.com/leepokai/Codync/releases/tag/v2.20.0)
