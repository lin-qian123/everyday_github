<!-- markdownlint-disable MD013 -->

# Obsidian Mind（breferrari/obsidian-mind）中文解读

> 上游仓库：<https://github.com/breferrari/obsidian-mind> · 归类：记忆层与个人 AI 基础设施 · 本页基于 2026-10-13 的 README、架构、vault manifest、Release、许可证与 GitHub REST API 静态整理；未导入真实工作记录、Slack、Obsidian vault 或本机 Agent 配置。

## 定位

Obsidian Mind 是给 Claude Code、Codex CLI 和 Gemini CLI 使用的 Obsidian vault 模板。它把目标、项目、会议、人员、决策、事故、绩效证据和 session transcript 组织成 Git 可跟踪的 Markdown 图谱，并用 hooks、commands、subagents、MCP 与 QMD 检索把相关记忆送回后续会话。

## 用法

上游推荐在空目录中用 `shardmind install github:breferrari/obsidian-mind` 安装，也可直接 clone。用户需以该目录作为 Obsidian vault 和 Agent 工作目录；Node.js 22+ 运行 TypeScript hooks，QMD 为可选本地语义检索层。正式迁移前应先复制现有 vault，在样本目录验证升级合并、ignore 规则和各宿主 hook 兼容性。

## 原理

- `AGENTS.md` 和分层目录规定信息归档、链接、更新与会话收尾规则。
- SessionStart 注入 North Star、活跃项目、任务和文件清单；写后 hook 校验 frontmatter / wikilink，PreCompact 备份 transcript，Stop 报告结构漂移。
- QMD 以 BM25、embedding 和 reranker 做按需检索；MCP 暴露 search / recall / remember 等有限入口，而不是把整个 vault 塞入上下文。
- `vault-manifest.json` 区分模板基础设施与用户内容，ShardMind 用三方合并更新模板。

## 价值

- 让跨 session 的工作事实、决策与绩效证据以可读 Markdown 和 Git 历史保存，不绑定单一模型供应商。
- 把自动分类、索引、检索和卫生检查拆成可测试脚本，便于审计上下文从哪里进入模型。
- v10.0.0 同时覆盖 Claude Code、Codex 与 Gemini，适合比较不同宿主对同一 vault 的行为差异。

## 风险边界

- vault 会集中保存人员、会议、事故、Slack、绩效和 transcript 等高敏感信息；Git 可追踪不等于加密、最小权限或删除合规。
- Claude Code mod 与 hooks 以当前用户权限运行，README 明确提示 mod 属于 unsandboxed code；第三方模板升级、MCP 和 QMD 依赖都要按供应链审计。
- QMD 的本地 embedding / reranking 改变检索排序但不证明记忆真实、完整或未过期；自动写笔记也可能固化错误归因。
- 三个宿主的 hook、工作目录和指令长度限制不同；“支持”不能替代真实版本上的启动、压缩、恢复和写后验证。

## 补充建议

- 用不含真实 PII 的复制 vault 先验证安装、升级、重建索引、断开 QMD 和回滚，再迁入正式资料。
- 对 `brain/`、`org/`、session logs 与 MCP 暴露根设置不同的加密、备份、保留期和访问控制。
- 为每条长期记忆保留来源、时间、责任人和复核状态；把 Agent 总结与原始记录分层保存。

## 参考资料

- GitHub 仓库：<https://github.com/breferrari/obsidian-mind>
- GitHub REST API：<https://api.github.com/repos/breferrari/obsidian-mind>
- `v10.0.0` Release：<https://github.com/breferrari/obsidian-mind/releases/tag/v10.0.0>
- 架构说明：<https://github.com/breferrari/obsidian-mind/blob/main/ARCHITECTURE.md>
- Vault manifest：<https://github.com/breferrari/obsidian-mind/blob/main/vault-manifest.json>
- LICENSE：<https://github.com/breferrari/obsidian-mind/blob/main/LICENSE>
