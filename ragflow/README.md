# ragflow（infiniflow/ragflow）

- GitHub: https://github.com/infiniflow/ragflow
- 记录日期: 2026-04-25 (Asia/Shanghai)

## 这是什么

`ragflow` 是面向生产场景的开源 RAG 引擎，主打“高质量上下文构建 + Agent 能力融合”。相比只做向量检索的轻量方案，它强调从文档理解、切分、检索、重排到引用回溯的一体化闭环。

## 热度信号

1. OSSInsight AI Trending Top 50（2026-04-25 快照）位列前 10 左右。
2. GitHub 仓库页显示 `8.8k forks`、`2.9k issues`、持续高活跃开发与讨论。
3. 官方更新日志中 2026-03 仍有功能发布，说明项目迭代频率高。

## 怎么用（最短路径）

### 1) 准备运行环境

- 官方给出的最低建议：`CPU >= 4`、`RAM >= 16GB`、`Docker >= 24`。

### 2) 启动服务

```bash
git clone https://github.com/infiniflow/ragflow.git
cd ragflow
# 按官方 README 执行 docker compose 启动
```

### 3) 跑通第一条 RAG 链路

1. 接入一个知识源（PDF/网页/文档库）。
2. 配置分块模板与召回策略。
3. 用带引用的问答验证“可追溯输出”。

## 核心原理

1. 文档理解优先：强调复杂文档结构解析与知识提取质量。
2. 可解释检索链：检索结果、分块、引用可视化，便于人工干预。
3. Agent 融合：把 RAG 从“问答插件”升级为可编排的上下文层。

## 适用场景

1. 企业知识库问答（合规、可追溯要求高）。
2. 多来源文档汇聚（Confluence/Notion/S3 等）与统一检索。
3. 需要“检索 + 自动化动作”联动的 Agent 工作流。

## 价值与风险

价值：
- 在可追溯性和工程化方面比纯向量检索更完整。
- 能较好支撑中大型团队的知识系统演进。

风险：
- 系统复杂度与运维成本高于轻量 RAG。
- 若缺少评测集与监控，容易出现“看起来可用、实际不稳”的错觉。

## 我认为有价值的补充材料

1. 建议先搭建领域评测集（召回率/答案准确率/引用正确率）再上线业务。
2. 对高风险问答启用人工复核或双通道校验。
3. 将“知识更新延迟”纳入 SLA，避免旧文档持续污染回答。

## 参考来源

- https://github.com/infiniflow/ragflow
- https://ossinsight.io/trending/ai
- https://cloud.ragflow.io
