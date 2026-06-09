# ruflo（ruvnet/ruflo）

- GitHub：https://github.com/ruvnet/ruflo
- 更新日期：2026-06-02（Asia/Shanghai）

## 定位

`ruflo` 是一个面向 Claude Code / Codex 生态的多代理编排平台，核心卖点不是“再包装一个 agent”，而是给 coding agent 补上编排、记忆、联邦协作和治理层。

## 用法

### 1) 最小安装路径

```bash
npx ruflo@latest init wizard
```

### 2) 作为 MCP 服务接入

```bash
claude mcp add ruflo -- npx ruflo@latest mcp start
```

### 3) 启动一个基础 swarm

```bash
npx ruflo@latest swarm init --topology hierarchical --max-agents 8
```

### 4) 实际落地建议

1. 先只开最小 agent 数量和一条单任务链路。
2. 再逐步补充记忆、浏览器测试、安全审计、文档生成等插件。
3. 最后再考虑跨机器协作、联邦通信和自动后台 worker。

## 原理（工程视角）

1. 控制平面：接收任务、拆分目标、选择拓扑、调度 agent。
2. 执行平面：不同 agent 负责编码、测试、检索、审计等垂直职责。
3. 记忆层：通过向量检索、图谱或共享状态降低重复推理成本。
4. 工具层：通过 MCP、CLI 与插件体系把浏览器、文档、测试、审计工具统一纳入工作流。
5. 治理层：用 hooks、日志、成本追踪和安全扫描降低多代理失控风险。

## 价值

- 适合把“单个 coding assistant”升级成“可连续运转的工程流水线”。
- 对多仓库、多步骤、多人协作场景更有吸引力。
- 插件矩阵完整，适合观察当下 agent platform 正在把哪些能力产品化。

## 风险边界

- 多代理并行会放大权限、预算和错误传播问题。
- 记忆与联邦通信提升能力的同时，也增加敏感信息外泄面。
- 官方叙事覆盖面很广，落地时必须收缩到少量明确用例，否则很容易变成复杂度债务。

## 补充建议

1. 把它当“编排中间层”而不是“全能替代品”，先接入已有流程。
2. 给每类 agent 设清晰职责和退出条件，避免 swarm 变成高成本闲聊。
3. 在评估阶段优先验证三件事：可观测性、失败回退、成本上限。

## 参考资料

- GitHub：https://github.com/ruvnet/ruflo
- 安装 Wiki：https://github.com/ruvnet/ruflo/wiki/Installation-Guide
- GitHub Trending：https://github.com/trending
- 趋势汇总页（2026-06-01 快照）：https://github.com/Lilembas/detailed-github-trending
