# exxperts

<!-- markdownlint-disable MD013 -->

## 定位

`exxperts` 是 EXXETA 开源的本地优先 AI rooms / memory runtime。它主打“受治理的持久记忆”：每个 room 像一个长期 AI 同事，记住任务、决策、知识库和产物，但记忆写入需要用户审批，数据默认保存在本机。

截至 2026-07-13，GitHub API 显示该仓库约 140 stars、11 forks，创建于 2026-07-07，许可证标识为 PolyForm Noncommercial。它更像本地 agent 工作台，而不是普通聊天 UI。

## 用法

安装并构建：

```bash
git clone https://github.com/EXXETA/exxperts.git
cd exxperts
npm install
npm run install:global
```

启动 Web 工作台：

```bash
exxperts web
```

在项目目录中使用 CLI / TUI：

```bash
cd /path/to/project
exxperts cli
```

## 原理

exxperts 把 room、memory、knowledge base、artifacts、usage wallet 和 MCP connectors 放在本地文件系统里。Web app 和 CLI 共享同一套 rooms 与凭据状态；room 可使用知识库、Web research、MCP connector 等工具，但不是无限制 shell。

最关键的设计是 approval-gated memory：AI 提议要记住什么，用户审批后才写入长期记忆。

## 价值

- 明确解决“agent 静默写画像”和“长期记忆不可审计”的问题。
- 对个人长期项目、家庭事务、产品发布、求职、旅行等多上下文场景有实际形态。
- 本地文件可备份、删除和审查，比黑盒 SaaS 记忆更容易治理。
- 和 `openwiki`、`brain0`、`ditto` 一起代表 agent memory 从会话摘要走向可治理基础设施。

## 风险边界

- PolyForm Noncommercial 许可证限制商业使用，需要明确评估。
- 本地优先不等于完全离线，模型 provider、Web research、MCP connector 仍可能产生外部网络访问。
- 长期 memory 可能保存敏感个人信息，备份和同步策略必须谨慎。
- 早期项目，room permission、connector 安全和迁移格式还需要持续验证。

## 补充建议

- 适合先作为个人 knowledge room / project room 试用，不宜直接替代企业知识库。
- 部署前应检查 `~/.exxperts` 的目录结构、日志、凭据保存方式和备份策略。
- 重点跟踪它是否把 memory proposal、approval、diff 和审计记录做得足够稳定。

## 参考资料

- GitHub 仓库：<https://github.com/EXXETA/exxperts>
- Trendshift 热度页：<https://trendshift.io/repositories/80701>
- 项目背景文章：<https://www.linkedin.com/pulse/memory-model-isnt-allowed-write-andr%C3%A9-lindenberg-mqjse>
