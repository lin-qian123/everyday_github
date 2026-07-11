# eve

<!-- markdownlint-disable MD013 -->

## 定位

`eve` 是 Vercel 发布的 filesystem-first agent framework。它把 agent 的 instructions、tools、skills、channels、schedules 等能力放在约定目录中，让 agent 项目像普通代码库一样被阅读、审查、版本管理和部署。

截至 2026-07-12，GitHub API 显示该仓库约 3429 stars、291 forks，创建于 2026-06-16，许可证为 Apache-2.0。README 将其定位为 “The Framework for Building Agents”，并强调 durable agents 与文件系统作为 authoring interface。

## 用法

创建新 agent：

```bash
npx eve@latest init my-agent
```

加入已有项目：

```bash
cd myapp
npx eve@latest init .
```

典型结构：

```text
agent/
  agent.ts
  instructions.md
  tools/
  skills/
  channels/
  schedules/
```

## 原理

eve 的核心思路是把 agent 运行时拆成可检查的文件：常驻系统提示词在 `instructions.md`，工具是 typed function，skill 是按需加载的过程文档，channel 负责 HTTP / Slack / Discord 等入口，schedule 负责定时任务。

这和“所有逻辑塞进一个 prompt 或 SaaS 控制台”相反，更接近可版本化的应用框架。

## 价值

- 适合团队把 agent 产品做成可审查、可部署、可复用的工程资产。
- 文件布局对 coding agent 友好，Vercel 还把文档随 npm 包分发，便于本地读取。
- 兼顾 tools、skills、channels、schedules，覆盖从聊天机器人到后台任务的常见 agent 形态。
- Vercel 背景让它值得持续观察是否会和前端部署、AI SDK、workflow 平台结合。

## 风险边界

- 仍是新框架，API、目录约定和部署生态可能快速变化。
- filesystem-first 降低黑盒感，但不自动解决权限、沙箱、凭据和审计问题。
- 对简单脚本型 agent 可能过重；对生产 agent 则仍需额外 observability 和测试策略。

## 补充建议

- 与 `flue`、`agent-runtime`、`agent-native` 对比：eve 更强调 Vercel 风格的文件约定和应用框架体验。
- 若团队已有 Next.js / Vercel 技术栈，可优先评估 eve 是否能自然接入部署链路。
- 建议重点跟踪它对 MCP、远程工具、队列和长期状态的后续设计。

## 参考资料

- GitHub 仓库：<https://github.com/vercel/eve>
- 文档：<https://eve.dev/docs>
- Vercel：<https://vercel.com/>
