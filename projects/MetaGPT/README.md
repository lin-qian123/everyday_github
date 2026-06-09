# MetaGPT（FoundationAgents/MetaGPT）

- GitHub: https://github.com/FoundationAgents/MetaGPT
- 记录日期: 2026-04-27 (Asia/Shanghai)

## 这是什么

`MetaGPT` 将“多角色协作”显式建模为软件生产流程：像一个虚拟团队一样分配 PM、架构师、工程师等角色完成任务。它在 Agent 社区的定位是“团队协同范式”的代表。

## 热度信号

1. OSSInsight AI Trending Top 50（2026-04-27 抓取）排名第 12，约 `59,362 stars`，近 28 天增长 `+336`。
2. 在“多 Agent 协同”讨论里，MetaGPT 仍是高频被引用的工程样板。

## 怎么用（最短路径）

### 1) 安装与配置

```bash
git clone https://github.com/FoundationAgents/MetaGPT.git
cd MetaGPT
```

- 按文档配置模型与密钥。

### 2) 运行一个小型需求

1. 输入一个明确产品需求（例如小型 Web 工具）。
2. 观察角色之间的任务交接与产物。
3. 对关键步骤加人工审核。

## 核心原理

1. 角色分工：不同 Agent 承担不同职责，减少单 Agent 过载。
2. 流程化协作：以“产物”驱动下一步，而不是纯对话驱动。
3. 反馈闭环：根据中间产物进行迭代修正。

## 适用场景

1. 需要把复杂需求拆成多阶段产出的团队。
2. 希望标准化“需求 -> 设计 -> 实现”链路。
3. 做 Agent 协作研究或流程评估。

## 价值与风险

价值：
- 对复杂任务的组织性更强。
- 产物边界清晰，便于审计。

风险：
- 角色越多，协调成本越高。
- 如果评审环节缺失，错误会被流程放大。

## 我认为有价值的补充材料

1. 先做 1-2 角色 MVP，再扩展到全角色。
2. 给每个角色定义明确输入/输出契约。
3. 对关键里程碑启用自动测试与人工 gate 双重校验。

## 参考来源

- https://github.com/FoundationAgents/MetaGPT
- https://ossinsight.io/trending/ai
