<!-- markdownlint-disable MD013 MD034 -->

# openresearch-cli：为并行科研 agents 保存实验谱系与可追溯工件

## 项目概览

- 上游仓库：https://github.com/alphaXiv/openresearch-cli
- GitHub API 快照（2026-09-02）：644 stars、47 forks、7 个开放 issue
- 当前 release：`v0.1.118`
- 主要技术：Rust CLI、本地 Web dashboard、SQLite、Git / worktree、SSH 与多类远程计算后端
- 许可证：MIT

## 定位

OpenResearch 是本地优先的科研 agent 工作区。它让 Claude Code、Codex 或 OpenCode 分别在独立 session / worktree 中探索文献、假设、代码和实验，并把 commit、日志、diff、结果与工件绑定到实验树。

它是科研执行与记录基础设施，不是自动证明科学结论正确的系统；“autoresearch”描述的是循环能力，不代表实验设计、数据、统计或引用已经通过同行评审。

## 用法

上游提供桌面应用，也提供 macOS / Linux 安装脚本：

```bash
curl -LsSf https://openresearch.sh/install.sh | sh
orx up
```

默认 dashboard 运行在 `127.0.0.1:4791`。`orx install-skills` 可向受支持的 coding agent 安装技能；`orx exp run`、`orx logs`、`orx paper` 等命令管理实验、日志和文献入口。远端模式可通过 SSH 把服务放在 GPU 主机旁。

## 原理

项目为每个研究方向分配独立 agent session 与 Git worktree，用实验树保存变体之间的谱系；每次运行绑定已记录 commit 的不可变归档，并把日志、文件、diff、结果和产物留在同一上下文中。

同一源码快照可调度到本地、SSH、Slurm、Kubernetes、Ray、Hugging Face Jobs、Modal、Tinker 或托管计算。上游同时说明：远端服务绑定 loopback 但没有应用层认证，同一远端主机上的其他用户可能访问。

## 价值

- 把并行 agent 探索与 Git 版本、实验运行和工件谱系绑定。
- 本地 SQLite、loopback dashboard 和自有计算路径降低不必要的代码发布。
- 同一界面连接交互式 agent、批处理和 HPC 后端，适合研究工程交接。
- 日志、diff 与结果并置，有助于区分“agent 建议”与“实际运行证据”。

## 风险边界

- 保存 commit 和日志不等于完全可复现；数据版本、环境、随机种子、驱动、调度器和外部服务仍需记录。
- autoresearch 可自动改代码和启动实验，可能消耗大量 GPU 配额、写错共享存储或重复提交作业。
- worktree 隔离 Git 文件状态，但不是 OS、网络、凭据或数据访问隔离。
- 远端 dashboard 没有应用层认证；共享主机、SSH 转发和端口暴露必须单独审计。
- 官方 release 默认发送可关闭的粗粒度遥测；敏感环境应明确执行 `orx telemetry off` 并验证网络出口。
- 本页依据上游静态资料与 API，未安装，也未向 Slurm/GPU 提交实验。

## 补充建议

1. 先在小型合成项目上固定 commit、环境锁文件、数据哈希、随机种子和资源上限。
2. 把“提议实验”和“允许提交”分开，对 GPU 数、时长、队列、费用和输出路径设置硬门槛。
3. 在共享主机上使用专用账户与 SSH 隧道，不把未认证 dashboard 暴露给局域网或公网。
4. 用同布局短测试核对 Slurm/Kubernetes 后端的环境、挂载、日志和停止行为，再扩展正式任务。
5. 报告中分别标记静态代码、排队、运行中、成功退出、诊断产物和科学结论，避免把流程记录升格为实验结果。

## 参考资料

- 仓库与 README：https://github.com/alphaXiv/openresearch-cli
- 官方站点：https://openresearch.sh
- 文档：https://openresearch.sh/docs
- Releases：https://github.com/alphaXiv/openresearch-cli/releases
- 安装页：https://openresearch.sh/download
- 遥测说明：https://github.com/alphaXiv/openresearch-cli#usage-analytics
