# agent-native（BuilderIO/agent-native）

- GitHub: https://github.com/BuilderIO/agent-native
- 官网: https://agent-native.com/
- 记录日期: 2026-06-20 (Asia/Shanghai)

## 定位

`agent-native` 是一个把“Agent”和“产品 UI”放在同一系统里设计的开源框架。它不是单纯再包一层聊天窗口，而是试图让同一套 action、状态、权限、技能、记忆和协作界面同时服务于人类用户与 AI agent。

## 热度信号

1. GitHub API 在 2026-06-20 抓取时显示约 `1.0k stars`、`117 forks`，但已经进入 GitHub Trending 日榜前列，说明它属于“起量很快的新框架”。
2. 官方 README 把卖点直接写成 `Agents and UIs — Fully Connected`，并强调 `shared one database and one state`、`real-time multiplayer`、`skills, memory, instructions, sub-agents, and MCP servers`。
3. README 还明确给出 `headless API / rich chat / whole app` 三种产品形态，说明它的目标不是单点 agent SDK，而是完整的 agent-native 应用底座。

## 用法

### 1) 先从技能入口快速试用

官方 README 给出的最低门槛体验是给现有 coding agent 增加技能：

```bash
npx @agent-native/core@latest skills add visual-plan
```

这会为 Claude Code、Codex、Cursor、OpenCode、GitHub Copilot / VS Code 一类工具增加 `/visual-plan` 和 `/visual-recap` 命令。

### 2) 以 action 为中心搭应用

README 的核心示例是先定义一份 action，再让它同时服务于 UI、agent、HTTP、MCP、A2A 和 CLI：

```ts
export default defineAction({
  schema: z.object({
    emailId: z.string(),
    body: z.string(),
  }),
  run: async ({ emailId, body }) => {
    await db.insert(replies).values({ emailId, body });
  },
});
```

### 3) 选择产品形态

- `Headless`：把 agent 当后端能力，供代码、CLI、HTTP 或 MCP 调用。
- `Rich chat`：做成内嵌或独立聊天入口。
- `Whole app`：让 chat 与完整 SaaS UI 共用状态与动作层。

## 原理

1. 框架把 `action` 设计成统一能力面，避免 UI、API、MCP 和 agent 各写一套接入逻辑。
2. agent 运行时内置聊天、工具、技能、记忆、任务、可观测性和 handoff，尽量减少开发者拼装多套中间件。
3. 数据层走 SQL + Drizzle，部署层走 Nitro 兼容宿主，目标是保持“后端可替换、宿主可替换、不锁平台”。
4. 从 README 的结构看，它还特别强调外部 agent 连接能力，试图让 Claude、ChatGPT、Codex、Cursor 等通过同一 action surface 接入同一个应用。

## 价值

- 这是很有代表性的“agent 不再只是旁路助手，而是产品本体一部分”的路线。
- 对做 agent-native SaaS、内部运营系统、可协作工作台的团队来说，它比单纯聊天 SDK 更接近真实产品需求。
- 如果这条路线成立，开发团队可以少维护很多“UI 一套逻辑、agent 一套逻辑”的重复工程。

## 风险边界

- 这是架构层框架，不是零配置玩具；数据库、身份、协作状态和 agent runtime 的耦合会带来较高设计门槛。
- README 中关于多协议、多形态统一的表述很强，但真正落地时，权限模型、审计链路和错误恢复仍可能非常复杂。
- 框架覆盖面越广，升级和兼容成本越高，尤其是当你同时接入 MCP、A2A、外部 chat runtime 和自定义 UI 时。

## 补充建议

1. 先用它做“单一业务对象 + 单一 action 流”的小应用验证，例如客服回复、日历调度或文档编辑，再考虑扩到复杂 SaaS。
2. 评估时重点看三件事：权限边界是否清晰、状态同步是否可靠、agent 改写 UI/数据后的可审计性是否足够。
3. 如果团队已经有成熟 Web 框架和内部权限体系，优先把 `agent-native` 当“统一 action + agent runtime 层”验证，而不是一开始全量迁移。

## 参考资料

- https://github.com/BuilderIO/agent-native
- https://agent-native.com/
- https://agent-native.com/docs/agent-surfaces
- https://github.com/trending
