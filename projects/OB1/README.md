<!-- markdownlint-disable MD013 -->

# OB1（NateBJones-Projects/OB1）

> 记录日期：2026-09-05（Asia/Shanghai）。本页依据上游 README、setup 文档、LICENSE 与 GitHub API 做静态整理；未连接个人聊天记录、Supabase、MCP 或外部模型。

## 定位

`OB1`（Open Brain）是一套个人知识与 agent 记忆基础设施配方库。它以数据库、向量检索、AI gateway、捕获入口和开放连接协议为核心，让不同 AI 客户端读取同一份可持续积累的个人上下文；仓库同时收录 recipe、primitive、skill、dashboard、integration 与 schema。

2026-09-05 的 GitHub 官方 TypeScript Trending 快照显示约 `+10 stars today`；REST API 快照为 `4,557 stars / 879 forks / 211 open issues`。API 许可证字段为 `NOASSERTION`，仓库实际 `LICENSE.md` 是 `FSL-1.1-MIT`：当前版本限制“Competing Use”，两年后按许可证条款转为 MIT，不应简称为“MIT 开源”。

## 用法

上游建议从 setup guide 建立数据库、AI gateway、Slack capture 与 MCP server，并声称约 45 分钟可完成；也提供让 Cursor、Claude Code 等 agent 辅助配置的路径。建议只用虚构数据完成首轮部署：

1. 建立隔离 Supabase / PostgreSQL 项目与最小权限服务账号。
2. 部署 capture 与 MCP 入口，确认认证、RLS、删除和导出路径。
3. 只导入少量脱敏笔记，记录每条 memory 的来源、时间和用途。
4. 接入一个只读测试客户端，验证召回、误召回、跨用户隔离和审计日志。
5. 再按需要选择 ChatGPT、Perplexity、Obsidian、X、Instagram 等导入 recipe。

## 原理

- **统一存储**：以 PostgreSQL / Supabase 与向量检索保存可跨工具访问的“thoughts”和扩展 schema。
- **MCP / gateway 接入**：不同 AI 客户端通过远程 MCP 或 gateway 查询、写回和使用记忆。
- **捕获渠道**：Slack、Discord、导入脚本和数据导出文件把信息送入同一记忆层。
- **扩展分层**：primitive 提供通用基础能力，recipe 组合流程，integration 接外部系统，schema 增加 provenance / review / relation / recall trace。
- **可选自托管**：除 Supabase 路径外，上游列出 PostgreSQL + pgvector 的 Kubernetes integration。
- **社区贡献模型**：仓库对 recipe、dashboard、skill 和 integration 做结构化收录，并描述自动审查后再由人维护者复核。

## 价值

- 将个人上下文从某个聊天产品的封闭 memory 抽离为可查询、可迁移的基础设施。
- 数据导入、schema、dashboard 和 MCP 连接均有可读实现，便于按需求裁剪。
- provenance、review、use policy 与 recall trace 方向有助于把“记住了”变成可审计记录。
- 适合研究不同 agent 共享长期记忆时的召回、纠错、删除和权限模型。

## 风险边界

- 个人聊天、私信、笔记和社媒导出高度敏感，可能包含第三方信息、密钥、健康、财务或工作数据。
- “一个 brain 给所有 AI”也会放大错误记忆、越权召回和跨工具泄露；共享不是默认安全。
- 向量检索相似不等于事实正确或仍然有效；记忆必须有来源、时间、置信度、生命周期和人工纠错。
- 远程 MCP、Edge Function、Supabase、Slack / Discord 和模型 provider 各自引入认证、日志、数据驻留与费用边界。
- FSL-1.1-MIT 当前限制竞争性商业用途；再分发、托管服务和产品集成需逐条审查许可证。
- 上游约 45 分钟 setup 是宣传性估计，不能替代组织级安全、备份和恢复设计。

## 补充建议

- 先定义数据分类、允许导入来源、保留期、删除 / 导出 SLA、跨用户隔离和模型外发策略。
- memory 记录至少包含 source、captured_at、valid_at、owner、sensitivity、review status 和 superseded_by。
- 使用 canary identities 测 RLS、MCP token、跨租户检索、日志脱敏和管理员访问。
- 将 recall 与 write-back 分权；新 agent 默认只读，并要求高风险写回进入 review queue。
- 定期运行“错误记忆、陈旧记忆、重复记忆、不可追溯记忆”审计，并演练全量导出与恢复。

## 参考资料

- [GitHub 仓库](https://github.com/NateBJones-Projects/OB1)
- [GitHub REST API](https://api.github.com/repos/NateBJones-Projects/OB1)
- [Getting Started](https://github.com/NateBJones-Projects/OB1/blob/main/docs/01-getting-started.md)
- [FSL-1.1-MIT 许可证](https://github.com/NateBJones-Projects/OB1/blob/main/LICENSE.md)
- [上游视频 walkthrough（Vimeo）](https://vimeo.com/1174979042/f883f6489a)
