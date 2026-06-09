# holaOS

- GitHub: <https://github.com/holaboss-ai/holaOS>
- 官方文档: <https://www.holaos.ai/docs>
- 观察时间: 2026-05-05

## 这是什么

`holaOS` 把“电脑环境”本身做成可与 AI 代理共用的工作空间：
- 人与 agent 共用浏览器、文件和应用上下文；
- 强调长会话连续性（memory/continuity），减少任务状态丢失；
- 以桌面环境 + runtime + API 的方式支持持续自动化工作。

它偏向“Agent Computer / Agent OS”路线，不是单一聊天助手。

## 快速用法

### 1) 一行安装（官方示例）

```bash
curl -fsSL https://raw.githubusercontent.com/holaboss-ai/holaOS/main/scripts/install.sh | bash -s -- --launch
```

### 2) 手动路径（适合可控部署）

```bash
git clone https://github.com/holaboss-ai/holaOS.git
cd holaOS
npm run desktop:install
npm run desktop:prepare-runtime:local
npm run desktop:typecheck
```

### 3) 适合的使用场景

- 需要“长期连续执行”的研究/运营型代理；
- 需要人机协同接管（随时查看、修正、继续跑）；
- 希望把多工具流程收敛到单一环境管理。

## 原理拆解

1. 共享环境模型：人和 agent 在同一 workspace 操作，减少上下文切换。
2. Runtime Harness：把 agent 执行边界固定在可观测运行时中。
3. 记忆与连续性：通过工作空间状态与产物维持长程任务一致性。
4. 应用化接口：通过 runtime API 对工作流进行编排而非一次性对话。

## 我认为有价值的补充

- 核心判断：它试图解决的不是“回答更聪明”，而是“执行更连续”。
- 风险点：
  - 权限与安全治理复杂度明显上升；
  - 团队落地时需要明确隔离策略（账号、网络、文件边界）。
- 引入建议：
  - 先在低风险任务试运行（资料整理、内容流水线）；
  - 再扩展到半自动研发流程（文档生成、测试编排）。

## 参考资料

- 仓库 README（安装与架构入口）: <https://github.com/holaboss-ai/holaOS>
- 官方 docs（workspace、runtime、memory）: <https://www.holaos.ai/docs>
- GitHub Trending（今日趋势参考）: <https://github.com/trending?since=daily>
