# background-agents（ColeMurray/background-agents）

- GitHub: https://github.com/ColeMurray/background-agents
- 官网: https://backgroundagents.dev
- 记录日期: 2026-06-22 (Asia/Shanghai)

## 定位

`background-agents` 是一个把 coding agent 放到后台长期运行的开源系统。它不是只在本地开一个终端会话，而是试图把 Web、Slack、GitHub、Linear、Webhook、定时任务和云沙箱统一成一个可调度的后台代理平台。

## 热度信号

1. GitHub API 在 2026-06-22 抓取时显示约 `2.0k stars`、`311 forks`，`updated_at` 为 `2026-06-22T00:58:06Z`。
2. GitHub Trending Developers 的 TypeScript 榜单在 2026-06-22 抓取时把 `background-agents` 作为热门仓库展示。
3. 官方 README 直接把它定义为 `An open-source background agents coding system`，并强调 Web、Slack、GitHub PR、Linear issue、Webhook 与 scheduled automation。

## 用法

### 1) 先按官方文档完成部署

README 把 `docs/SETUP_GUIDE.md` 和 `docs/GETTING_STARTED.md` 作为推荐入口，说明这个项目的核心体验不是单文件 CLI，而是先把控制面、沙箱和认证链路搭起来。

### 2) 让代理在后台执行代码任务

官方描述的典型能力包括：

- 后台持续跑任务，不阻塞当前会话。
- 连接完整开发环境，包括 `Node.js`、`Python`、`git`、浏览器自动化和浏览器版 `VS Code`。
- 通过 GitHub PR 和用户 OAuth 做变更归属。

### 3) 并行拆分子任务

README 明确写到可以通过 `spawn-task` 创建并行子会话，在独立沙箱中拆分执行任务，并用 `get-task-status` / `cancel-task` 做协调。

## 原理

1. 它把“聊天入口”和“执行环境”拆开，让用户从 Web、Slack 或 issue 触发任务，真正执行发生在远端沙箱里。
2. Git 操作依赖共享 GitHub App 安装，PR 创建则尽量回落到用户自己的 OAuth 身份，以保持归属关系。
3. 从 README 的架构和安全模型看，它更像内部工程团队的后台代理控制面，而不是面向公网多租户的 SaaS。

## 价值

- 对已经进入“多任务并行 + 异步代理”阶段的团队，它比单终端 agent 更接近真实工程流。
- 它代表了一个明显趋势：coding agent 不再只是当前 shell 的副驾驶，而是在往队列化、计划化、长期运行的 worker 演化。
- 如果你关心的是自动化值守、告警触发修复、夜间批量任务，这类系统比单点 IDE 插件更值得跟踪。

## 风险边界

- README 明确声明当前设计只适合 `single-tenant deployment`；如果跨团队或多租户复用，共享 GitHub App 权限会放大安全风险。
- 后台代理能接触更多仓库、凭据和运行时资源，失败半径明显大于本地单会话工具。
- 并行子任务和远端沙箱提升了吞吐，但也会提高成本、审计和失败恢复复杂度。

## 补充建议

1. 如果要试用，先在可信内部仓库里验证最小闭环，不要直接接到“全组织全部仓库”。
2. 重点评估三件事：权限隔离、失败回收、PR 归属和审计链是否满足团队要求。
3. 它适合与 `Archon`、`mcphub` 这类流程层和工具层项目一起看，理解后台代理平台这一层正在怎样成形。

## 参考资料

- https://github.com/ColeMurray/background-agents
- https://backgroundagents.dev
- https://github.com/trending/developers/typescript
