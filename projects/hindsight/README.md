<!-- markdownlint-disable MD013 -->

# Hindsight（vectorize-io/hindsight）

- GitHub：<https://github.com/vectorize-io/hindsight>
- 抓取快照：2026-09-25，27,732 stars、2,678 forks、191 open issues
- 热度信号：GitHub 综合 / Python Trending 抓取时约 +1,607 当日 stars
- 版本与许可：MIT；latest GitHub Release / tag 为 `v0.10.1`，`hindsight-api` manifest 同为 `0.10.1`

## 定位

Hindsight 是面向 AI Agent 的长期记忆服务，重点不是保存完整聊天记录，而是把事件、事实、经验、偏好和持续演化的“mental model”组织成可调用的 memory bank。它向应用提供 `retain`、`recall`、`reflect` 三类操作，并覆盖 SDK、REST、MCP、coding-agent 与多种 Agent 框架集成。

## 用法

可用 Docker、外部 PostgreSQL、Helm、`pip` server 或嵌入式 Python / Node 方式部署；客户端支持 Python、Node.js、Go、CLI 与 REST。最小流程是启动服务、为用户或项目选择独立 `bank_id`，写入内容后执行召回或反思；coding-agent 集成可自动从 Git 历史和既有会话构建项目 bank。托管 Hindsight Cloud 是另一条数据与运维边界，不能和自托管路径混写。

## 原理

输入先被结构化为不同记忆类型和 observations，再围绕 bank 建立时间、实体、关系与 disposition-aware 表示；`recall` 面向证据检索，`reflect` 在检索结果上进一步生成带当前心智模型的回答。服务可使用本地或云端 LLM provider，持久层可落在嵌入式 pg0、PostgreSQL 或企业数据库；wrapper 会在模型调用前召回、调用后自动保留内容。

## 价值

它把“跨会话记住什么、何时更新、如何召回”从应用 prompt 中拆成独立服务，便于多个 Agent / 应用复用同一项目或用户知识。SDK、MCP、框架集成与可见 benchmark 入口降低接入和比较成本，也为记忆版本、来源、延迟与 token 注入量建立可观察面。

## 风险边界

- README 的 LongMemEval 领先、企业采用和独立复现是上游陈述；本轮没有重跑数据集、模型、延迟、成本或污染检查，不能直接外推到私有任务。
- 自动 wrapper 会扩大默认采集范围；conversation、源码、Git 历史、身份偏好与模型生成的推断都可能进入 bank，必须设计保留期、删除、导出与纠错机制。
- `bank_id` 是逻辑隔离入口，不等于已经证明的多租户强隔离；认证、授权、备份、数据库权限和跨 bank 测试仍需独立完成。
- 自托管并不等于零外发：使用 OpenAI、Anthropic、Gemini 等 provider 时，召回上下文和待处理内容仍会发送给相应服务；Cloud 路径还增加托管方边界。
- `reflect` 生成的是模型综合，不是事实数据库查询；过期、矛盾、错误归因和“把推断记成事实”需要可回溯来源与人工纠正。

## 补充建议

先用合成角色和可穷举时间线建立 retain / update / forget / contradiction 金标，按用户、团队与项目设计独立 bank 和访问策略。固定 `v0.10.1`、模型、embedding、数据库与 prompt，联合记录 recall accuracy、P95 latency、注入 token、成本和删除传播；真实部署前再做跨租户、备份恢复、prompt injection 与敏感字段 redaction 测试。

## 参考资料

- [GitHub 仓库](https://github.com/vectorize-io/hindsight)
- [GitHub REST API](https://api.github.com/repos/vectorize-io/hindsight)
- [v0.10.1 Release](https://github.com/vectorize-io/hindsight/releases/tag/v0.10.1)
- [官方文档](https://hindsight.vectorize.io/)
- [在线 benchmark](https://benchmarks.hindsight.vectorize.io/)
- [Hindsight 论文](https://arxiv.org/abs/2512.12818)
- [安全策略](https://github.com/vectorize-io/hindsight/blob/main/SECURITY.md)
- [LICENSE](https://github.com/vectorize-io/hindsight/blob/main/LICENSE)
