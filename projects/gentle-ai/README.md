<!-- markdownlint-disable MD013 MD034 -->

# Gentle-AI：为既有 Coding Agent 配置记忆、工作流与审查证据

> 上游仓库：https://github.com/Gentleman-Programming/gentle-ai · 归类：Coding Agents 与终端助手 · 本页基于 2026-09-18 的 README、intended usage、telemetry、agent integration、release、LICENSE 与 REST API 静态整理；未运行 installer 或修改用户级 agent 配置。

## 定位

Gentle-AI 不提供新模型或新 coding agent，而是为 Pi、OpenCode、Claude Code、Codex、Cursor 等 16 类宿主写入统一的 memory、ODD / SDD workflow、skills、MCP、personas、security deny-list 与可选 RDD review。Go CLI 负责确定性状态迁移和配置备份。

2026-09-18 的 GitHub 官方 Go Trending 抓取显示约 `+65 stars today`；REST API 快照为 `6,965 stars / 760 forks / 1,066 open issues`，MIT，最新 release 为 `v3.1.0`（9 月 17 日），源码要求 Go `1.25.10`。

## 用法

上游支持 Homebrew、installer 与源码安装：

```sh
brew install gentleman-programming/tap/gentle-ai
gentle-ai
gentle-ai doctor
```

交互式安装器选择宿主、组件和 persona；`doctor` 是只读健康报告。项目称每次配置写入前会快照备份，但仍应在可恢复用户配置副本上先验证。

## 原理

- Engram 保存跨 session 项目记忆，并要求 Agent 在重复询问用户前先检索已有决策。
- ODD 让小任务保持轻量、较大任务写一个可恢复 feature document；正式 SDD 只在显式选择时进入 proposal / spec / design / tasks / apply 等阶段。
- opt-in RDD 冻结候选 lineage / revision，再按风险选择结构回读或多 lens review；提交、push 与 release 仍归用户。
- Go binary 读取磁盘状态并返回下一合法 transition，避免由模型临时猜流程状态。
- installer 为 16 类 Agent 写入原生配置；skills、Context7、CodeGraph、deny-list、personas 与 per-phase model assignment 按宿主能力启用。

## 价值

- 把记忆、流程和 review receipt 放到跨宿主层，团队可在更换模型 / Agent 后继续使用同一工程约束。
- 明确区分轻量 ODD、显式 SDD 与 opt-in review，减少所有任务被同一重流程绑住。
- 文件状态、确定性 transition、配置备份和 doctor 提供比纯 prompt 约定更可审计的恢复路径。
- README 明确 archive 不等于 ship / approve，review 也不夺取人的 commit / push 决策。

## 风险边界

- installer 会修改用户级 Agent 配置、skills、MCP 和 hooks；备份存在不等于所有宿主版本、并发写入和回滚都已验证。
- memory、workflow 和 persona 会持续影响后续会话；错误或恶意记忆可能把偏差长期固化并跨模型传播。
- deny-list 只覆盖已知路径，不能阻止 shell、外部工具、编码内容、网络或 symlink 等所有 secret 泄露路径。
- 上游有匿名 telemetry；文档称不发送 code / prompt / machine / organization，但会发送宿主、公开模型 family / suffix、agent class、token / duration / error category 等聚合字段，且旧的 install / heartbeat telemetry 是另一条路径。
- RDD receipt 和 verify 是过程证据，不是业务正确性、安全性、性能或独立 code review 的替代物。
- 本页未运行 `v3.1.0`，未验证 16 个宿主的配置 parity、telemetry opt-out、恢复、签名或工作流效果。

## 补充建议

1. 在新用户目录或可丢弃 VM 中列出 installer 的全部写入、备份、网络和 hook 行为，再迁移到真实配置。
2. 安装前保存配置 hash，安装后逐宿主检查 diff、skill source、MCP 权限和 model assignment，并实测恢复。
3. 阅读 telemetry 当前与 legacy 两部分，先选择明确 opt-out；抓包确认 endpoint、字段、失败与升级后的行为。
4. 用固定小 / 中 / 高风险任务比较 ODD、SDD 与 RDD 的额外成本、缺陷发现率和状态恢复，不以流程完成数当质量指标。

## 参考资料

- 上游 README：https://github.com/Gentleman-Programming/gentle-ai
- Intended Usage：https://github.com/Gentleman-Programming/gentle-ai/blob/main/docs/intended-usage.md
- Telemetry：https://github.com/Gentleman-Programming/gentle-ai/blob/main/docs/telemetry.md
- Agent integrations：https://github.com/Gentleman-Programming/gentle-ai/blob/main/docs/agents.md
- `v3.1.0` release：https://github.com/Gentleman-Programming/gentle-ai/releases/tag/v3.1.0
- GitHub REST API：https://api.github.com/repos/Gentleman-Programming/gentle-ai
- LICENSE：https://github.com/Gentleman-Programming/gentle-ai/blob/main/LICENSE
