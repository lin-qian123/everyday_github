<!-- markdownlint-disable MD013 -->

# OpenBot

- 主上游：[CopilotKit/OpenBot](https://github.com/CopilotKit/OpenBot)
- 分类：Agent 框架与技能生态。
- 核验日期：2026-10-23（Asia/Shanghai）；主线快照 `bd4dc94943a9`。
- [API](https://api.github.com/repos/CopilotKit/OpenBot) 快照：6,934 stars / 943 forks / 36 open issues；发行列表首项 [v0.2.0](https://github.com/CopilotKit/OpenBot/releases/tag/v0.2.0)（UTC 2026-10-12，正式）。累计值不代表今日增量。

## 定位

OpenBot 是 CopilotKit 的 AI 同事应用：Bot 通过 AG-UI 接入，各自获得浏览器、文件和工具工作环境，产品层提供动作策略、审批、审计、定时任务与多种交互入口。它是需部署的应用栈，不是安装一个 skill 即可获得的隔离保证。[README](https://github.com/CopilotKit/OpenBot/blob/bd4dc94943a9d62aefd05e5e99073ba58919c9c6/README.md)

## 用法

准备 Docker、Bun 1.3+、模型 key 与 CopilotKit Intelligence 项目 / 许可。上游流程从复制 `.env.example`、`bun install`、Intelligence 登录和 `bun scripts/setup-learning.ts` 开始；补齐数据库、凭据加密 key、Intelligence API / WebSocket URL 与项目 key 后运行 `bash scripts/start.sh`，访问 localhost:3010。

新部署应先使用测试账号和公开页面。自托管 Intelligence 也要配置其许可与正确端点，不能仅因 OpenBot 根代码 MIT 就推断全栈无需账号或许可。[配置指南](https://github.com/CopilotKit/OpenBot/blob/bd4dc94943a9d62aefd05e5e99073ba58919c9c6/docs/configuration.md)

## 原理

React/Vite 前端与 Hono API 连接 PostgreSQL、routine worker、Bot 运行器及 computer supervisor；持久线程和记忆由 Intelligence 提供。产品网关解析动作目标、评估策略、写审计后再调用浏览器 / 文件服务。低层 computer 端点另有 token，须保持私有；绕过产品网关的直连不会自动获得相同策略语义。[架构](https://github.com/CopilotKit/OpenBot/blob/bd4dc94943a9d62aefd05e5e99073ba58919c9c6/README.md)

## 价值

适合验证“多个业务助手、可追溯动作、可审批外部工具”的应用形态。AG-UI 降低替换 Agent 实现的耦合；独立浏览器 profile 和持久卷能承接长流程。是否安全省人力，应以实际越权、重复动作和恢复测试衡量。

## 风险边界

- `.env.example` 默认 `OPENBOT_SINGLE_USER=true`，所有请求视为同一管理员且无需登录。共享部署需改为身份提供者配置；浏览器可能持有真实登录状态，示例开发 token / 加密 key 不能用于生产。[认证与默认值](https://github.com/CopilotKit/OpenBot/blob/bd4dc94943a9d62aefd05e5e99073ba58919c9c6/.env.example)
- 每 Bot 一个 computer 不等于默认启用 gVisor 或 Chromium sandbox；这些是另外配置项。模型 key、工具凭据、持久浏览器数据和服务端口需分别治理。
- 自动学习默认开启，但收集与投递需已存在且分配的容器；默认容器可自动识别。暂停 OpenBot Learning 不会移除 Intelligence 中此前绑定线程及已有证据，要停止这些容器的分析还需在 Intelligence 管理。[学习生命周期](https://github.com/CopilotKit/OpenBot/blob/bd4dc94943a9d62aefd05e5e99073ba58919c9c6/docs/automatic-learning.md)
- 桌面版遥测默认开启，需在启动前设置 `COPILOTKIT_TELEMETRY_DISABLED=true` 或 `DO_NOT_TRACK=1` 并重启；该说明针对桌面发行面，不代表所有服务的数据流均被关闭。[桌面遥测](https://github.com/CopilotKit/OpenBot/blob/bd4dc94943a9d62aefd05e5e99073ba58919c9c6/desktop/TELEMETRY.md)

## 补充建议

先测拒绝动作、审批失效、重试幂等、停机恢复与低层端点隔离；以合成线程核学习开关和容器保留行为。固定正式版与主线源码的差异。本轮未部署服务、登录 Intelligence、授予凭据或触发外部动作。

## 参考资料

- [README.md](https://github.com/CopilotKit/OpenBot/blob/bd4dc94943a9d62aefd05e5e99073ba58919c9c6/README.md)（固定 commit）。
- [docs/configuration.md](https://github.com/CopilotKit/OpenBot/blob/bd4dc94943a9d62aefd05e5e99073ba58919c9c6/docs/configuration.md)（固定 commit）。
- [docs/automatic-learning.md](https://github.com/CopilotKit/OpenBot/blob/bd4dc94943a9d62aefd05e5e99073ba58919c9c6/docs/automatic-learning.md)（固定 commit）。
- [.env.example](https://github.com/CopilotKit/OpenBot/blob/bd4dc94943a9d62aefd05e5e99073ba58919c9c6/.env.example)（固定 commit）。
- [desktop/TELEMETRY.md](https://github.com/CopilotKit/OpenBot/blob/bd4dc94943a9d62aefd05e5e99073ba58919c9c6/desktop/TELEMETRY.md)（固定 commit）。
- [正式发行列表](https://github.com/CopilotKit/OpenBot/releases)、[仓库 API](https://api.github.com/repos/CopilotKit/OpenBot)（动态状态）。
