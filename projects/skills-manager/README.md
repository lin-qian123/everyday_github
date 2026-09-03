<!-- markdownlint-disable MD013 MD034 -->

# Skills Manager：带 Git 备份与 Agent CLI 的多宿主技能控制面

## 项目概览

- 上游仓库：https://github.com/xingkongliang/skills-manager
- GitHub API 快照（2026-09-04）：4,399 stars、373 forks、191 个开放 issue
- 当前 release：`v1.36.1`
- 主要技术：Tauri 2 / Rust、React 19、SQLite、中央 skill library、Git backup/sync、agent-friendly CLI
- 许可证：MIT

## 定位

Skills Manager 管理 Claude Code、Codex、Cursor、Copilot、Gemini CLI 等 53 个上游列出的 agent/tool 的全局与项目 skills。它除了中央库、preset 和批量部署，还提供 Git 备份、多设备同步、快照恢复与可由 agent 调用的 CLI。

它是高权限配置与供应链控制面，不是 skill sandbox；“统一管理”也不自动等于来源可信或跨宿主行为一致。

## 用法

macOS 可用 Homebrew 安装，Windows/Linux 可下载 release installer：

```bash
brew install --cask skills-manager
```

在 Library 导入 Git、本地目录、archive 或 marketplace skill，再在 Global / Project Workspace 选择目标 agent。可选 GitHub device flow 创建私有备份仓库，多设备在后台提交、拉取、合并和推送。

## 原理

Tauri/Rust core 维护 SQLite 元数据、中央 skill 文件与每个 agent 的真实部署状态；桌面端和 CLI 共享数据库、repository lock 与 sync engine。symlink/copy 把 skill 部署到宿主目录，preset 是一次性批量应用而不是持续绑定。

Git sync 以 skill 为单位处理 rename/edit 冲突，保留本地版本并要求用户选择；API token 存入 OS keychain，skill 内容、tags、preset 和开关进入备份，secrets 与机级 wiring 按上游设计不入库。

## 价值

- 统一 library、workspace、preset、来源检查和实际部署状态。
- Git 快照与多设备同步为 skill 变更提供可恢复历史。
- CLI 可输出 JSON、支持 dry-run 和冲突结构，便于 agent 自动化前先检查。
- 自 v1.29.0 起上游声明 macOS release 已签名和 notarized，降低手工绕过 Gatekeeper 的需要。

## 风险边界

- 应用和 CLI 可写多个 agent 的全局/项目配置；误部署或恶意 skill 会跨工具扩散。
- GitHub device flow、私有仓库创建、后台 commit/push 和远端删除都是外部副作用，须明确 scopes、组织政策与人工确认。
- “secrets 不入备份”是上游设计声明；日志、导出包、skill 文本和意外嵌入的密钥仍需实测扫描。
- 53 个工具支持来自路径适配，不能证明每个宿主版本都正确加载或等价解释同一 skill。
- 自动更新、in-app updater、marketplace 和 Git 上游共同构成供应链；签名只能确认发布者，不能证明内容安全。
- 本页只核验 README、release 与 API，没有授权 GitHub、创建远端仓库或测试跨设备冲突。

## 补充建议

1. 先用专用测试账号、空白私有仓库和两个可丢弃 profile 验证 backup、merge、restore、disconnect 与 remote delete。
2. 保持 agent-driven 管理默认 dry-run；部署、删除、Git push 和远端操作保留独立人工 gate。
3. 对入库 skill 保存来源 commit、hash、审查结论和允许的 tools，不只保存显示名称。
4. 扫描 skill、日志和导出包中的 token/路径/提示词，并验证 OS keychain 撤销与换机流程。
5. 升级前固定 release、核验签名和 changelog，在一个宿主验证后再批量推广。

## 参考资料

- 仓库与 README：https://github.com/xingkongliang/skills-manager
- Releases：https://github.com/xingkongliang/skills-manager/releases
- 官方站点：https://skillsmanager.dev/
- 中文说明：https://github.com/xingkongliang/skills-manager/blob/main/README.zh-CN.md
- X 作者账号：https://x.com/JayTL00
- YouTube 介绍：https://www.youtube.com/watch?v=wfbCrfNASVU
