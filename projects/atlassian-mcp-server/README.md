<!-- markdownlint-disable MD013 -->

# Atlassian Rovo MCP Server（atlassian/atlassian-mcp-server）

> 上游仓库：<https://github.com/atlassian/atlassian-mcp-server> · 归类：办公、商业与行业应用 · 本页基于 2026-10-09 的 GitHub API、README、MCP / plugin manifest、skills 与安全文档静态整理，未连接 Jira、Confluence、JSM、Bitbucket、Loom 或组织 Teamwork Graph。

- 抓取快照：1,087 stars、139 forks、92 open issues。
- 热度信号：GitHub JavaScript Trending 抓取时约 +1 当日 star；最后 push 为 2026-10-07。
- 版本与许可：GitHub 无 Release / tag；MCP registry manifest 为 `2.0.0`、plugin manifest 为 `1.0.0`，Apache-2.0；本页固定审计 commit `b74220d41142`。

## 定位

这是 Atlassian 官方托管 Rovo MCP Server 的公共配置、文档、manifest 与 skills 仓库。远端服务把 Jira、Confluence、Jira Service Management、Bitbucket、Compass、Loom 及部分 Atlassian platform 数据连接到 ChatGPT、Codex、Claude、Cursor、VS Code 等 MCP client，并支持搜索、读取、创建、更新和受控管理操作。

## 用法

新连接使用 `https://mcp.atlassian.com/v2/mcp`，优先浏览器 OAuth 2.1；headless API token 需管理员显式启用，JSM 目前只支持 token。首次接入先给只读、单项目 / 单 space 权限，核对组织允许的 client 与 IP allowlist；写工具逐组开放，delete / manage Jira 保持关闭，任何 create / update 前回读目标与 snapshot token。

## 原理

client 通过 streamable HTTP 连接 Atlassian 托管 endpoint；服务继承用户已有产品权限和组织策略。v2 只直接暴露少量 primary tools，其余经 discover / execute meta-tool 动态发现，以减少上下文；同一仓库将 endpoint 和 skills 打包为 Agent Plugins、Claude / Cursor plugin、Gemini extension 与 MCP registry manifest。

## 价值

它用一个官方维护的连接面覆盖 issue、文档、服务管理、代码协作、视频和组织图谱，减少第三方 connector 与复制粘贴。v2 的 permission group、动态工具发现、Confluence snapshot token 与 space instruction 能为企业 Agent 提供更明确的读取、编辑和版本边界。

## 风险边界

- MCP server 是 Atlassian 托管服务；公开仓库不包含服务端实现，无法仅凭源码独立审计认证、日志、隔离和运行时更新。
- Agent 使用用户权限行动，OAuth 不是意图验证；prompt injection、tool poisoning 或错误目标仍可能创建 / 修改 Jira、Confluence、Bitbucket 和 Loom 内容。
- Teamwork Graph 可跨 GitHub、CI 等连接器检索数据；实际可见范围取决于 full / limited access、Jira 权限和第三方连接配置。
- v1 / v2 的工具名、参数和编辑契约不同，旧 skill 或缓存 client ID 可能失败或调用错误目标；自动迁移后必须回归。
- API token 是长寿命高价值凭据，JSM 又要求 token；不得交给不可信 client、日志、prompt 或用户级共享配置。
- 组织权限、IP allowlist 和 audit log 是必要控制，但不能替代高影响操作确认、内容 diff、恢复策略和业务审批。

## 补充建议

在测试 site 建假项目、假 page 和低权限用户，分别记录 OAuth / token tool inventory 与审计日志。为 Agent 固定 v2 endpoint 和 reviewed skills commit，默认只读；写操作要求“读取当前对象—展示 diff / parent—人工确认—写入—回读”，delete / manage 独立审批，定期撤销闲置 consent 与 token。

## 参考资料

- [GitHub 仓库](https://github.com/atlassian/atlassian-mcp-server)
- [GitHub REST API](https://api.github.com/repos/atlassian/atlassian-mcp-server)
- [README 与工具边界](https://github.com/atlassian/atlassian-mcp-server/blob/main/README.md)
- [MCP registry manifest](https://github.com/atlassian/atlassian-mcp-server/blob/main/server.json)
- [Plugin manifest](https://github.com/atlassian/atlassian-mcp-server/blob/main/plugin.json)
- [v1 / v2 skills 差异](https://github.com/atlassian/atlassian-mcp-server/blob/main/skills/README.md)
- [安全策略](https://github.com/atlassian/atlassian-mcp-server/blob/main/SECURITY.md)
- [Atlassian 官方入门文档](https://support.atlassian.com/atlassian-rovo-mcp-server/docs/getting-started-with-the-atlassian-remote-mcp-server/)
