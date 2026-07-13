<!-- markdownlint-disable MD013 MD034 -->

# Daytona

- GitHub: https://github.com/daytonaio/daytona
- 分类：Agent 框架与技能生态
- 形态：AI 代码执行沙箱 / runtime 基础设施
- 抓取日期：2026-07-14

## 定位

`daytona` 是面向 AI-generated code 和 agent workflow 的安全、弹性代码执行基础设施。GitHub API 样本显示该仓库约 `72.2k stars`，topics 包含 `ai-sandboxes`、`code-execution`、`code-interpreter`、`ai-runtime`。

需要特别标注：项目 README 在 2026 年 6 月声明该公开仓库不再维护，核心开发已迁移到私有代码库。它仍有选型价值，但更适合作为“agent 沙箱架构样本”和历史开源实现参考，而不是直接当成新项目的长期依赖。

## 用法

README 中描述的使用路径包括：

1. 通过 SDK、API 或 CLI 创建 sandbox。
2. 在隔离环境中运行 Python、TypeScript、JavaScript 等代码。
3. 使用文件系统、进程执行、日志、Git 操作、预览代理、VNC/SSH 等工具能力。
4. 通过 snapshot 保留 agent 状态，支持跨 session 的长期任务。

由于公开仓库已停止维护，实际使用前应优先确认 Daytona 当前商业/私有平台文档和许可证边界。

## 原理

Daytona 把 agent 执行环境拆成多个 plane：

- Interface plane：SDK、API、CLI、Dashboard 等入口。
- Control plane：调度 sandbox 生命周期和资源策略。
- Compute plane：运行隔离 sandbox 实例。

其核心卖点是把 sandbox 做成“完整可组合计算机”：独立 kernel、文件系统、网络栈、CPU、内存和磁盘资源。这样 agent 运行代码时不直接污染用户本机，也能复现、暂停和恢复状态。

## 价值

- 对 coding agent：提供可编程执行环境，降低在开发者主机上直接运行未知代码的风险。
- 对企业：把审计、配额、网络限制、日志、密钥和环境模板集中管理。
- 对架构研究：展示了 agent runtime 从简单 Docker 容器走向可治理平台的方向。

## 风险边界

- 公开仓库已不再维护，这是最大风险；安全补丁、兼容性和路线图都不能默认依赖开源版本。
- 沙箱隔离不是万能防线，仍需网络、密钥、文件系统和供应链限制。
- 长期持久化 sandbox 可能积累敏感状态，应设置过期、清理和审计策略。
- 代码执行平台本身是高价值攻击面，部署时需要独立威胁建模。

## 补充建议

- 新项目选型时同时比较 `E2B`、`OpenSandbox`、`tupper`、`daytona`，重点看维护状态、隔离模型、SDK 体验和企业控制面。
- 对无人值守 coding agent，优先把执行环境放进受控 sandbox，再把写权限分阶段打开。
- 若只需要本地实验，不应把停止维护的公开版本接入生产密钥或生产网络。

## 参考资料

- GitHub 仓库：https://github.com/daytonaio/daytona
- 官方文档：https://www.daytona.io/docs
- Daytona GitHub 组织：https://github.com/daytona
