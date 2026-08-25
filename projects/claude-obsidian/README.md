<!-- markdownlint-disable MD013 -->

# claude-obsidian

> 上游仓库：[AgriciDaniel/claude-obsidian](https://github.com/AgriciDaniel/claude-obsidian) · 归类：记忆层与个人 AI 基础设施 · 本页基于 2026-08-26 的上游 README、安装材料与 GitHub API 快照整理。

## 定位

`claude-obsidian` 是面向 Claude Code 及兼容 Agent Skills 宿主的 local-first Obsidian 知识系统：将资料留在普通 Markdown/JSON/源文件 vault 中，按来源、主张、链接页、索引与 Canvas 组织，并提供采集、检索、维护和可视化工作流。API 快照为 12,674 stars、1,380 forks、135 个开放 issue，MIT；GitHub Trending 抓取时约 +810 当日 stars。这是短期公开关注度，不证明事实准确、数据不外流或能安全自动修改真实知识库。

## 用法

上游建议把产品 checkout 与个人 vault 分开，初始化先生成计划，再用计划哈希显式批准写入：

```sh
git clone https://github.com/AgriciDaniel/claude-obsidian.git
cd claude-obsidian

python scripts/claude-obsidian.py init "$HOME/Documents/MyKnowledgeVault" \
  --generated-at "$(date -u +%Y-%m-%dT%H:%M:%SZ)" --operation-id init-reviewed

# 审阅 JSON plan 后，将返回的哈希代入并执行
python scripts/claude-obsidian.py init "$HOME/Documents/MyKnowledgeVault" \
  --generated-at "$(date -u +%Y-%m-%dT%H:%M:%SZ)" --operation-id init-reviewed \
  --approved-plan-sha256 "<approved-plan-sha256>" --apply
```

随后在 vault 目录启用本地 plugin，例如 `claude --plugin-dir /absolute/path/to/claude-obsidian`，再调用 `/claude-obsidian:wiki`、`wiki-ingest`、`wiki-query` 或 `save`。对 Codex/OpenCode/Gemini，先预览 `bin/setup-multi-agent.sh --host codex`，确认链接和写入范围后才附加 `--apply`。

## 原理

- 采集时先保留可追溯、内容寻址的来源副本；主张台账记录来源权威性、新鲜度、支持/矛盾、置信度与复核状态。
- 基于这些证据生成相互链接的 Markdown 页面、索引、Maps of Content 与 Obsidian Canvas，并通过查询、lint、维护与 rollup 再利用 vault。
- 并行 worker 返回草稿，由单一 orchestrator 检查后以可恢复事务应用，降低多 agent 同时写入的冲突风险。
- vault 本体并非云数据库或隐藏缓存；是否调用模型、网络工具或第三方插件仍取决于安装与运行配置。

## 价值

- 将“总结一次就丢”的研究流程变成保留原始证据、支持状态与关联笔记的长期知识资产。
- 普通文本文件可用 Obsidian、Git 和常规工具查看或迁移，不必完全依赖特定模型/服务。
- 明确的计划/批准和证据结构，有助于把 agent 写入、研究笔记和检索回答放进可审阅工作流。

## 风险边界

- local-first 并不等于默认离线：模型、网页检索、插件和安装脚本可能产生网络出口；真实 vault 上线前需逐项审计 provider、OAuth、日志和同步配置。
- 来源台账能暴露证据薄弱处，却不保证提取、引用、链接、摘要或回答事实正确；关键结论必须回到原始资料人工核验。
- agent 的写入、整理和链接仍可能误删、错误归类或放大敏感信息；现有 vault 应走非破坏性的 `adopt` 路径并先备份。
- vault 可能含个人、客户或受版权约束材料；可读 Markdown 不赋予上传、训练、共享或再利用权限。

## 补充建议

1. 用复制的 vault 和合成/公开资料先回归导入、来源哈希、链接、Canvas、撤销与冲突处理，再接触真实笔记。
2. 建立“来源—权限—保留期—敏感级别”清单，并把原始资料、可分享笔记与模型上下文分区。
3. 将高风险操作限定为预览后批准：安装脚本、批量重构、外部检索、同步及任何自动应用草稿。
4. 用抽样审查衡量 claim ledger 的引用覆盖、过期率与矛盾处理；不要把结构化字段或图谱可视化误作事实验证。

## 参考资料

- [上游 README / 工作流、安装与限制](https://github.com/AgriciDaniel/claude-obsidian)
- [完整安装指南](https://github.com/AgriciDaniel/claude-obsidian/blob/main/docs/install-guide.md)
- [GitHub API 元数据](https://api.github.com/repos/AgriciDaniel/claude-obsidian)
- [MIT License](https://github.com/AgriciDaniel/claude-obsidian/blob/main/LICENSE)
- [GitHub Trending](https://github.com/trending)
