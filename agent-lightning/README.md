# agent-lightning

概览
agent-lightning 是一个“每个任务使用一个专用子智能体”的超轻量多智能体编排器。它把任务拆分为多个子 Agent 并并行执行，以显著降低整体时延和 token 成本。核心目标是让多任务协作更快、更便宜、更可控。

核心能力
- One-agent-per-task：每个任务独立 Agent，隔离上下文，减少干扰。
- 并发执行：子任务并行运行，降低等待时间。
- 低成本：使用轻量模型与上下文隔离减少 token 消耗。

原理与架构（基于公开说明的归纳）
agent-lightning 用“任务划分 + 并发调度”的方式分派子任务，子 Agent 拥有独立上下文并可并行执行，主调度器负责汇总结果，从而降低单线程链路的整体等待与成本。

快速上手
- 安装：
  - `pip install agent-lightning`
- 使用：
  - `from agent_lightning import Agent`
  - 创建 Agent，传入任务列表并运行。

使用场景
- 需要在一个请求内并发完成多个子任务的应用。
- 对成本和时延敏感的多步骤 LLM 工作流。

参考链接
- https://github.com/solololo/agent-lightning
