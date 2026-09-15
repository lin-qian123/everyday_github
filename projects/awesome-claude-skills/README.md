<!-- markdownlint-disable MD013 MD034 -->

# awesome-claude-skills：跨 Agent 的技能发现与动作目录

> 上游仓库：https://github.com/ComposioHQ/awesome-claude-skills · 归类：Agent 框架与技能生态 · 本页基于 2026-09-16 的 README、目录、内含许可证、GitHub Trending 与 REST API 静态整理；未批量安装或执行任何 skill、plugin 或 MCP 动作。

## 定位

`awesome-claude-skills` 是 Composio 维护的技能目录兼可安装集合。它既链接 Anthropic、社区与第三方仓库中的 skills，也在仓库内提供文档、开发、创意、业务和 SaaS 自动化能力；README 还把 skill、MCP 与 tool 三层的职责分开说明。

2026-09-16 的 GitHub 官方 Python Trending 抓取显示约 `+80 stars today`；REST API 快照为 `75,107 stars / 8,689 forks / 1,461 open issues`，master 最近 push 为 2026-08-10，没有 GitHub Release。当前 checkout 可数到 `864` 个 `SKILL.md`，但这只是文件快照，不等于 864 个经过安全或质量认证的独立能力。

## 用法

优先把仓库当目录阅读，只安装已审计的单个 skill。若试用其 Composio 连接插件，上游示例为：

```sh
git clone https://github.com/ComposioHQ/awesome-claude-skills.git
cd awesome-claude-skills
claude --plugin-dir ./connect-apps-plugin
```

重启 Claude Code 后运行 `/connect-apps:setup`，会要求 Composio API key。对于普通 skill，应跟随其原始仓库的安装说明，并固定来源与 revision，不建议整库全局安装。

## 原理

- Skills 用 `SKILL.md` 描述任务流程、触发条件、步骤和 guardrails，脚本、参考资料与资产按需加载。
- README 将 MCP 视为认证、传输和工具发现层，将 tool 视为具体函数，将 skill 视为编排工作流；三者组合后才可能产生外部动作。
- 仓库内含文档/创意类 skill，也列出大量外部 skill 链接；不同条目的代码、维护者和许可证并不统一。
- “App Automation via Composio” 为 README 所列 78 个 SaaS 类别提供工作流说明，经 Rube MCP 发现工具 schema 并调用 Gmail、GitHub、Slack、支付、CRM 等外部系统。

## 价值

- 为快速增长的 skill 生态提供按用途检索的入口，适合先发现可复用方案，再决定是否自行实现。
- 把只生成文本的说明型 skill 与可产生外部动作的 MCP/tool 组合放在同一视图中，便于做权限分层。
- 目录本身能帮助团队建立重复项、维护状态、来源和许可证清单。
- 单个 skill 可拆开审阅和版本化，适合构建项目级最小能力集。

## 风险边界

- GitHub API 返回 `NOASSERTION`，根目录没有可发现的 LICENSE 文件；README 声称仓库为 Apache-2.0，但同时说明各 skill 可能使用不同许可证，复用前必须逐目录、逐上游核验。
- “curated”“production ready”与 stars 不是安全、正确、维护活跃或供应链可信的证明。
- Composio 连接层可发送邮件、修改 issue、发帖、付款或变更业务对象；API key、OAuth scope、actor identity、审批和事后回读必须由宿主控制。
- 外部链接条目可能改名、转移所有者、被删除或在后续版本加入脚本；只看目录描述无法审计真实执行面。
- 医疗、辅助技术、安全、招聘、金融等领域的自然语言规则不能代替专业判断、合规政策或确定性验证。
- 本页没有运行任何 skill，也没有验证 README 所称规模、跨宿主兼容性或 Composio 审计能力。

## 补充建议

1. 维护允许清单：记录 skill 原始 URL、commit、文件哈希、许可证、脚本入口、网络域名和所需 secrets。
2. 默认按项目安装单个 skill；对含脚本、浏览器、shell、文件删除、消息、支付或部署动作的条目做人工 diff。
3. 将“生成草稿”“读取数据”“外部写入”“不可逆动作”分成权限层，写入前要求预览和显式批准，写入后回读。
4. 定期检查失效链接、所有者转移、schema 漂移和许可证变化，不把目录收录当成持续背书。

## 参考资料

- 上游 README 与目录：https://github.com/ComposioHQ/awesome-claude-skills
- 连接插件：https://github.com/ComposioHQ/awesome-claude-skills/tree/master/connect-apps-plugin
- GitHub REST API：https://api.github.com/repos/ComposioHQ/awesome-claude-skills
- Anthropic skills 上游目录：https://github.com/anthropics/skills
- README 许可证说明：https://github.com/ComposioHQ/awesome-claude-skills#license
