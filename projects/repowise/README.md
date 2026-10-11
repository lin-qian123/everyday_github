<!-- markdownlint-disable MD013 -->

# Repowise（repowise-dev/repowise）中文解读

> 上游仓库：<https://github.com/repowise-dev/repowise> · 归类：RAG、检索与知识处理 · 本页基于 2026-10-12 的 README、架构、benchmark、telemetry、安全 / 合规文档、Release、许可证与 GitHub REST API 静态整理；未索引用户仓库、连接 MCP host 或复跑作者实验。

## 定位

Repowise 把代码 AST / 调用图、Git 历史、测试 / coverage、文档和架构决策编入本地索引，再通过 CLI、Dashboard 与 MCP 回答“谁调用它、改动会影响什么、应跑哪些测试、哪些代码最危险”等问题。它强调确定性图与历史信号，LLM prose 是可选层。

## 用法

```bash
uv tool install repowise
cd /path/to/repo
repowise init --yes --no-prose
repowise serve
```

`--no-prose` 可在不调用 LLM 的情况下建立 graph、git、health、dead-code 和结构化 wiki；需要模型生成文档、聊天或 decision extraction 时，再按仓库配置 provider。MCP host 可调用任务型工具获取 overview、change risk、code search 与 evidence。

## 原理

- tree-sitter / AST 与语言解析器构造文件、symbol 和 call graph，并给边标 confidence / provenance。
- Git churn、ownership、co-change、bug-fix history 与 coverage 叠加到图上，形成 change risk、health 和 test impact。
- 文档、ADR、注释、commit / PR 与可选 agent transcript 进入 decision / wiki 层。
- 本地索引保存在 `.repowise/`；raw source 由上游称为只在内存解析，但向量、图、元数据和生成文档会持久化。

## 价值

- 让 coding agent 先查询已计算的结构与历史，减少反复 grep、开文件和猜测影响面。
- 将“实测 coverage”与“由图推断 reachability”等证据类型分开，便于审查结论强度。
- 支持 PR risk、doc drift、dead code、ownership、跨仓库契约和 agent 上下文等多种工程入口。

## 风险边界

- call graph、dead code、bug magnet、health score 与 test reachability 都可能因动态语言、反射、生成代码、运行时配置或历史噪声产生误报 / 漏报，不能替代编译、测试和人工审查。
- `.repowise/` 中的 embeddings、图、作者与历史衍生数据仍应按源码同等级保护；“向量不可逆”不是降密依据。
- CLI 默认有可关闭的匿名 telemetry，包含随机 install id、命令 / MCP tool 名称与粗粒度运行信息；正式环境要先核对 payload 和保留策略。
- 开源版为 AGPL-3.0，另有商业功能；作者 benchmark 只证明其公开任务与环境，不构成对任意仓库、语言或 Agent 的通用收益证明。

## 补充建议

- 在无敏感副本上用固定 commit 建索引，抽样核对 call edges、dead-code 高置信项和 impacted tests，再决定是否接入 Agent。
- 把 `.repowise/` 纳入访问控制、备份 / 删除和泄露响应；对 hosted / BYOK / local model 三种模式分别画数据流。
- 将作者 benchmark 与自有任务 A/B 分开记录，统计正确率、检索调用数、token、延迟、人工返工和漏测缺陷。

## 参考资料

- GitHub 仓库：<https://github.com/repowise-dev/repowise>
- GitHub REST API：<https://api.github.com/repos/repowise-dev/repowise>
- `v0.55.0` Release：<https://github.com/repowise-dev/repowise/releases/tag/v0.55.0>
- Benchmarks：<https://github.com/repowise-dev/repowise/blob/main/docs/BENCHMARKS.md>
- 架构：<https://github.com/repowise-dev/repowise/blob/main/docs/architecture/ARCHITECTURE.md>
- Telemetry：<https://github.com/repowise-dev/repowise/blob/main/docs/reference/TELEMETRY.md>
- Security & Compliance：<https://github.com/repowise-dev/repowise/blob/main/docs/business/SECURITY_COMPLIANCE.md>
- LICENSE：<https://github.com/repowise-dev/repowise/blob/main/LICENSE>
