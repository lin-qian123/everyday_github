<!-- markdownlint-disable MD013 -->

# research-evidence-agent

- 仓库：[zxxasdfrty/research-evidence-agent](https://github.com/zxxasdfrty/research-evidence-agent)
- 快照：2026-08-09 抓取；GitHub API 显示其创建于 2026-08-08，约 20 stars、1 fork，BSD-3-Clause。数字会随时间变化。
- 分类：RAG、检索与知识处理

## 定位

本地优先的科研证据溯源和主张—证据审计工具。它把原始实验、再处理数据、模型输出/推断和合成示意图区分为四层，并检查 claim ledger 是否以相容类型的证据支持主张。

## 用法

安装开发依赖后可运行 `research-evidence-agent demo --output-dir outputs/demo-bundle` 和 `pytest`。实际项目可用 `scan ./my-study --output manifest.json` 生成清单，再以 `audit manifest.json claims.json` 审计主张。可选的 OpenAI Agents SDK 层需另装 extra、设置 key 与模型；默认只暴露聚合计数和问题代码。

## 原理

确定性核心对文件生成 SHA-256 manifest，按可审阅路径规则分类、标记未分类或疑似敏感文件，并按主张类型验证证据层级；例如 observation 缺少 raw evidence 会失败，模型输出不能悄然改写成观测。可选模型只组织风险报告，哈希、分类和校验仍由确定性代码控制。

## 价值

它可在论文、报告或数据包发布前把“直接观测、推断、再处理结果、示意图”混淆显式化，并把机器可读的告警接入 CI。默认不发送文件内容或单个文件名的边界，适合先做本地预检。

## 风险边界

清单和类型一致性不能证明实验正确、模型有效、因果成立或数据可合法再分发。路径规则和敏感文件启发式也可能漏报或误报；启用可选 AI 后仍要审查其 provider 的数据、密钥与保留边界。

## 补充建议

先用小型公开 bundle 检验分类规则和 claim schema，再把 manifest、ledger 与 CI 输出纳入版本控制。将每条关键 claim 交由领域研究者审核，并以机构数据治理、伦理和许可审查补足该工具没有覆盖的合规判断。

## 参考资料

- [项目 README](https://github.com/zxxasdfrty/research-evidence-agent)
- [Agent 边界说明](https://github.com/zxxasdfrty/research-evidence-agent/blob/main/docs/agent-boundary.md)
- [GitHub API 元数据快照](https://api.github.com/repos/zxxasdfrty/research-evidence-agent)
