# production-agentic-rag-course

## 项目定位
`production-agentic-rag-course` 是一个“边做边学”的生产级 RAG 课程仓库，主题是从零搭一个面向论文检索与问答的研究助手，并逐步进化到带 LangGraph 与 Telegram Bot 的 agentic RAG 系统。

- GitHub：https://github.com/jamwithai/production-agentic-rag-course
- 适用人群：RAG 工程初学者、想把 demo 升级到生产化架构的 AI 工程师、做研究助手类产品的人。

## 用法

官方 Quick Start 的主线很清晰：

1. 准备环境：Docker Desktop、Python 3.12+、`uv`、至少 8GB 内存和 20GB 磁盘。
2. 克隆仓库并复制 `.env.example` 到 `.env`。
3. 安装依赖：`uv sync`。
4. 启动全套服务：`docker compose up --build -d`。
5. 用 `curl http://localhost:8000/api/v1/health` 检查服务健康状态。

如果想直接看 agentic RAG 部分，仓库还提供了 `notebooks/week7/week7_agentic_rag.ipynb` 作为实操入口。

## 原理

这个项目的价值在于它把“课程”做成了可运行系统，而不是只讲概念：

- 数据层：自动抓取和解析 arXiv 论文，形成结构化语料。
- 检索层：先做生产化 BM25 关键词检索，再叠加向量检索，强调 hybrid search。
- 生成层：接入本地 LLM、流式响应和 Gradio 界面。
- 可观测层：加入 Langfuse tracing 与 Redis caching，开始关注生产运维问题。
- Agent 层：用 LangGraph 编排 guardrail、retrieve、grade、rewrite、generate 等节点，并接入 Telegram Bot。

它的核心方法论很明确：先把搜索基础打稳，再谈 agentic RAG，而不是一开始就堆“智能感”。

## 价值

- 对想系统补课的人，它比零散博客更完整，因为把基础设施、搜索、监控、Agent 一路串起来了。
- 对工程团队，它提供的是“课程化脚手架”，方便快速搭出可演示、可扩展的研究助手。
- 对做垂直知识库产品的人，这类仓库可以作为内部 PoC 蓝本。

## 风险边界

- 这是课程仓库，不等于开箱即用的生产方案；部署、鉴权、数据治理仍需团队自己补。
- 依赖 OpenSearch、PostgreSQL、Airflow、Langfuse、Redis 等组件，学习成本和运维成本都不低。
- 论文问答场景较友好，迁移到企业知识库后会立即遇到权限、更新频率和引用可信度问题。

## 补充建议

- 如果你要复用它，优先抽取三部分：数据管道、混合检索、LangGraph 工作流；不要一上来全盘照搬。
- 做企业版 PoC 时，应尽早补上鉴权、引用回链、失败回退和离线评测。
- 这个项目最值得学的不是“Telegram Bot”，而是它坚持把传统搜索、监控和 agent 编排放在同一张工程图里。

## 参考资料

- 仓库主页：https://github.com/jamwithai/production-agentic-rag-course
- Week 7 博文：https://jamwithai.substack.com/
- GitHub Trending：https://github.com/trending
