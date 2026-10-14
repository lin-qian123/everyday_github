<!-- markdownlint-disable MD013 -->

# Azure Skills Plugin（microsoft/azure-skills）中文解读

> 上游仓库：<https://github.com/microsoft/azure-skills> · 归类：Agent 框架与技能生态 · 本页基于 2026-10-15 的 README、plugin manifest、MCP / telemetry / security 说明、skills 目录、Release、许可证与 GitHub REST API 静态整理；未登录 Azure、加载订阅资源或执行部署、RBAC、Key Vault、短信和成本操作。

## 定位

Azure Skills Plugin 是微软维护的 Azure Agent 插件，将 Azure 工作流 skills、Azure MCP Server 与 Foundry MCP 打包给 Copilot、Claude Code、Codex、Cursor、Gemini 和 JetBrains 等宿主。skills 提供选型与 guardrail，MCP 则以 200+ tools 覆盖 40+ Azure services，能够查询资源、诊断、定价并执行真实部署与管理动作。

## 用法

用户可通过各宿主 marketplace 或 APM 安装，随后用 Azure CLI `az login`、Azure Developer CLI 或 managed identity 认证。更安全的初次验证是使用独立测试订阅、只读 RBAC 和无生产 secret 的 managed identity，只运行资源 inventory / pricing / validate；部署、RBAC、Key Vault、通信和删除类能力另设人工审批。

## 原理

- `SKILL.md` 提供 prepare、validate、deploy、diagnostics、cost、AI、storage、Kusto、messaging、RBAC 等领域流程。
- `.mcp.json` 通过 `npx` 启动 Azure MCP / Foundry MCP，将结构化工具暴露给宿主 Agent。
- plugin hooks 追踪 skill / MCP usage；`AZURE_MCP_COLLECT_TELEMETRY=false` 可关闭 Azure MCP telemetry。
- 同一 payload 为 Claude、Codex、Copilot、Cursor 等宿主提供插件 / marketplace manifest，当前版本 `1.2.92`。

## 价值

- 将通用云建议升级为可执行、可验证的 Azure 工作流，减少 Agent 猜测 CLI 参数和服务组合。
- skills 与 MCP 同包，能让规划、验证、部署和诊断引用同一服务能力层。
- 支持 public、China、US Government cloud 的显式配置，方便多云环境避免端点误连。

## 风险边界

- MCP 能管理资源、部署、读取日志 / 存储 / Key Vault、调整 RBAC，甚至触发通信；宿主自然语言确认不能代替 Azure RBAC、预算、policy 和审批。
- 上游警告 `npx` 继承本机 `.npmrc`；受污染 registry / config 可导致下载并执行恶意代码。必须固定包版本、registry 和制品来源。
- telemetry 默认存在，关闭变量只覆盖 Azure MCP 采集；Azure control-plane、宿主 Agent、CLI、Foundry 与组织审计日志仍分别保留数据。
- 根 README 写 Node.js 18+，内层插件 README 写 Node.js 22+，部署应按具体 payload / release 采用更严格要求并记录漂移。
- 仓库 README 说明内容从 `microsoft/GitHub-Copilot-for-Azure` 自动同步；提交与发布节奏不应仅凭此镜像推断。

## 补充建议

- 创建测试 tenant / subscription 和专用 principal，以 read-only inventory 建 tool allowlist；对 create / update / delete / send 强制 Azure Policy 与外部审批。
- 固定 `v1.2.92`、npm lock / registry、MCP image 或 package hash；检查 `.npmrc`、proxy、hook 与 telemetry 后再运行。
- 用部署前后 resource graph、activity log、cost budget 和 rollback 验收每次 Agent 动作，不把“命令成功”当成架构或合规通过。

## 参考资料

- GitHub 仓库：<https://github.com/microsoft/azure-skills>
- GitHub REST API：<https://api.github.com/repos/microsoft/azure-skills>
- `v1.2.92` Release：<https://github.com/microsoft/azure-skills/releases/tag/v1.2.92>
- 插件 README：<https://github.com/microsoft/azure-skills/blob/main/.github/plugins/azure-skills/README.md>
- Plugin manifest：<https://github.com/microsoft/azure-skills/blob/main/.github/plugins/azure-skills/.plugin/plugin.json>
- Azure MCP 文档：<https://learn.microsoft.com/azure/developer/azure-mcp-server/>
- LICENSE：<https://github.com/microsoft/azure-skills/blob/main/LICENSE>
