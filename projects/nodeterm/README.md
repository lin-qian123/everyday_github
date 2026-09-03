<!-- markdownlint-disable MD013 MD034 -->

# Nodeterm：把终端与 Coding-Agent 会话铺到无限画布的桌面工作台

## 项目概览

- 上游仓库：https://github.com/eneskirca/nodeterm
- GitHub API 快照（2026-09-04）：1,682 stars、173 forks、50 个开放 issue
- 当前 release：`v0.3.4`
- 主要技术：Electron / React、tmux、xterm、React Flow、Monaco、SSH、WebSocket、移动端配对
- 许可证：GitHub API 为 `NOASSERTION`；仓库 LICENSE / README 为 BUSL-1.1，各 release 四年后转 MIT

## 定位

Nodeterm 用无限画布承载真实终端、Claude Code / Codex / Gemini / Copilot / OpenCode 等 agent、笔记、编辑器、diff 和网页节点，并把 live sessions 同步映射到 Kanban 视图。

它是 session 与工作区控制面，不是容器或 OS sandbox。当前许可证是 source-available 的 BUSL-1.1，不能直接按 MIT/Apache 类开源项目处理。

## 用法

普通用户可下载 macOS、Linux 和 Windows 版本；macOS 也提供 tap：

```bash
brew tap nodeterm/tap
brew trust nodeterm/tap
brew install --cask nodeterm
```

源码开发要求 Node.js 20+，session 持久化依赖 tmux；Server Edition 可在浏览器访问远端主机。首次试用应放在无敏感仓库，先关闭 GitHub issue 双向同步、手机 relay、auto-update 和自动 Git 操作。

## 原理

Electron main、preload、renderer 三层通过受限 bridge 通信，`src/core` 的服务由 `CorePlatform` 抽象复用到桌面和 Server Edition。PTY 由 tmux 保持，React Flow 保存画布状态；SSH transport、WebSocket-RPC 和移动端 relay 把同一 live session 暴露到其他表面。

Agent 状态主要通过 hooks 而不是输出文本抓取；Git、worktree、issue、commit、push 与 discard 都通过系统工具或上游服务执行。这些能力提升可见性，也意味着应用继承真实用户权限。

## 价值

- 空间布局和持久 tmux session 适合同时监督多路 agent 与终端。
- 画布、Kanban、编辑器、diff 和 agent 状态集中，减少在窗口间丢失上下文。
- desktop / browser / mobile 三个表面为远程监督提供一致入口。
- hook 状态、context meter 和通知可减少依赖肉眼轮询输出。

## 风险边界

- tmux、worktree 和画布不提供 OS 隔离；agent 仍可继承当前用户的文件、网络、凭据与命令权限。
- 应用可 stage/discard/commit/push、同步 issue、改 agent hooks 并远程输入终端，后果性动作必须最小授权。
- 手机 relay 的“E2E encrypted”、本地 Whisper 和状态恢复都是上游声明，本轮未做协议或流量审计。
- Server Edition、SSH、WebSocket、通知与 auto-update 扩大攻击面；远程暴露前需核验认证、TLS、日志和撤销。
- Windows installer 当前 README 明示未签名、session 恢复仍在完善；跨平台不能按 macOS 行为外推。
- BUSL-1.1 限制竞争性产品/服务，release 四年后才转 MIT；商用和再分发须读实际 LICENSE。
- 本页只做静态资料核验，未安装、配对手机或执行 Git 写操作。

## 补充建议

1. 先在可丢弃仓库运行单 agent，记录 hooks、配置、tmux、`.nodeterm/`、日志和系统服务的全部写入。
2. 对 stage/discard/commit/push、issue 同步、远程输入与权限提示分别设置人工 gate。
3. 用测试账号和隔离网络验证 Server Edition、手机配对、relay、撤销、会话超时与丢设备流程。
4. 通过源码/流量审计复核 E2E、语音本地化、更新源和敏感 transcript 的保留期。
5. 商用前让法务按具体 release 日期、Additional Use Grant 与部署方式审查 BUSL 条款。

## 参考资料

- 仓库与 README：https://github.com/eneskirca/nodeterm
- Releases：https://github.com/eneskirca/nodeterm/releases
- 官方站点：https://nodeterm.dev/
- 文档：https://nodeterm.dev/docs
- Server Edition：https://github.com/eneskirca/nodeterm/blob/main/docs/SERVER.md
- 许可证：https://github.com/eneskirca/nodeterm/blob/main/LICENSE
