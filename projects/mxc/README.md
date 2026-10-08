<!-- markdownlint-disable MD013 -->

# Microsoft eXecution Container（microsoft/mxc）

> 上游仓库：<https://github.com/microsoft/mxc> · 归类：Agent 框架与技能生态 · 本页基于 2026-10-09 的 GitHub API、README、backend、schema、sample 与 telemetry 文档静态整理，未执行不可信模型输出或复测各平台隔离强度。

- 抓取快照：1,767 stars、103 forks、54 open issues。
- 热度信号：GitHub Rust Trending 抓取时约 +106 当日 stars；最后 push 为 2026-10-08。
- 版本与许可：最新 Release / tag `v1.0.0`，MIT；本页固定审计 commit `e157fa4bbde7`。

## 定位

MXC 是 Microsoft 的跨平台不可信代码执行 SDK，面向模型输出、plugin 和工具。应用通过统一 JSON policy 与 Rust / .NET / Node SDK 选择 Windows ProcessContainer、Windows Sandbox、WSLC、Linux Bubblewrap / LXC、macOS Seatbelt、MicroVM、Hyperlight 等 backend，并控制 filesystem、network、UI、lifecycle 与 I/O。

## 用法

应用从包管理器安装对应 SDK，提交 command、container type、timeout 和 policy；例如默认拒绝 network egress，再只开放必要路径和 host。采用前先运行 backend support probe，并用官方 transient / persisted / filesystem / network / telemetry sample 做当前 OS 验收。`--audit` 只能用于可信工具的 policy authoring，绝不能用来运行不可信代码。

## 原理

SDK 在进程内验证版本化 request，选择平台 backend，再创建一次性或持久 container 并启动 workload。统一模型描述期望权限，但隔离实施依赖 backend：Windows ProcessContainer、Bubblewrap 与 Seatbelt 是 OS 原语组合，Windows Sandbox、MicroVM / Hyperlight 等拥有不同的 VM 与实验状态；因此同一 policy 在不同平台不等价。

## 价值

MXC 将 Agent 产品常见的“执行模型生成代码”从零散 subprocess / container 调用提升为类型化 SDK、稳定 schema、backend 探测和跨平台 lifecycle。对宿主应用而言，统一的 deny policy、I/O capture、access-denied diagnostics 和持久环境接口能减少自行拼装隔离层的成本。

## 风险边界

- 多 backend 只统一 API，不统一安全强度；默认 backend 与实验 VM 的 kernel、filesystem、network 和 escape 面必须分别做威胁建模。
- README 明确 `--audit` 会关闭全部 sandbox 安全；若对不可信 workload 使用，会把诊断模式变成直接执行通道。
- policy allowlist 配错、宿主 mount、代理、clipboard / GUI 和持久 container 都可能扩大权限或跨任务残留。
- 部分 backend 标记 experimental；Release `v1.0.0` 不代表所有 OS / 架构 / backend 具有同等稳定性或生产 SLA。
- 官方 Windows build 的 telemetry 需要每次运行 opt-in、用户同意和 policy 允许；这仍需在集成产品中正确呈现、记录和测试。
- containment 不能判断代码是否满足业务目标，也不能替代资源 quota、供应链验证、输出审查、速率限制和宿主补丁。

## 补充建议

按平台建立 backend capability matrix，不支持或低强度 backend 默认拒绝不可信任务。用 canary 文件、内网诱饵、fork bomb、磁盘 / 内存配额、GUI / clipboard 与持久状态做负测试；固定 SDK、schema 和 native asset 版本，记录实际 backend，且让 audit artifact 与生产执行环境完全隔离。

## 参考资料

- [GitHub 仓库](https://github.com/microsoft/mxc)
- [GitHub REST API](https://api.github.com/repos/microsoft/mxc)
- [README](https://github.com/microsoft/mxc/blob/main/README.md)
- [Backend 文档](https://github.com/microsoft/mxc/tree/main/docs/backends)
- [配置 Schema](https://github.com/microsoft/mxc/tree/main/schemas/stable)
- [示例](https://github.com/microsoft/mxc/tree/main/samples)
- [Telemetry](https://github.com/microsoft/mxc/blob/main/docs/telemetry.md)
- [v1.0.0 Release](https://github.com/microsoft/mxc/releases/tag/v1.0.0)
