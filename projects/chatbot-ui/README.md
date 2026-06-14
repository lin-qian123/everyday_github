# chatbot-ui

## 项目定位
`chatbot-ui` 是一个开源 AI 聊天应用前端，目标是为“接多模型、可自托管、可二次开发”的聊天入口提供一套现成界面与后端集成骨架。

- GitHub：https://github.com/mckaywrigley/chatbot-ui
- 官方托管版：https://chatbotui.com
- 记录日期：2026-06-14（Asia/Shanghai）

## 为什么值得关注

- OSSInsight AI Trending（2026-06-14 核对）中，`mckaywrigley/chatbot-ui` 位于 Top 50 第 `32` 位。
- GitHub API 抓取显示约 `33.3k stars`、`9.4k forks`。
- 官方 README 直接把它定义为 `The open-source AI chat app for everyone.`，并明确给出本地与托管部署路线。

它值得建档，不是因为聊天 UI 本身新鲜，而是因为“多模型聊天入口”仍然是很多团队落地 AI 应用的第一层表面：账号、历史记录、模型切换、文件上传、权限和分享都会先在这里碰撞。

## 用法

官方 README 当前给出的本地快速路径是：

```bash
git clone https://github.com/mckaywrigley/chatbot-ui.git
cd chatbot-ui
npm install
supabase start
cp .env.local.example .env.local
npm run chat
```

其中几个关键前提要注意：

1. 数据层默认依赖 `Supabase`，不再只是浏览器本地存储。
2. 本地模型可选接入 `Ollama`。
3. 如果部署托管版，还要执行数据库迁移，例如：

```bash
npm run db-push
```

## 原理

`chatbot-ui` 的核心不在模型，而在“聊天产品壳”：

1. 交互层
   提供多模型聊天界面、会话历史、配置入口和可托管前端。

2. 状态与数据层
   官方 README 说明 2.0 版本把数据管理转到 Supabase/Postgres，解决本地存储在安全性、多模态扩展和容量上的限制。

3. 模型接入层
   它不是单一模型产品，而是一个可接多模型、多后端的通用聊天入口。

## 价值

- 适合需要快速做“可自托管聊天产品”原型的团队。
- 比从零写聊天界面更快，尤其适合作为内部工具、演示环境或客户 PoC。
- 对前端工程师来说，它提供了一个观察“AI 应用壳层”怎么组织的现成样本。

## 风险边界

- 热门聊天前端不等于差异化产品；很多价值最后仍取决于后端模型、权限体系和业务工作流。
- 默认依赖 Supabase，意味着自托管时要接受数据库、存储和认证的额外复杂度。
- 如果没有额外的组织级约束，聊天壳很容易变成“大家都能跑，但谁都离不开人工维护”的中间层。
- 安全边界、审计、租户隔离和敏感信息处理，不能因为它是 UI 项目就被忽略。

## 补充建议

- 更适合作为“内部 AI 门户”或“多模型聊天前端骨架”来评估，而不是直接当成熟平台。
- 选型时要重点看它与你现有认证系统、知识库、模型网关和部署平台的接缝成本。
- 如果团队真正要做 agent-native 产品，不能只停留在聊天框，还要继续补工具调用、结构化输出和任务流。

## 参考资料

- https://github.com/mckaywrigley/chatbot-ui
- https://chatbotui.com
- https://ossinsight.io/trending/ai
