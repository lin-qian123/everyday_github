# agent-toolkit-for-aws（aws/agent-toolkit-for-aws）

- GitHub: https://github.com/aws/agent-toolkit-for-aws
- 文档: https://docs.aws.amazon.com/agent-toolkit/latest/userguide/
- 记录日期: 2026-06-24 (Asia/Shanghai)

## 定位

`agent-toolkit-for-aws` 是 AWS 官方维护的 agent 工具包，目标不是再做一个通用 agent 框架，而是把 AWS 上云开发、部署、数据分析、DevSecOps 与 MCP 接入能力打包成一组可直接被 Claude Code、Codex、Cursor、Kiro 等工具消费的插件、skills 与服务器配置。

## 热度信号

1. GitHub API 在 2026-06-24 抓取时显示约 `973 stars`、`100 forks`，`updated_at` 为 `2026-06-23T23:05:37Z`。
2. GitHub Trending Python 日榜在 2026-06-24 抓取时显示该项目进入榜单，约 `18 stars today`。
3. 官方 README 明确把定位写成 `Official, AWS-supported MCP servers, skills, and plugins to help AI agents build on AWS`，并直接列出 Claude Code、Codex、Cursor、Kiro 的接入方式。

## 用法

### 1) 在 Codex 中接入 AWS 插件市场

README 给出的入口是：

```bash
codex plugin marketplace add aws/agent-toolkit-for-aws
```

之后在 Codex 里通过 `/plugins` 浏览并安装 `aws-core`。

### 2) 在 Claude Code 中安装官方插件

README 推荐先从 `claude-plugins-official` 安装：

```bash
/plugin install aws-core@claude-plugins-official
/plugin install aws-agents@claude-plugins-official
/plugin install aws-data-analytics@claude-plugins-official
```

如果需要 DevSecOps 套件，还可以额外安装 `aws-agents-for-devsecops`。

### 3) 在 Kiro / 其他 MCP 客户端里挂 AWS MCP Server

README 提供了基于 `uvx mcp-proxy-for-aws` 的配置示例，并建议固定版本号以保证可复现性与供应链稳定性。

## 原理

1. 项目把 AWS 能力拆成多层入口：插件市场、MCP server、skills、用户指南，而不是只给一个 SDK。
2. `aws-core` 更像“通用 AWS 开发底座”，覆盖服务选择、CDK/CloudFormation、容器、存储、observability 与部署。
3. `aws-agents` 和 `aws-data-analytics` 则分别把 Bedrock / AgentCore 工作流，以及 S3 Tables、Glue、Athena 等数据链路，封装成更垂直的 agent 能力包。
4. 对 MCP 客户端而言，它的价值在于把“模型会写 AWS 代码”进一步推进成“agent 能在真实云环境里更安全地检索文档、调用服务并遵守 guardrails”。

## 价值

- 对已经把开发流程迁到 Claude Code、Codex、Cursor 这类工具的团队，这个仓库明显降低了 AWS 接入的整理成本。
- 它代表了一个更值得注意的趋势：云厂商开始直接为 agent 生态提供官方插件、skills 和 MCP 配置，而不是只停留在 API 文档层。
- 如果你关注 agent 工具生态，这类官方仓库通常比社区脚本更有长期可维护性和企业采用机会。

## 风险边界

- 它主要解决的是“如何把 agent 接进 AWS”，并不自动解决权限最小化、账单控制、审计追踪和生产变更审批。
- README 已明确提醒要固定 `mcp-proxy-for-aws` 版本；不做版本钉住时，供应链和行为漂移风险会更高。
- 很多能力都要求本地已有 AWS 账户和凭证配置，文档检索可以无状态开始，但真实资源操作不能忽略账号治理。

## 补充建议

1. 落地前先把插件拆成只读文档检索、开发环境试运行、生产环境受控执行三层，不要让 agent 一上来就拿全权限。
2. 如果仓库里已经在用 `claude-plugins-official`、`postman-mcp-server`、`chrome-devtools-mcp` 这类工具生态项目，可以把它视作云侧配套层，而不是孤立的新框架。
3. 评估重点应放在权限模型、错误可解释性、部署回滚链路和成本可见性，而不是只看它能否生成 CloudFormation/CDK 片段。

## 参考资料

- https://github.com/aws/agent-toolkit-for-aws
- https://docs.aws.amazon.com/agent-toolkit/latest/userguide/
- https://github.com/trending/python?since=daily
