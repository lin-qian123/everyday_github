# agent（Talivia Agent Kit）

## 定位

Talivia Agent Kit 是连接 MCP 客户端与 Talivia 网站/收入分析服务的集成包。其 README 声称可让 Codex、Claude Code、ChatGPT 等 agent 完成追踪器安装、事件接收核验和支付归因接入。截至 2026-08-03 的 GitHub API 快照：项目创建于 2026-08-02，约 71 stars、0 forks，MIT。

## 用法

在已授权的 Talivia 账号中，支持 HTTP MCP 的客户端可添加 `https://talivia.com/mcp` 并走浏览器 OAuth；README 也给出 `npx -y @talivia/agent setup --agent codex`、`checkin` 和本地 stdio MCP 的示例。只应让 agent 修改隔离分支的测试站点；创建网站、连接支付服务商和生产验证均须人工确认。

## 原理

本地包将客户端接到托管 MCP 服务；服务按已批准的网站权限返回框架安装方案、追踪状态和归因就绪度。认证与支付服务连接在浏览器中完成，业务规则留在服务端而非随 npm 包复制。

## 价值

- 将“贴埋点代码”推进为可检查的构建、事件接收和收入归因流程。
- 为多种 MCP 客户端复用同一套网站分析接入面。

## 风险边界

- 它是托管分析服务接入，不等于自托管或独立审计的分析系统；数据处理、账号权限与留存需单独评估。
- 追踪脚本、支付归因和 agent 对仓库的写入都可能影响隐私合规与生产指标；不能凭 agent 的“完成”文字替代真实验收。
- 安全交接不应要求在聊天或 MCP 参数中提交支付密钥，但仍应核验 OAuth 授权范围与撤销路径。

## 补充建议

先在无真实客户数据的预发布站点做一次完整闭环，保存代码 diff、事件样本和撤销测试记录；上线前让隐私、财务与网站负责人分别复核追踪范围和归因口径。

## 参考资料

- GitHub：<https://github.com/talivia-group/agent>
- AI Agent Kit：<https://talivia.com/ai-agent-kit>
- GitHub API 快照：<https://api.github.com/repos/talivia-group/agent>
