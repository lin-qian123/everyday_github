# dify（langgenius/dify）

- GitHub: https://github.com/langgenius/dify
- 文档: https://docs.dify.ai/
- 记录日期: 2026-04-28 (Asia/Shanghai)

## 这是什么

`dify` 是开源 LLM 应用平台，强调从 Prompt Demo 到可运营 AI 产品的全链路能力（工作流、知识库、模型接入、发布与监控）。

## 热度信号

1. OSSInsight AI Trending Top 50（2026-04-28 抓取）排名第 4。
2. 仓库约 `111,030 stars`，近 28 天增长 `+798`。

## 怎么用（最短路径）

### 1) 本地启动（Docker）

```bash
git clone https://github.com/langgenius/dify.git
cd dify/docker
docker compose up -d
```

### 2) 创建最小应用

1. 在控制台创建 Chatbot/Workflow 应用。
2. 配置模型供应商 API Key。
3. 可选接入知识库，发布 Web/API 端点。

## 核心原理

1. 可视化编排：把多步 LLM 流程显式化与可维护化。
2. 统一模型抽象：屏蔽不同模型供应商接口差异。
3. 运营层内建：日志、观测、权限与版本迭代。

## 适用场景

1. 企业内部知识问答与流程助手。
2. 需要低代码快速落地 AI 应用的团队。
3. 要求业务同学可参与迭代的场景。

## 价值与风险

价值：
- 从研发到运营路径完整，交付速度快。
- 非纯工程团队也能参与应用迭代。

风险：
- 工作流复杂后会出现“可视化债务”。
- 模型与提示词治理仍需工程规范补位。

## 我认为有价值的补充材料

1. 建立工作流命名与版本规则，避免后期不可维护。
2. 关键节点加回归集与自动评测，不只看演示效果。
3. 先做 1-2 个高频业务场景再扩散，防止平台先行过度建设。

## 参考来源

- https://github.com/langgenius/dify
- https://docs.dify.ai/
- https://ossinsight.io/trending/ai
