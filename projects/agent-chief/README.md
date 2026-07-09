# agent-chief

<!-- markdownlint-disable MD013 MD012 -->

## 定位

`agent-chief` 是一个本地优先的“agent chief of staff”，目标是挡住无价值通知、判断哪些事件值得打断用户、把可委派任务派给 agent，并把低优先级信息沉淀到记忆。它更像是 agent、CI、RSS、heartbeat、watcher 和用户注意力之间的路由/判断层。

截至 2026-07-10 抓取时，GitHub 仓库约 `320` stars、`2` forks，主语言为 Python，许可证为 MIT。

## 用法

- 零配置体验可运行 `uvx agent-chief demo`。
- 常驻使用先 `uvx agent-chief init` 完成向导，再执行 `chief run`。
- 外部系统通过 `POST /v1/events` 或 MCP `propose` 提交事件。
- 用户可用 `chief trace <event_id>` 回放一次决策链，也可编辑本地 `POLICY.md` 覆盖学习结果。

## 原理

项目采用多阶段 worthiness engine：先用硬规则快速过滤，再用相似度分类器判断，必要时才调用 LLM judge。它按用户场景设置 interrupt threshold，并把决策原因、分数、命中的规则、token 成本和 prompt 版本记录下来。对可委派任务，agent 报告完成后还会通过 acceptance command 或二次判断验证。

## 价值

- 针对多 agent/自动化时代的真实痛点：不是缺 agent，而是缺注意力治理。
- 本地 SQLite + Markdown 存储、无云端遥测，适合个人工程师先试。
- 把“是否打扰我”变成可解释、可回放、可评测的决策，而不是单纯通知中心。
- 对常见 heartbeat agent 的空报告、CI 噪音、RSS 噪音有明确过滤价值。

## 风险边界

- 自动屏蔽通知存在漏报风险，前期应使用 shadow mode 或只做 digest。
- 学习用户偏好需要代表性反馈，少量点赞/点踩可能造成偏置。
- 事件内容可能包含敏感信息，连接外部 LLM judge 时要确认脱敏和本地策略。
- “verified dispatch” 的质量取决于每个任务的 acceptance command 或验证 prompt 是否可靠。

## 补充建议

- 适合与 `agentsview`、`ax`、`superlog` 对比：前者偏使用/成本分析，后两者偏 observability，`agent-chief` 偏注意力路由和委派验证。
- 接入真实工作流前，先跑一周 shadow mode，比较“本应打断”和“实际想看”的差异。
- 为不同事件源设置最小 schema，至少包含来源、严重性、用户可行动作和去重 key。

## 参考资料

- GitHub 仓库：<https://github.com/SmileLikeYe/agent-chief>
- PyPI：<https://pypi.org/project/agent-chief/>
