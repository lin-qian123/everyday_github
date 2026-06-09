# open-webui（open-webui/open-webui）

- GitHub: https://github.com/open-webui/open-webui
- 记录日期: 2026-04-28 (Asia/Shanghai)

## 这是什么

`open-webui` 是开源 AI 统一交互前端，可对接本地模型与云模型，常被用作团队的“统一 AI 工作台”。

## 热度信号

1. OSSInsight AI Trending Top 50（2026-04-28 抓取）排名第 5。
2. 仓库约 `105,458 stars`，近 28 天增长 `+864`。

## 怎么用（最短路径）

### 1) 拉起服务

```bash
git clone https://github.com/open-webui/open-webui.git
cd open-webui
# 按官方文档选择 docker compose 或本地开发方式启动
```

### 2) 接入模型

1. 本地后端：连接 Ollama。
2. 云端后端：配置 OpenAI 兼容 API。

### 3) 跑通最小链路

- 建一个团队空间，配置模型路由与一个检索问答任务。

## 核心原理

1. 多模型统一入口：把模型调用与交互体验标准化。
2. 插件化扩展：支持外部工具与能力接入。
3. 检索增强：把知识源接入回答链路，提高可追溯性。

## 适用场景

1. 团队内统一 AI 门户。
2. 本地 + 云混合推理管理。
3. 需要快速验证多模型效果的业务团队。

## 价值与风险

价值：
- 上手快，适配多种后端。
- 便于组织内统一入口与权限管理。

风险：
- 多模型并存时，路由与成本控制复杂。
- 对话数据与审计策略需提前定义。

## 我认为有价值的补充材料

1. 先定义默认模型路由策略与回退策略。
2. 对敏感知识库启用细粒度访问控制。
3. 用“任务成功率 + 单任务成本”做每周复盘，而非只看活跃度。

## 参考来源

- https://github.com/open-webui/open-webui
- https://ossinsight.io/trending/ai
