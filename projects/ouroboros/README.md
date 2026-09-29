<!-- markdownlint-disable MD013 -->

# Ouroboros（Q00/ouroboros）

> 上游仓库：<https://github.com/Q00/ouroboros> · 归类：Agent 框架与技能生态 · 本页基于 2026-09-30 的 GitHub API、README、runtime / platform 文档、Telemetry、Security Policy、Release 与 LICENSE 静态整理，未安装插件、运行 workflow 或复现评测结果。

- 抓取快照：6,139 stars、619 forks、90 open issues。
- 热度信号：GitHub Python Trending 抓取时约 +11 当日 stars。
- 版本与许可：MIT；latest Release、tag 与 PyPI 说明均为 `v0.55.2` / `0.55.2`。

## 定位

Ouroboros 自称面向 AI coding 的 “Agent OS”，实质是覆盖 Claude Code、Codex、OpenCode、Gemini、Kiro 等宿主的 specification-first workflow layer。它用访谈澄清需求，生成冻结的 Seed contract，以 ledger 记录事件，并通过分阶段执行、评估和演化减少长任务中的目标漂移。

## 用法

可通过 PyPI / `pipx` / `uv tool` 安装 `ouroboros-ai`，然后在支持的宿主中执行 `ooo setup` 与 `ooo interview`；也提供 Codex / Claude plugin 和 MCP server。上游 README 的 `curl | sh` / PowerShell 一键安装会自动探测宿主并写入配置，受限环境应改用包管理器路径，安装前固定版本并审阅生成的 runtime artifacts。

## 原理

核心流程为 interview → crystallize Seed → execute → evaluate → evolve。Seed 固定目标、验收和边界，ledger 保存可回放事件，runtime adapter 把同一合同映射到不同 Agent CLI / MCP；三阶段评估与 validation gate 决定是否接受结果。项目另有 plugin 应用层和 Ourocode shell，但这些仓库的权限与发行应分别审查。

## 价值

它把“写一段 prompt 后看 Agent 自由发挥”改造成可审阅规格、事件记录和验收循环，对多宿主、长时程和需要交接的 coding workflow 有工程价值。Seed、ledger 和可重复 evaluation 也便于比较不同 runtime，而不只比较最终回答文风。

## 风险边界

- “Agent OS”是工作流层定位，不是操作系统、容器或 sandbox；实际文件、网络、shell 与 secret 权限仍由宿主 runtime 和运行用户决定。
- workflow 与 plugin 可以触发任意工具调用；冻结 Seed 只能约束合同，不能从技术上阻止越权副作用或恶意依赖。
- 项目默认收集有限匿名 telemetry，包括安装、日活、runtime 和失败分类；虽支持 `DO_NOT_TRACK=1` / `OUROBOROS_TELEMETRY=0`，仍应先按组织政策配置。
- 一键安装与 `ooo setup` 会改动用户级宿主配置、skills / rules / plugin；升级和多 runtime 映射可能产生配置漂移。
- evaluation gate 只与验收命令、数据和环境一样可靠；Agent 可过拟合公开 verifier，静态 ledger 也不证明结果正确。
- 第三方 runtime、plugin、模型 provider 和生成代码不由 MIT 根许可或本项目 Security Policy 全部覆盖。

## 补充建议

在无 secret 的仓库副本和低权限 OS 用户中先试用，逐项审阅安装 diff、MCP / plugin capability 和 egress。把关键验收放到 Agent 无法修改的外部 runner，保留隐藏测试、预算和人工 review；默认关闭 telemetry 或完成隐私评审，并固定 Release 与全部 runtime 版本，准备卸载和配置回滚清单。

## 参考资料

- [GitHub 仓库](https://github.com/Q00/ouroboros)
- [GitHub REST API](https://api.github.com/repos/Q00/ouroboros)
- [v0.55.2 Release](https://github.com/Q00/ouroboros/releases/tag/v0.55.2)
- [使用指南](https://ouroboros.page/learn/en/)
- [Platform Support](https://github.com/Q00/ouroboros/blob/main/docs/platform-support.md)
- [Telemetry](https://github.com/Q00/ouroboros/blob/main/TELEMETRY.md)
- [Security Policy](https://github.com/Q00/ouroboros/blob/main/SECURITY.md)
- [LICENSE](https://github.com/Q00/ouroboros/blob/main/LICENSE)
