<!-- markdownlint-disable MD013 -->

# uniTerm（ys-ll/uniterm）

> 上游仓库：<https://github.com/ys-ll/uniterm> · 归类：Coding Agents 与终端助手 · 本页基于 2026-10-05 的 GitHub API、README、CHANGELOG、MCP / credential / sync 源码、Release、manifest 与 LICENSE 静态整理，未安装未签名二进制、导入凭据、连接 SSH / 数据库 / 集群或允许 Agent 执行命令。

- 抓取快照：672 stars、95 forks、46 open issues。
- 热度信号：GitHub Go Trending 抓取时约 +11 当日 stars。
- 版本与许可：Apache-2.0；latest Release 为 `v1.10.0`，但 Wails build manifest 仍写 `0.1.0`，采用时须以实际制品和 runtime version 为准。

## 定位

uniTerm 是跨 Windows、macOS、Linux 与 Android 的多协议终端和运维工作台，把 SSH、文件传输、RDP / VNC、数据库、Kubernetes、容器与 server monitor 放进统一 Wails 应用。内置自主 AI Agent 可多轮规划并直接执行 shell，另有 MCP server 让外部 Agent 复用已保存连接。

## 用法

可从 GitHub / Gitee Release、Scoop、Homebrew 或 deb / rpm 安装，也可用 Go 1.26、Node 20 与 Wails 3 beta 从源码构建。用户先创建 SSH / database 等连接，再配置 OpenAI 或 Anthropic compatible provider；AI sidebar 可选择 bypass、只确认危险命令、危险 + 写入或全部确认，MCP server 可按保存连接执行命令和传输文件。

## 原理

Go backend 负责协议、PTY、数据库 / Kubernetes / 容器会话、credential store、Git / WebDAV sync 和 update；Vue / TypeScript 前端维护多标签与 workspace，Agent loop 通过兼容 API生成命令并读取终端结果。MCP 把连接级执行能力暴露给外部客户端，声称凭据留在应用内，但命令和文件副作用仍发生在真实目标。

## 价值

它把大量常见运维协议、可视化管理和 AI / MCP 自动化集中到一个跨平台客户端，降低在多个终端、数据库 GUI 和容器工具之间切换的成本。多种确认模式、split pane、workspace、云同步和 source build 也便于建立可审阅的个人运维工作流。

## 风险边界

- Agent 与 MCP 连接的是真实 shell、文件系统、数据库、容器和 Kubernetes；`bypass` 或宽松确认会把一次提示扩大为多轮生产写入，GUI 不是 sandbox。
- 应用集中保存 SSH key、password、API key、database 与 cloud-sync 凭据；“凭据不离开 app”不等于命令输出、schema、文件内容或 prompt 不会发往模型 provider。
- Git / WebDAV sync 的范围、历史压缩和冲突行为可能复制敏感连接元数据；必须确认哪些字段被同步、如何加密、如何撤销。
- Release 文档建议对未签名 Windows 可执行文件加杀软排除，这不是安全证明；应优先固定来源、校验 artifact，必要时从源码构建。
- `go.mod` 对 mosh、S3 与 `x/crypto` 使用维护者 fork / replace，且依赖 Wails beta；供应链、补丁来源和升级兼容需额外审计。
- 本轮未验证 keyring / encryption、MCP auth、provider data flow、危险命令识别、sync 泄露或 30+ 协议兼容性。

## 补充建议

先在专用 OS 用户、测试 SSH 主机和只读 database 中固定 `v1.10.0`，确认所有 Agent / MCP 模式均为“全部确认”，禁用不需要的协议与 sync；逐条记录发给 provider 的内容、命令目标和审批回执。生产连接拆分低权限账号，MCP 只绑定 loopback，发布制品核验 hash / 签名并审阅三项 forked dependency。

## 参考资料

- [GitHub 仓库](https://github.com/ys-ll/uniterm)
- [GitHub REST API](https://api.github.com/repos/ys-ll/uniterm)
- [README、协议与 AI 模式](https://github.com/ys-ll/uniterm/blob/main/README.md)
- [v1.10.0 CHANGELOG](https://github.com/ys-ll/uniterm/blob/main/CHANGELOG.md)
- [MCP backend](https://github.com/ys-ll/uniterm/blob/main/app_mcp.go)
- [Go dependencies 与 replace](https://github.com/ys-ll/uniterm/blob/main/go.mod)
- [Wails build manifest](https://github.com/ys-ll/uniterm/blob/main/build/config.yml)
- [v1.10.0 Release](https://github.com/ys-ll/uniterm/releases/tag/v1.10.0)
- [LICENSE](https://github.com/ys-ll/uniterm/blob/main/LICENSE)
