<!-- markdownlint-disable MD013 -->

# ADR（uber/ADR）

> 上游仓库：<https://github.com/uber/ADR> · 归类：Agent 框架与技能生态 · 本页基于 2026-10-08 的 GitHub API、README、Sensor / Detection / Discovery 文档与源码静态整理，未采集真实员工 Agent 日志、运行攻击 benchmark 或复测论文指标。

- 抓取快照：1,900 stars、196 forks、5 open issues。
- 热度信号：GitHub Python Trending 抓取时约 +36 当日 stars；最后 push 为 2026-10-07。
- 版本与许可：最新 Release `sensor-v1.0.0`；根仓库 Apache-2.0，vendored AgentDojo 代码另为 MIT；本页固定审计 commit `8ba11735e349`。

## 定位

ADR（Agentic AI Detection and Response）是 Uber 开源的企业 Agent 安全研究与观测套件：发现终端上的 AI 工具，归一化 coding-agent 活动，运行合成攻击任务，并用双层 detector 标记高风险会话。上游称其相关系统已在 Uber 生产部署，但开源仓库不是完整生产系统。

## 用法

最小、无真实日志的入口是克隆仓库后进入 `Detection/`，用 `uv sync` 安装依赖，再对仓库提供的 packed synthetic benchmark 运行 detector。默认 ADR detector 需要模型 API key；`llamafirewall` 可作不带 key 的 smoke test。正式接入 Sensor 或 Discovery 前，应先确认日志来源、保存周期、脱敏字段、员工告知与合法处理依据。

## 原理

Discovery 通过指纹与 endpoint probe 盘点应用、CLI、IDE 扩展、本地模型和 MCP server；Sensor 读取 Claude Code、Codex、Cursor、Copilot CLI、Gemini CLI 等本地日志并映射到统一 schema；Detection 先做高召回 triage，再对可疑 session 做更深的 Agent 分析。ADR-Bench 提供 303 条已打包对话与额外任务定义、134 个模拟 MCP server 和合成 prompt-injection / 越权场景。

## 价值

它把“装了哪些 Agent”“Agent 实际调用了什么工具”“防御能否识别攻击”放到同一可复现实验面，且提供输入哈希、manifest、packed benchmark 和基线复现说明。对企业安全团队而言，统一日志 schema 与可回放检测比只审静态配置更接近真实运行风险。

## 风险边界

- 开源仓库不包含 Prevention，也不包含强化 detector 的离线 ADR Explorer；不能据项目总览声称已实现自动阻断或完整产品能力。
- Sensor 可读取 prompt、tool arguments、tool results、会话路径与模型元数据；这些往往含源码、凭据和个人信息，集中采集会扩大敏感面。
- Detection 明确是研究制品，含已知 CVE 的固定依赖、合成凭据和恶意 payload，只能在隔离容器 / VM / 专用主机运行，不能接生产 MCP、真实 key 或真实数据。
- 论文 benchmark、Uber 内部部署与公开 packed dataset 的可见范围不同；本仓库的复现文档明确不提供生产部署结果，不能把实验指标外推为本组织检出率。
- 双层 LLM detector 仍受模型、prompt、阈值、成本与概念漂移影响；告警不是攻击事实，未告警也不是安全证明。
- Discovery 的“发现”依赖指纹目录和 probe 覆盖，未知工具、便携二进制、远端执行与未落盘会话可能漏检。

## 补充建议

先用 packed benchmark 固定 commit、lockfile、模型、配置和随机性复现实验，再用本组织批准的合成日志做盲测。生产评估将采集、传输、存储、检测、告警和处置拆开授权，默认只保留必要字段，并用人工复核与误报 / 漏报回放校准阈值。

## 参考资料

- [GitHub 仓库](https://github.com/uber/ADR)
- [GitHub REST API](https://api.github.com/repos/uber/ADR)
- [Sensor 文档](https://github.com/uber/ADR/blob/main/Sensor/README.md)
- [Detection 文档](https://github.com/uber/ADR/blob/main/Detection/README.md)
- [Discovery 文档](https://github.com/uber/ADR/blob/main/Discovery/README.md)
- [复现说明](https://github.com/uber/ADR/blob/main/docs/REPRODUCIBILITY.md)
- [开源审查与合成数据说明](https://github.com/uber/ADR/blob/main/docs/OPEN_SOURCE_REVIEW.md)
- [sensor-v1.0.0 Release](https://github.com/uber/ADR/releases/tag/sensor-v1.0.0)
