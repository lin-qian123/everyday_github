# OpenHands（All-Hands-AI/OpenHands）

- GitHub: https://github.com/All-Hands-AI/OpenHands
- 文档: https://docs.all-hands.dev/
- 记录日期: 2026-04-28 (Asia/Shanghai)

## 这是什么

`OpenHands` 是开源开发者 Agent 平台，强调真实工程闭环：读仓库、改代码、执行命令、根据反馈持续修复。

## 热度信号

1. OSSInsight AI Trending Top 50（2026-04-28 抓取）排名第 11。
2. 仓库约 `60,297 stars`，近 28 天增长 `+325`。

## 怎么用（最短路径）

### 1) 启动容器（按官方示例）

```bash
docker pull docker.all-hands.dev/all-hands-ai/runtime:0.49-nikolaik
docker run -it --rm \
  -e SANDBOX_RUNTIME_CONTAINER_IMAGE=docker.all-hands.dev/all-hands-ai/runtime:0.49-nikolaik \
  -e LOG_ALL_EVENTS=true \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -p 3000:3000 \
  --add-host host.docker.internal:host-gateway \
  --name openhands-app \
  docker.all-hands.dev/all-hands-ai/openhands:0.49
```

### 2) 最小任务验证

1. 连接一个小型仓库。
2. 给出单一目标（如补测试或修 1 个 bug）。
3. 审核执行日志与 diff，再放大任务范围。

## 核心原理

1. 代理执行循环：计划 -> 执行 -> 验证 -> 修正。
2. 沙箱隔离：把高风险操作收敛在可控环境。
3. 工具链集成：可调用 Shell、Git、测试工具完成端到端任务。

## 适用场景

1. 自动化修复与重构试点。
2. 需要“可执行”而非“只建议”的开发场景。
3. 用于评估 Agent 工程化边界的团队。

## 价值与风险

价值：
- 更接近真实研发流程。
- 便于观察 Agent 在复杂任务中的行为模式。

风险：
- 任务边界不清会导致漂移与成本上升。
- 高权限工具接入必须有审批与审计。

## 我认为有价值的补充材料

1. 先从只读/低风险任务起步，逐步放权。
2. 为每类任务定义“完成标准 + 失败回退策略”。
3. 保存失败轨迹样本，用于后续提示词与策略优化。

## 参考来源

- https://github.com/All-Hands-AI/OpenHands
- https://docs.all-hands.dev/
- https://ossinsight.io/trending/ai
