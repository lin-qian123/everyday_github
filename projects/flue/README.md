# flue（withastro/flue）

- GitHub: https://github.com/withastro/flue
- 官网: https://flueframework.com/
- 记录日期: 2026-06-20 (Asia/Shanghai)

## 定位

`flue` 是一个面向“真实可执行 agent”的 TypeScript harness 框架。它关注的不是 prompt 编排，而是把 session、skills、tools、sandbox、durable execution、subagents 和可部署运行时一起打包，帮助开发者做出接近 Claude Code / Codex 这类风格的自主代理。

## 热度信号

1. GitHub API 在 2026-06-20 抓取时显示约 `5.8k stars`、`324 forks`，并进入 GitHub Trending 日榜前列。
2. 官方 README 的第一句就是 `Not another SDK`，说明作者在主动把它和普通 LLM SDK 区分开。
3. README 反复强调 `sandbox`、`durable execution`、`skills`、`MCP servers`、`subagents`、`observability`，说明它的目标是 agent 运行底座，而不是 demo 框架。

## 用法

### 1) 先定义一个 agent

README 给出的最小示例就是在 TypeScript 中创建 agent：

```ts
import { createAgent, type AgentRouteHandler } from '@flue/runtime';
import { local } from '@flue/runtime/node';

export default createAgent(() => ({
  model: 'anthropic/claude-sonnet-4-6',
  tools: [...githubTools],
  skills: [triage, verify],
  sandbox: local(),
  instructions,
}));
```

### 2) 同时暴露 HTTP 路由

```ts
export const route: AgentRouteHandler = async (_c, next) => next();
```

这意味着它天然把 agent 当成可部署服务，而不是只能本地跑的脚本。

### 3) 选择部署与沙箱后端

官方文档和 README 提到的能力包括：

- 本地 Node.js 运行
- Cloudflare Workers
- GitHub Actions
- GitLab CI/CD
- Render
- Daytona 等沙箱环境

## 原理

1. `flue` 的核心是“给模型一个可持续工作的 harness”，把上下文、工具、技能和可执行环境组合成长期运行的 agent 实体。
2. 它把 agent 与 workflow 分开：agent 适合开放式自主任务，workflow 适合结构化自动化。
3. 通过 durable execution 机制，框架试图让 agent 在失败、重启和长任务场景下保持连续性。
4. 技能、MCP server、typed tools、channels 和 observability 共同构成运行时周边，使其更接近生产系统而不是 playground。

## 价值

- 对想做“真能操作文件、调用 API、分派子代理并长期执行”的团队，这类 harness 比简单 SDK 更实用。
- 它很好地代表了 2026 年 agent 基础设施的一个转向：从 prompt orchestration 走向执行环境 orchestration。
- TypeScript 生态团队如果本来就在 Node、Workers、CI 环境里工作，会比较容易接入。

## 风险边界

- 框架把权限、工具、技能和沙箱都拉进来后，安全设计就不再是附加项，而是核心复杂度。
- “自主”越强，验证与回滚需求越强；没有完善的观测和批准机制时，误操作代价会很高。
- 生产稳定性最终不只取决于框架本身，还取决于模型、沙箱实现、外部工具速率限制和状态持久化策略。

## 补充建议

1. 第一次试用时不要直接做开放式长任务，先从一个边界明确的 workflow，例如 issue triage 或 PR 检查开始。
2. 优先验证 durable execution 和 sandbox 行为，因为这是它相对普通 SDK 最关键的差异点。
3. 如果团队已经在用 MCP，把 `flue` 当成“技能 + 工具 + 持久执行”的运行底座看，会更容易评估它的长期价值。

## 参考资料

- https://github.com/withastro/flue
- https://flueframework.com/
- https://flueframework.com/docs/guide/building-agents/
- https://github.com/trending
