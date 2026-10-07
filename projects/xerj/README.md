<!-- markdownlint-disable MD013 -->

# XERJ（xerj-org/xerj）

> 上游仓库：<https://github.com/xerj-org/xerj> · 归类：RAG、检索与知识处理 · 本页基于 2026-10-08 的 GitHub API、README、security / architecture / benchmark 文档与源码静态整理，未索引私有仓库、运行 reference-coding 实验或连接第三方 reranker。

- 抓取快照：3,107 stars、235 forks、19 open issues。
- 热度信号：GitHub Rust Trending 抓取时约 +185 当日 stars；最后 push 为 2026-10-07。
- 版本与许可：最新 Release / tag `v1.0.0-rc.89`（名称仍为 RC，但 API 未标 prerelease），Apache-2.0；本页固定审计 commit `e260e076ed3a`。

## 定位

XERJ 是本地优先、Elasticsearch API 兼容的搜索与 Agent memory 引擎。`autoindex` 可识别代码、文档、日志、PDF、SQLite、Office 等目录内容，建立 BM25、vector / hybrid 与结构化索引；MCP 和普通 Elasticsearch client 可共享同一 node。

## 用法

优先从源码或校验过的 release 安装，在专用数据目录以默认 auth-on 模式启动，读取首次生成的 admin key 后再执行 `xerj autoindex <allowlisted-folder>`。不要在共享主机照抄 `--insecure`；如需 MCP，先启动 node，再以 `xerj mcp` 通过 stdio 连接，并用只读 / namespace 角色限制工具。

## 原理

Rust engine 对文件做类型嗅探、tree-sitter code split 与数据集推断，建立兼容 Elasticsearch 的 index、query、aggregation、kNN 和 hybrid API。默认 lexical embedding 离线，可选 neural model 下载；`/_memory` 提供 namespace 记忆。HTTP authz middleware 与 engine index guard 双层判定 principal、role、index expression 和 privilege。

## 价值

统一 API 让 Agent 能用 file:line passage、结构化数据和已有 Elasticsearch tooling 取代逐文件读取；单二进制、离线 lexical 模式与 snapshot / restore 对本地部署友好。上游 reference-coding case study 给出明确任务数、token 与 solve rate，比只写“节省 token”更可审查。

## 风险边界

- `--insecure` 关闭 TLS 和 API-key auth；虽然新 node 默认绑定 `127.0.0.1`，所有能到达端口的 caller 都是可读写 / 删除全部 index 和 memory 的 superuser。
- 自动索引可能吸入 `.env`、密钥、客户文档、邮件和第三方代码；skip 规则与目录 allowlist 不应由 Agent 自行扩大。
- 上游 2.7× output-token / 16/16 solve-rate 结论来自 8 个任务、4 种语言、每组 16 次的作者实验，并明确对模型已熟悉的公共库可能中性或有害。
- 可选 Jev rerank 会把候选文本发送给 TypeSafe 服务；分数只用于排序且未良好校准，默认关闭不代表其他配置也无外发。
- Elasticsearch compatibility 是实现覆盖，不是完整替代承诺；RC 版本、1366/1369 conformance 与真实集群、插件、snapshot 一致性仍需差分测试。
- MCP 只代理 node 权限，不额外提供信任；Agent memory、索引删除、sharing、cluster 和 admin API 仍须按 server authz 控制。

## 补充建议

用无密钥 fixture 建立包含 / 排除清单，验证 symlink、gitignored secret、二进制、超大文件和删除行为；对每个 Agent 发只读或 namespace-scoped key。用自己的私有、后训练代码任务做盲测，同时记录检索召回、token、正确率和额外维护成本，不只看作者 token 指标。

## 参考资料

- [GitHub 仓库](https://github.com/xerj-org/xerj)
- [GitHub REST API](https://api.github.com/repos/xerj-org/xerj)
- [Security model](https://github.com/xerj-org/xerj/blob/main/docs/SECURITY_MODEL.md)
- [Architecture](https://github.com/xerj-org/xerj/blob/main/docs/ARCHITECTURE.md)
- [Token usage](https://github.com/xerj-org/xerj/blob/main/docs/TOKEN_USAGE.md)
- [Snapshot and restore](https://github.com/xerj-org/xerj/blob/main/docs/SNAPSHOT_AND_RESTORE.md)
- [Rerank data boundary](https://github.com/xerj-org/xerj/blob/main/docs/RERANK.md)
- [v1.0.0-rc.89 Release](https://github.com/xerj-org/xerj/releases/tag/v1.0.0-rc.89)
