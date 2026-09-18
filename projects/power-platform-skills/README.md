<!-- markdownlint-disable MD013 MD034 -->

# power-platform-skills：微软 Power Platform 的官方 Agent 插件市场

> 上游仓库：https://github.com/microsoft/power-platform-skills · 归类：办公、商业与行业应用 · 本页基于 2026-09-19 的 README、各插件说明、telemetry 文档、LICENSE 与 REST API 静态整理；未登录 Azure / Dataverse、未部署应用或运行 cloud flow。

## 定位

`power-platform-skills` 是微软为 Claude Code 与 GitHub Copilot CLI 提供的 Power Platform 插件市场，覆盖 Power Pages、model-driven apps、MCP Apps、Code Apps、移动应用、Canvas Apps 与 Power Automate。它把 PAC CLI、Azure CLI、Dataverse、Canvas Authoring MCP 和 FlowAgent 等真实企业开发面包装为 skills、agents 与 commands。

2026-09-19 的 GitHub 官方 JavaScript Trending 抓取显示约 `+11 stars today`；REST API 快照为 `895 stars / 182 forks / 135 open issues`，MIT。当前无 GitHub Release，插件版本由各自 `.plugin/plugin.json` 管理。

## 用法

快速安装器会安装 PAC CLI、检测 Claude Code / Copilot CLI、注册 marketplace、安装全部插件并启用自动更新：

```sh
curl -fsSL https://raw.githubusercontent.com/microsoft/power-platform-skills/main/scripts/install.js | node
```

更可控的做法是在宿主内手工添加 marketplace，再只安装需要的插件，例如 `power-pages`、`model-apps`、`mcp-apps` 或 `power-automate`。Canvas Apps 需要 .NET 10 SDK；Power Automate 还需要 Node.js 18+、`az login` 与 MCP bundle。

## 原理

- marketplace manifest 指向多个 plugin，每个 plugin 独立声明 skills、agents、commands、版本、license 与关键词。
- Power Pages / Code Apps 生成 React、Vue、Angular、Astro 或 Vite 项目，再通过 PAC CLI 部署到 Power Platform。
- Model Apps 操作 Dataverse 表、关系、表单、视图、图表、安全角色与 sitemap；Canvas Apps 使用 Canvas Authoring MCP 写 `.pa.yaml`。
- MCP Apps 生成 codeful tool runtime、JSON Schema、MCP annotations、structured output 和可嵌入 widget。
- Power Automate 通过 FlowAgent MCP 构建、编辑、运行和调试 cloud flow，需要 Azure 身份与真实租户权限。
- telemetry 状态并不统一：README 说明 Power Pages 默认开启 1DS，可能包含 Dataverse organization、Entra tenant GUID 与用户 object ID；Model Apps 当前 hard-disabled。

## 价值

- 把 Power Platform 的多套 CLI、schema 和部署规则沉淀为官方可复用 workflow，降低 Agent 生成企业应用的上下文门槛。
- 覆盖网页、模型驱动、Canvas、移动端、MCP App 与自动化流，能在同一仓库比较不同 Power Platform 开发面。
- 官方插件提供样例、references、AGENTS 和验证步骤，适合团队在其上叠加自己的租户治理规则。
- MIT 许可和手工安装路径允许只引入需要的插件，而非强制采用全部 marketplace。

## 风险边界

- skills 可执行 `pac`、`az`、Node、文件写入与真实租户部署；README 中的 `--dangerously-skip-permissions` / `--allow-all-tools` 只是便捷选项，不是安全建议。
- 快速安装器会拉取并执行远程 JavaScript、安装 PAC CLI、全部插件并启用自动更新，供应链与权限面显著大于手工单插件安装。
- Power Pages telemetry 默认开启，opt-out 只停止传输，本地 diagnostic mirror 仍会写入；organization / tenant / user 标识应按企业数据治理处理。
- Agent 生成的 table、security role、flow、connector 与 deployment 可能影响真实数据和业务流程；语法成功不等于权限、合规或业务逻辑正确。
- repo 统一 MIT 不自动覆盖平台服务条款、connector 数据、第三方模板、租户 license 与商标使用。
- 本页未验证插件版本矩阵、回滚、自动更新、telemetry 字段、Dataverse 权限、Canvas MCP 或 FlowAgent 的生产行为。

## 补充建议

1. 使用手工安装和测试 tenant，只安装一个插件；固定 commit / plugin version，禁用自动更新后记录全部配置写入。
2. 为 `pac`、`az`、MCP 和 shell 建精确 allowlist，禁止全工具自动批准；部署前生成计划并由平台管理员复核。
3. 默认关闭 telemetry transmission，检查本地 mirror、日志和 CI artifact；对 tenant、organization 与 user 标识设定保留和访问策略。
4. 在合成 Dataverse 数据上回归 schema、RBAC、connector、flow retry / idempotency、rollback 和删除，不让 Agent 直接操作生产环境。

## 参考资料

- 上游 README：https://github.com/microsoft/power-platform-skills
- Power Pages 文档：https://learn.microsoft.com/en-us/power-pages/configure/create-code-sites
- PAC CLI 参考：https://learn.microsoft.com/en-us/power-platform/developer/cli/reference
- GitHub REST API：https://api.github.com/repos/microsoft/power-platform-skills
- LICENSE：https://github.com/microsoft/power-platform-skills/blob/main/LICENSE
- Telemetry 说明：https://github.com/microsoft/power-platform-skills/blob/main/shared/telemetry/README.md
