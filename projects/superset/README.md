<!-- markdownlint-disable MD013 MD034 -->

# Superset：用独立 Git worktrees 编排并审查多路 coding agents

## 项目概览

- 上游仓库：https://github.com/superset-sh/superset
- GitHub API 快照（2026-09-03）：13,668 stars、1,242 forks、609 个开放 issue
- 当前 release：`desktop-v1.25.1`
- 主要技术：Electron / React、Git worktrees、terminal、diff viewer、CLI / SDK / MCP、remote hosts
- 许可证：Elastic License 2.0（source-available）

## 定位

Superset 是面向 Claude Code、Codex 等 CLI agents 的桌面 IDE 和控制面。它为每个 agent 创建独立 Git worktree / branch，提供持久终端、状态提醒、diff 审查、浏览器预览、自动化和远端 host 管理。

上游口号是并行运行“100+ agents”，但这是产品能力描述，不是本轮在固定硬件、仓库和任务上的容量或效率实测。

## 用法

macOS 是主要目标，Linux AppImage 标为 experimental，Windows 尚未提供。也可单独安装 CLI：

```bash
brew install superset-sh/tap/superset
```

工作区可配置 setup、teardown 和 run scripts。真实仓库试用前应固定 release，限制每个 worktree 的环境变量和服务端口，并要求所有 agent 输出先进入 diff / test gate，不自动合并或推送。

## 原理

每个 workspace 绑定独立 worktree、branch、terminal 和环境；桌面端集中显示 agent 状态、diff 与本地服务。CLI、TypeScript SDK 与 MCP 可创建 workspace、启动 agent、读取终端和管理自动化；远端 host 让同一控制面访问其他机器。

Git worktree 能降低文件冲突，但所有进程仍可能共享同一 OS 用户、网络、keychain、全局配置与外部账号，因此不是 sandbox。

## 价值

- 将多 agent 并行、状态提醒、diff、终端和浏览器预览集中在一个界面。
- 用 worktree / branch 保持文件改动分离，便于比较候选实现。
- 支持多种现有 CLI agents，减少专有 agent runtime 锁定。
- CLI / SDK / MCP 与 remote hosts 适合把桌面工作流扩展到自动化和异地机器。

## 风险边界

- worktree 隔离的是 Git 工作目录，不隔离进程、网络、凭据、数据库或云资源。
- 并发 agent 会放大模型费用、I/O、构建负载、端口冲突和错误外部动作。
- setup / teardown scripts、MCP、remote access 与 scheduled automations 都是高权限入口，需要签名、审计和停止机制。
- ELv2 是 source-available 许可证，并限制把 Superset 本身作为托管服务转售；不能按 MIT/Apache 的方式假设再分发权利。
- “private by default”与“free forever”来自上游声明，仍需核对连接、telemetry、账号与可选服务的数据流。
- 本页未安装 Superset，也未实测 100+ agents、远端连接或故障恢复。

## 补充建议

1. 从 2 个 agents、2 个 worktrees 和一个可丢弃仓库开始，测量冲突、CPU/内存、token 与 review 返工。
2. 对 setup / teardown 和自动化脚本做代码审查，禁止默认读取用户级 secrets 或触碰生产数据库。
3. 将测试、lint、diff review 与人工合并作为统一 gate，不把“agent 已完成”直接当作可发布状态。
4. 远端 host 使用专用账户、最小 SSH 权限和网络 allowlist，并测试断线、重复执行与紧急停止。
5. 在团队或商业部署前单独审查 ELv2 与可选托管服务条款。

## 参考资料

- 仓库与 README：https://github.com/superset-sh/superset
- Releases：https://github.com/superset-sh/superset/releases
- 官方文档：https://docs.superset.sh/
- Workspaces：https://docs.superset.sh/workspaces
- Remote access：https://docs.superset.sh/remote-access
- Elastic License 2.0：https://github.com/superset-sh/superset/blob/main/LICENSE.md
- 官方 X 账号：https://x.com/superset_sh
