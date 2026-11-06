<!-- markdownlint-disable MD013 -->

# llm-zoomcamp（DataTalks.Club 实践课程）

- 更新：2026-11-07（Asia/Shanghai）；官方 Jupyter Notebook daily +31，为读取快照，不是自然日结算。
- GitHub API：7,609 stars / 1,410 forks / 8 open issues（含 PR）；仓库 ID `777814395`。
- 核读基线：`2632cf7bae255172dce5c0021a524f1a46bf1158`；仅文档与抽样实现核验，未安装运行或独立评测。

## 定位

LLM Zoomcamp 是 DataTalks.Club 的免费实践课程，围绕 RAG、向量检索、Agent / function calling、编排、评估、监控和端到端项目。当前根目录是 2026 路线，历史 2024 / 2025 材料归入 cohorts；不是可不加判断部署的生产系统模板。[课程首页](https://github.com/DataTalksClub/llm-zoomcamp/blob/2632cf7bae255172dce5c0021a524f1a46bf1158/README.md)

## 用法

可随时自学，也可按当期 cohort 截止时间参加作业 / 同行评审。所谓 live cohort 主要指进度和评分，不等于每节实时授课。证书需要在 cohort 内完成项目并评审三份同学项目；自学不提供证书。免费材料与可选付费 AI Shipping Labs 社区应分开理解。

从 Module 1 环境和 code 子目录开始，按模块建立环境，避免把旧 cohort 依赖混在一起：

```bash
git clone https://github.com/DataTalksClub/llm-zoomcamp.git
cd llm-zoomcamp/01-agentic-rag/code
uv sync
```

先固定本页 SHA，再按模块文档配置 provider 与未入库的 .env；以上仅是源码学习路径，没有在本轮安装依赖。环境讲义写 Python 3.14+，实际 pyproject 写 >=3.12，需在拟用解释器上验证 lock / 依赖，不将两者混成单一已测支持范围。[环境讲义](https://github.com/DataTalksClub/llm-zoomcamp/blob/2632cf7bae255172dce5c0021a524f1a46bf1158/01-agentic-rag/02-environment.md)、[模块依赖](https://github.com/DataTalksClub/llm-zoomcamp/blob/2632cf7bae255172dce5c0021a524f1a46bf1158/01-agentic-rag/code/pyproject.toml)

## 原理

路线从关键词 RAG / 工具循环，扩展到 embedding、minsearch / SQLite / PGVector、Kestra 编排、数据接入、混合检索与 rerank。评估模块用 LLM 生成问答样本，再计算 Hit Rate、MRR 和 LLM-as-a-judge，并保存最终答案和工具轨迹。

合成 ground truth 是教学构造，不能天然充当人工事实金标；检索命中和答案忠实度也须分别测量。[评估模块](https://github.com/DataTalksClub/llm-zoomcamp/blob/2632cf7bae255172dce5c0021a524f1a46bf1158/04-evaluation/README.md)

## 价值

它把检索、生成、评估和反馈串成可操作的学习路线，便于形成可复现项目，而非只收藏 prompt。课程对项目要求数据、界面、评估、依赖版本和复现说明，适合建立个人工程作品与比较检索策略。

## 风险边界

- “不需 GPU”依赖课程使用云 API，并非不需外部服务或计算费用。README 估算约 1–5 美元 API credits；这是作者估算，实际费用随模型、重跑、judge 和服务计费变化，本轮未核价或调用。
- 根 README 指向 2026 schedule，但通用 project.md 的提交链接仍指向 cohorts/2025；实际截止时间、报名和提交流程须查当期页面，不沿用旧入口。
- 课程 FAQ 数据不能用作结课项目语料；应选独立、可授权分发的数据集，避免用训练式演示集夸大泛化表现。
- 根树未见 LICENSE，API 也未给出许可字段；“免费 / open-source 课程”措辞本身不足以证明所有材料可任意再分发。
- 本轮未跑 notebook、调用 API、评审项目、核实证书或完成教学视频观看。

## 补充建议

先做一个小型公开语料 RAG，保留题目、引用、预期答案和失败样例；按文档来源分割开发与测试样本，再比较关键词、向量和混合方案。人工复核合成评估题与 judge 分歧，记录每次实验的源码、模块 lock、模型版本、费用与重跑命令。报名时只使用当期 cohort 的正式入口。

## 参考资料

- [仓库](https://github.com/DataTalksClub/llm-zoomcamp)、[发行列表（本轮为空）](https://github.com/DataTalksClub/llm-zoomcamp/releases)。
- [固定课程首页](https://github.com/DataTalksClub/llm-zoomcamp/blob/2632cf7bae255172dce5c0021a524f1a46bf1158/README.md)、[环境](https://github.com/DataTalksClub/llm-zoomcamp/blob/2632cf7bae255172dce5c0021a524f1a46bf1158/01-agentic-rag/02-environment.md)、[依赖](https://github.com/DataTalksClub/llm-zoomcamp/blob/2632cf7bae255172dce5c0021a524f1a46bf1158/01-agentic-rag/code/pyproject.toml)。
- [评估](https://github.com/DataTalksClub/llm-zoomcamp/blob/2632cf7bae255172dce5c0021a524f1a46bf1158/04-evaluation/README.md)、[项目要求与旧 cohort 链接](https://github.com/DataTalksClub/llm-zoomcamp/blob/2632cf7bae255172dce5c0021a524f1a46bf1158/project.md)。
- [README 回链开课视频](https://www.youtube.com/watch?v=7TuZTVwnmhk)；元数据可核，未完整观看。
