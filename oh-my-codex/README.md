# oh-my-codex（Yeachan-Heo/oh-my-codex）项目速览与上手指南

- GitHub: https://github.com/Yeachan-Heo/oh-my-codex
- 更新时间: 2026-04-03（Asia/Shanghai）

## 1. 为什么今天值得跟踪

`oh-my-codex` 是今天 GitHub Trending 的高热 AI 开发工具之一，定位是给 Codex CLI 增加“多代理编排层”。

- 热度信号（2026-04-03 抓取）:
  - GitHub Trending: `2,852 stars today`
  - Trending 页面显示总量：`11,562 stars`、`1,073 forks`

## 2. 项目在做什么（核心定位）

官方一句话：`Your codex is not alone.`

它不是替代 Codex，而是在 Codex 之上补一层“组织与流程系统”：

1. 多代理协作
- 将复杂任务拆分到不同 agent（如探索、实现、验证），用并行模式压缩交付时间。

2. 可复用工作流
- 通过 skills / modes / hooks 让团队把“高频开发流程”固化成模板，减少重复提示词劳动。

3. 会话可观测性
- 用 HUD、日志、状态文件记录执行过程，方便回放、排障和复盘。

4. 与现有 CLI 生态兼容
- 设计目标是低侵入接入已有 agentic coding 习惯，而不是重做一整套 IDE。

## 3. 怎么用（快速上手）

下面给的是最短可运行路径（以官方 README 为准）：

## 3.1 安装

```bash
git clone https://github.com/Yeachan-Heo/oh-my-codex.git
cd oh-my-codex
```

官方 README 提供了一键安装入口：

```bash
./install.sh
```

## 3.2 基础健康检查

```bash
omx doctor
```

目的：先确认 shell、依赖、配置是否齐全，再进实际任务。

## 3.3 最小体验路径

```bash
omx setup
```

配置完后，用一个小任务测试：
- 让它扫描仓库并输出任务拆解
- 再让它执行单一子任务（如补测试或修一个 lint 问题）

建议先从低风险任务开始，逐步放大任务范围。

## 4. 原理是什么（工程视角）

1. “编排层”而非“模型层”
- 核心价值在任务分解、路由、并行与收敛，不在训练新模型。

2. 把 agent 当成可调度资源
- 通过策略决定何时并行、何时串行，目标是降低总等待时间与上下文丢失。

3. 标准化执行协议
- 把“探索 -> 实现 -> 验证 -> 总结”固定成可重复流程，提高稳定性。

4. 可观测 + 可回滚
- 执行状态有迹可循，出现偏航时能快速定位并切回上一步。

## 5. 适用场景

- 中大型代码库：单轮上下文难覆盖全局时，用多代理分治。
- 高频重复工程任务：如批量修复、批量补测试、批量升级。
- 需要可追溯交付的团队：要求记录“谁做了什么、为什么这么做”。

## 6. 风险与边界

1. 并行不等于无脑提速
- 任务切分不合理会放大冲突与合并成本。

2. 自动化程度越高，治理要求越高
- 需要明确 reviewer 边界、质量门禁、失败回退策略。

3. 对仓库规范有依赖
- 若项目缺少测试、lint、分层规范，编排系统收益会打折。

## 7. 实操建议（给你这种每日跟踪仓库）

1. 先用单仓试点
- 选一个活跃但可控的仓库，跑 1-2 周，观察“交付速度/返工率/冲突率”。

2. 固化最小工作流
- 至少固定三段：`分析`、`实现`、`验证`。

3. 把“失败样本”也纳入模板
- 记录失败拆解方式，防止团队重复踩坑。

## 8. 信息来源

- GitHub Trending（today）: https://github.com/trending?since=daily
- 项目仓库: https://github.com/Yeachan-Heo/oh-my-codex
- 项目 README（原文）: https://raw.githubusercontent.com/Yeachan-Heo/oh-my-codex/main/README.md
