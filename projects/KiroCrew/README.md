<!-- markdownlint-disable MD013 -->

# KiroCrew

## 定位

Kiro Crew 是运行在自有主机上的持久开发工作区。Gateway 管会话、记忆、任务检查点、定时作业和审批，桌面、网页、CLI 及 Slack / Discord 等界面连接同一执行端。其 self-learning / self-evolving 指将纠正与经验沉淀为可编辑记忆 / 技能，不表示模型权重自动训练。

2026-10-31 采样：Python daily +19 stars；API 累计 4,669 stars / 914 forks / 2,932 open issues（含 PR）。核读 main `ec46e9bfaa4e`；发行 API 首项 [v0.11.0](https://github.com/kirodotdev/KiroCrew/releases/tag/v0.11.0)，2026-10-30 UTC。以下区分作者文档与有限源码核读，未做上游运行验收。

## 用法

从上游发行选择 Stable / Insider / Nightly；默认执行器 `kiro-cli` 需要另行安装并登录。源码构建要求 Python 3.12+、Node 22.12+，上游推荐 Node 24 LTS。构建后在虚拟环境依次配置、检查、启动：

```bash
kirocrew setup
kirocrew doctor
kirocrew gateway
```

默认网页入口为本机 5476 端口；远程访问先配置认证。主线 manifest 已是 `0.12.0`，发行首项仍为 `v0.11.0`，本页架构描述绑定主线 commit，不能当作对 0.11.0 安装包的验证。本轮未构建或运行。

## 原理

界面请求进入 Gateway，经会话、调度、策略与审批层调用 ACP 执行器及 MCP 工具。持久化状态支持重启续接；长任务分步执行与验证，定时任务和 heartbeat 可在无对话时触发。文档将策略 / profile 上限、路径与命令检查、输出脱敏、OS sandbox 和审计分层说明。

## 价值

适合把跨天开发、定期检查和多个消息入口汇到一个运行端。经验与技能可见可改，便于追查自动化行为；是否改善成功率、减少人工维护仍要以真实任务测量。

## 风险边界

- Apache-2.0；默认 Kiro CLI 登录、模型服务、消息连接与第三方依赖另有要求，自有硬件不等于离线。
- 架构文档称 `agent.sandbox` 默认 `auto` / standard；standard 为保留 git / 云 CLI 工作流，会保留部分 `~/.ssh`、`~/.aws`、`~/.kube` 可见性。strict 才进一步遮蔽这些存储，不能以“开启 sandbox”概括所有凭证保护。
- macOS / Linux 包装器、Windows 向官方 Kiro CLI 委托与无后端执行的处理不同；无隔离运行的默认值和显式开关依平台 / 治理策略而变，须检查 doctor、实际子进程和审计，不能假设跨平台等价。
- README 披露每天一个匿名使用心跳，以及安装公共 App 时的匿名收据；界面隐私开关、`kirocrew telemetry disable` 或 `KIROCREW_TELEMETRY_DISABLED=1` 控制外发，与本地诊断 telemetry 配置分开。此为文档核读，未抓包。
- 自主调度、动态技能和长期记忆可能保留错误或扩大重复动作，需检查权限、终止条件和任务恢复窗口。

## 补充建议

在专用工作区验证拒绝敏感路径、定时任务重复触发、Gateway 重启恢复、审批超时与主动停机。按平台分别留存 sandbox backend、可见凭证、联网及遥测关闭后的证据；不要用网页显示“完成”替代检查实际提交 / 产物。

## 参考资料

- [上游仓库](https://github.com/kirodotdev/KiroCrew)、[仓库 API](https://api.github.com/repos/kirodotdev/KiroCrew)。
- [README.md](https://github.com/kirodotdev/KiroCrew/blob/ec46e9bfaa4ed951b37cacfb7b978c7bb12ab616/README.md)。
- [LICENSE](https://github.com/kirodotdev/KiroCrew/blob/ec46e9bfaa4ed951b37cacfb7b978c7bb12ab616/LICENSE)。
- [pyproject.toml](https://github.com/kirodotdev/KiroCrew/blob/ec46e9bfaa4ed951b37cacfb7b978c7bb12ab616/pyproject.toml)。
- [docs/architecture/security-deep-dive.md](https://github.com/kirodotdev/KiroCrew/blob/ec46e9bfaa4ed951b37cacfb7b978c7bb12ab616/docs/architecture/security-deep-dive.md)。
