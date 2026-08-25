<!-- markdownlint-disable MD013 -->

# Apache Maka

> 上游仓库：[apache/maka](https://github.com/apache/maka) · 归类：Coding Agents 与终端助手 · 本页基于 2026-08-26 的上游 README、架构说明与 GitHub API 快照整理。

## 定位

Apache Maka（Incubating）是 local-first 的 agent 工作区：桌面端、终端和评测入口共同通过 Runtime Host 执行，模型消息、工具调用/结果、权限决定与终止状态被保存为可恢复的追加式执行记录。API 快照为 3,301 stars、327 forks、285 个开放 issue，Apache-2.0；GitHub Trending 抓取时显示约 +538 当日 stars。该信号说明短期开发者关注，不能证明稳定性、隔离强度或生产可用性。

## 用法

当前上游建议从源码构建，要求 Node.js 22.19+、npm、Git 与 `rg`；macOS Apple Silicon 是早期公开桌面构建，Windows 仍为未签名预览，尚无 Apache 正式发布包。

```sh
git clone https://github.com/apache/maka.git
cd maka
npm ci
npm run dev

# 先编译后使用开发 CLI
npm run build
npm run cli:dev -- run "Summarize this repository and identify its most important risk"
```

首次运行须在 Settings 配置并测试自带的模型/API/本地模型连接；不要把未接入 Runtime 的账号流当作可执行模型。首次试用应使用可丢弃仓库、无真实凭据的 provider 与只读任务。

## 原理

- Runtime Host 是唯一的执行通道；Desktop、TUI/CLI 和 eval 共享它，而不是各自维护不可对齐的 agent 状态。
- 每个 turn 的消息、调用、结果、审批与结束理由保存为 durable record；压缩旧工具输出只影响后续提示上下文，不等于删除可审计历史。
- 内置 `Read`、`Write`、`Edit`、`Bash`、`Glob`、`Grep`，越过 sandbox 边界的工具须审批；可中止、分类失败并恢复中断的 session。
- eval 用声明式实验扩展任务、重复与 subject 单元，记录得分、用量、成本、耗时、失败原因与产物；它是评测基础设施，不是模型能力证明。

## 价值

- 将 coding agent 的“做过什么、何时获批、工具返回什么”保留为可回放事实，便于故障恢复、复盘和受控评测。
- 本地优先数据位置和多模型连接，适合希望把桌面交互、CLI 与实验记录整合到同一执行内核的团队。
- 明确区分已保存历史与压缩后的模型上下文，可减少长会话 token 压力而不直接牺牲审计线索。

## 风险边界

- 项目仍在 Apache 孵化和积极开发期；接口、数据格式、CLI 与实验能力会变，孵化不等于功能或治理成熟度承诺。
- “sandbox boundary”不等于主机级完备隔离；写入、shell、网络、模型连接、第三方 gateway 和工作区指令仍须最小权限、人工审批和独立测试。
- 本地保存的执行记录可能包含源码、提示词、路径、工具输出或密钥；local-first 不是自动加密、脱敏、合规留存或安全备份。
- 所有模型成本、正确性与评测结果都依赖具体 provider、任务集、配置和评分标准，不能从项目 README 推导通用性能结论。

## 补充建议

1. 先在无敏感 fixture 上验证审批、取消、崩溃恢复、记录导出和删除/保留策略，再接入真实仓库或凭据。
2. 将 sandbox、网络出口、可写目录、模型 endpoint、token 预算和日志留存期分别显式配置；对工具调用与 prompt injection 设置人工闸门。
3. 以固定任务、版本、模型、重复次数和可审计评分运行 eval，并把失败、成本与人工返工一并记录。
4. 下载任何将来的预构建产物前核对 Apache 源码发布、签名与供应链说明；当前上游明确不建议把现有便利构建视为 Apache 正式发布。

## 参考资料

- [上游 README / 安装、能力与限制](https://github.com/apache/maka)
- [Backend Architecture](https://github.com/apache/maka/blob/main/ARCHITECTURE.md)
- [GitHub API 元数据](https://api.github.com/repos/apache/maka)
- [Apache Maka 的免责声明](https://github.com/apache/maka/blob/main/DISCLAIMER-WIP)
- [GitHub Trending](https://github.com/trending)
