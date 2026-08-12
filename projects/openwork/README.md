<!-- markdownlint-disable MD013 -->

# OpenWork

> 跨 macOS、Windows、Linux 的桌面工作区和远程 MCP 服务，用于在不同 AI agent、团队成员和机器间复用 skills、MCP 连接与已连接服务。

- 上游仓库：[different-ai/openwork](https://github.com/different-ai/openwork)
- 许可证：仓库 API 标为 `NOASSERTION`（非标准 SPDX，须另行审阅实际许可文本与发行条款）
- 本轮快照：2026-08-13，GitHub REST API 约 `21.9k` stars、`2.2k` forks；GitHub Trending 页面当时显示当天约 `916` stars。以上计数会随时间变化。
- 分类：Agent 框架与技能生态

## 定位

OpenWork 自称为 Claude Cowork 与 Codex 的开源替代方案，但其实际重心是“能力分发层”：桌面应用可提供专用工作区，远程 OpenWork MCP 则让 Codex、Claude Code、Cursor 等兼容客户端发现并执行已分配的 skills、插件、MCP 连接、Google Workspace 与 Microsoft 365 能力。其组织控制面 OpenWork Den 提供成员、策略、模型 provider 和能力发布管理。

## 用法

桌面端可从项目下载页安装；若已使用兼容 agent，上游建议让 agent 按其安装指引创建初始 workspace。以 Codex 为例，添加远程 MCP：

```bash
codex mcp add openwork --url https://api.openworklabs.com/mcp/agent
```

客户端会在浏览器中完成登录并选择组织。该 MCP 暴露 `search_capabilities`（查找能力）和 `execute_capability`（执行能力）两个工具。开发者在本地 checkout 中可运行 `pnpm dev`；并行 worktree 应使用 `pnpm dev:worktree`，避免 Electron profile 锁和调试端口冲突。

## 原理

1. 管理者在 Den 中发布/分配 skills、插件、远程 MCP 和业务连接；
2. 兼容 agent 通过远程 MCP 认证，按组织与用户权限发现可用能力；
3. agent 调用 `execute_capability`，由 OpenWork 的服务和策略层转发到相应集成；
4. 桌面端或团队控制面统一承载 workspace、策略和版本限制。

它把“每个 agent 各装一套工具”收敛为可共享的能力目录，但也因此把认证、权限和第三方连接集中到更高价值的控制面。

## 价值

- 让同一套组织能力跨 Codex、Claude Code、Cursor 等客户端复用，减少重复配置。
- 将模型 provider、应用版本、团队/个人连接与能力发布放入统一治理入口。
- 对使用多 worktree 的开发者，README 明确提供隔离的本地开发 profile 路径。

## 风险边界

- 远程 MCP 登录与“执行能力”可能触及邮件、文档和企业服务；接入前应核验 OAuth scope、数据处理地域、审计与撤销流程。
- `search_capabilities` 的结果不代表每项能力都可安全自动执行。写入、发信、外部发布、费用型模型调用应有独立确认门。
- GitHub API 未给出标准 SPDX 许可证；“开源替代”不能替代对仓库 LICENSE、二进制发行、云服务和商业条款的逐项审阅。
- 本地开发说明涉及 Chromium/Electron profile、keychain 与 CDP；调试端口和 mock keychain 仅限隔离开发环境，不能直接沿用到生产设备。

## 补充建议

- 从只读、无敏感数据的测试组织开始，导出并审查每个 capability 的输入、输出、网络目的地和实际权限。
- 建立能力清单：owner、允许的 agent、数据级别、是否写入、是否需人工批准、撤销方式。
- 对 desktop 自动更新、remote MCP 端点与插件版本启用变更审计；在引入业务连接前完成许可证与供应商安全评估。

## 参考资料

- [项目 README：安装、MCP 与控制面说明](https://github.com/different-ai/openwork#readme)
- [OpenWork 文档](https://openworklabs.com/docs)
- [GitHub 仓库元数据](https://api.github.com/repos/different-ai/openwork)
- [GitHub Trending 观察入口](https://github.com/trending)
