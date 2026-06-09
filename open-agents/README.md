# Open Agents

- GitHub: https://github.com/vercel-labs/open-agents
- 官网: https://open-agents.dev
- 记录日期: 2026-04-16 (Asia/Shanghai)

## 这是什么

Open Agents 是 Vercel 开源的「云端编码 Agent 参考实现」，目标不是只给一个聊天机器人，而是给一整套可 fork 的工程模板：

- Web 端会话与流式 UI
- 持久化工作流驱动的 Agent 执行
- 可休眠/恢复的沙箱 VM（文件系统、终端、git、预览端口）
- GitHub 集成（可选自动提交、推送、创建 PR）

仓库 README 明确强调一个核心架构点：**Agent 不运行在沙箱里**，而是运行在沙箱外，通过工具接口读写文件、执行命令与编排任务。这使 Agent 生命周期与 VM 生命周期解耦。

## 为什么今天值得关注

1. GitHub Trending 和 AI 开源榜单都显示「Coding Agent 工程化」在持续升温。
2. Open Agents 给出的不是“单模型效果演示”，而是一套可部署、可运维、可审计的产品工程骨架。
3. 对团队来说，它降低了“从 Prompt 到真实代码变更”这条链路的搭建成本。

## 怎么用（最短可运行路径）

## 路径 A：本地跑起来（开发验证）

1. 克隆仓库并安装依赖：

```bash
bun install
```

2. 复制环境变量模板：

```bash
cp apps/web/.env.example apps/web/.env
```

3. 填入最小必需项（README 中给出的硬要求）：

- `POSTGRES_URL`
- `JWE_SECRET`

4. 启动：

```bash
bun run web
```

## 路径 B：部署到 Vercel（生产路径）

1. fork 仓库并导入 Vercel。
2. 准备 PostgreSQL。
3. 生成密钥并配置：`JWE_SECRET`、`ENCRYPTION_KEY`。
4. 配置 Vercel OAuth（否则登录不可用）。
5. 需要 GitHub 私仓克隆/推送/PR 时，再配置 GitHub App 相关环境变量。

## 路径 C：把它当“公司内部 Agent 平台模板”

适合：

- 你想要受控沙箱与审计能力
- 你需要把 Agent 执行变成持久化工作流，而不是一次 HTTP 请求
- 你希望把模型层和执行层分离，后续可替换模型或沙箱实现

## 原理拆解（工程视角）

1. 三层架构
- `Web -> Agent workflow -> Sandbox VM`
- Web 层负责会话和流式交互。
- Workflow 层负责持久执行、断点续跑、取消。
- Sandbox 层负责真实代码操作环境。

2. 关键解耦
- Agent 在沙箱外，避免“业务控制平面”被 VM 绑定。
- 沙箱可单独休眠/恢复，节省成本并支持长任务。

3. 可恢复执行
- 每轮 Agent 可以跨多个持久步骤继续。
- 前端重连后可恢复已有运行流。

4. 工具化执行
- Agent 通过 file/search/shell/web/task/skill 等工具操控项目。
- 这使运行记录天然可追踪，利于审计和复盘。

## 仓库结构（对二开最关键的目录）

- `apps/web`: Next.js Web 应用、鉴权、工作流入口
- `packages/agent`: Agent 本体、工具与技能系统
- `packages/sandbox`: 沙箱抽象与 Vercel 沙箱集成
- `packages/shared`: 共享工具库

## 能力边界与风险

## 优势

- 参考实现完整，适合直接 fork 改造成内部产品
- 工作流持久化 + 沙箱隔离，工程可用性高
- 与 GitHub 流程天然衔接，便于接入团队开发范式

## 风险/成本

- 依赖项多（数据库、OAuth、GitHub App、密钥管理）
- 若要大规模并发，沙箱成本与资源调度策略是关键
- 自动提交/自动 PR 需要严格权限隔离和审核策略

## 与常见“本地 Agent”方案的差异

- 本地 Agent 常见痛点是任务中断、长任务不可恢复、环境一致性差。
- Open Agents 用“持久工作流 + 云沙箱”换取稳定性与协作能力，更偏团队级基础设施。

## 参考

- https://github.com/vercel-labs/open-agents
- https://open-agents.dev
- https://github.com/trending
- https://ossinsight.io/trending/ai
