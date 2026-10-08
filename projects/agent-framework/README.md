<!-- markdownlint-disable MD013 -->

# Microsoft Agent Framework（microsoft/agent-framework）

> 上游仓库：<https://github.com/microsoft/agent-framework> · 归类：Agent 框架与技能生态 · 本页基于 2026-10-09 的 GitHub API、README、samples、decision records、transparency 与 migration 文档静态整理，未连接 Foundry、Azure OpenAI、GitHub Copilot SDK 或第三方 Agent / tool。

- 抓取快照：14,019 stars、2,448 forks、783 open issues。
- 热度信号：GitHub Python Trending 抓取时约 +24 当日 stars；最后 push 为 2026-10-08。
- 版本与许可：多包仓库；GitHub latest Release 为 `python-1.21.0`，MIT；本页固定审计 commit `2d9cc3f8ae46`。

## 定位

Microsoft Agent Framework（MAF）是面向 Python 与 .NET 的生产级 Agent / workflow 框架，Go SDK 独立维护。它统一 provider、middleware、graph workflow、multi-agent orchestration、checkpoint、streaming、human-in-the-loop、OpenTelemetry、declarative agent、skills、DevUI 与本地 / 云端 hosting，并提供从 Semantic Kernel 和 AutoGen 迁移的路径。

## 用法

Python 可安装 `agent-framework`，.NET 使用 `Microsoft.Agents.AI` 等包；先从单 Agent、本地 mock tool 和固定 provider 开始，再把 sequential / concurrent / handoff workflow、checkpoint 与 hosting 逐层加入。开发时 Azure CLI credential 方便，但生产应改为明确 credential / managed identity，并将 tool、model、memory、trace 与第三方 endpoint 分别做权限和数据流审查。

## 原理

Agent 把 provider client、instruction、tool 与 middleware 组合为可运行单元；workflow 用图描述节点、edge、handoff、并发和人机暂停，checkpoint 支撑恢复与 time-travel。provider adapter 与 hosting layer 将相同抽象连接到 Foundry、Azure OpenAI、OpenAI、GitHub Copilot 和其他系统；OpenTelemetry 记录跨 Agent / tool 的执行链。

## 价值

它把 Microsoft 既有 Semantic Kernel / AutoGen 经验收敛到较一致的 Python / .NET API，并同时考虑耐久性、恢复、治理、观测与部署。对从原型走向服务的团队，多种 orchestration pattern、middleware、checkpoint 和 samples 能减少自建状态机与跨语言接口成本。

## 风险边界

- framework 提供编排，不提供默认业务正确性；handoff、group collaboration 与 checkpoint 可能持久化或放大错误状态。
- provider、tool、third-party Agent 与 non-Azure model 具有不同的日志、保留、区域、费用和许可；抽象层不会消除这些差异。
- human-in-the-loop 只有在 workflow 正确设置 pause、展示足够上下文并校验恢复 token 时才有效，不是自动审批保证。
- OpenTelemetry、DevUI、checkpoint、memory 和 transcript 会形成集中敏感数据面；生产必须配置采样、脱敏、访问和保留期。
- latest Release 只代表 Python 包线；Python、.NET、Go、hosting extension 与实验 Labs 版本不能用一个 tag 概括。
- 上游明确要求集成者自行实现 metaprompt、content filter、权限、可靠性与 responsible-AI 缓解，本轮未复测样例外任务。

## 补充建议

建立跨 Python / .NET 的最小 golden workflow，注入 provider timeout、重复 tool result、handoff 失败、checkpoint 损坏和恶意 tool output。锁定每个包与 schema 版本，trace 只保留脱敏字段；迁移 Semantic Kernel / AutoGen 时按行为和状态兼容验收，不以代码能编译作为完成标准。

## 参考资料

- [GitHub 仓库](https://github.com/microsoft/agent-framework)
- [GitHub REST API](https://api.github.com/repos/microsoft/agent-framework)
- [README](https://github.com/microsoft/agent-framework/blob/main/README.md)
- [Microsoft Learn 文档](https://learn.microsoft.com/en-us/agent-framework/)
- [Python samples](https://github.com/microsoft/agent-framework/tree/main/python/samples)
- [.NET samples](https://github.com/microsoft/agent-framework/tree/main/dotnet/samples)
- [Transparency FAQ](https://github.com/microsoft/agent-framework/blob/main/TRANSPARENCY_FAQ.md)
- [python-1.21.0 Release](https://github.com/microsoft/agent-framework/releases/tag/python-1.21.0)
