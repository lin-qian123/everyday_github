<!-- markdownlint-disable MD013 -->

# Leviathan（elstongun/leviathan）

> 上游仓库：<https://github.com/elstongun/leviathan> · 归类：RAG、检索与知识处理 · 本页基于 2026-10-06 的 GitHub API、README、benchmark / config / security 文档、Cargo manifest 与 LICENSE 静态整理，未编译二进制、导入真实数据或复跑 1M 记录 benchmark。

- 抓取快照：244 stars、14 forks、0 open issues；仓库创建于 2026-10-05 08:57 UTC。
- 热度信号：GitHub Search 按新建仓库 stars 排序的早期开发者信号；不是 GitHub Trending 或社媒互动量。
- 版本与许可：Apache-2.0；tag 与 Cargo manifest 均为 `v0.1.0` / `0.1.0`，REST API 未返回 latest Release。

## 定位

Leviathan 是面向 Agent 大规模结构化记录检索的本地单二进制工具。它把 JSONL、JSON、CSV / TSV、SQLite 或数据库 CLI 输出映射到一个 SQLite / FTS5 索引，通过 CLI 或只读 stdio MCP 返回少量带引用的结果卡，而不是把整段历史塞进模型上下文。

## 用法

安装 `leviathan-index` 后，先用 `leviathan init` 推断字段映射，再以 `index / upsert / delete` 构建或增量更新索引；查询使用 `search`、`recent`、`resolve`、`get` 与 `describe`。需要 Agent 集成时可复制仓库内 skill，或运行 `leviathan mcp` 暴露四个只读工具。

## 原理

记录流式写入单个 SQLite 文件，文本进入 FTS5；查询先按精确键、名称、包含和模糊规则解析 group，再把 group / filter 作为索引 token 参与一次 BM25 检索，并只解码前 N 条为长度受控的卡片。MCP 查询面以只读方式打开索引，不暴露任意 SQL 或文件访问；索引构建与更新仍是独立写入命令。

## 价值

它针对“某个客户 / 机器过去发生过什么”这类实体历史问题，把结果长度、命中状态、引用和 group 歧义处理做成确定接口。CLI + skill 可以按需加载，避免每个会话都支付完整 MCP schema 与原始历史的上下文成本。

## 风险边界

- 作者的 436-token、99% top-5 与 33 ms 数据来自合成维护日志、单机和一套问题分布；文档明确不测最终 LLM 回答，不能外推到企业语料或语义检索任务。
- 核心是词法 BM25；同义词、跨实体问题、缺失 group、错误字段映射和多语言形态可能降低召回，引用存在也不证明回答正确。
- 索引保存原始展示字段并约为源数据 1.8 倍，必须像源数据库一样做权限、备份、删除和保留治理；“无网络”不等于数据自动加密。
- MCP 查询面只读，但 `index / upsert / delete` 会写文件，`--sql` 也会在本机读取用户指定 SQLite；两类能力不应混在同一高权限 Agent profile。
- 仓库创建不足一天，API 无 latest Release；tag、crate、二进制和源码 commit 的 provenance 需要逐项固定。
- 本轮未做恶意输入、FTS query、资源耗尽、索引损坏恢复或真实隐私数据验证。

## 补充建议

从脱敏小数据集开始，冻结字段映射与 `v0.1.0` 源 commit，建立已知答案的 recall@k / citation correctness 金标；把建索引账号与只读查询账号分离，并加文件权限和磁盘加密。采购前在自身长尾查询、多语言、同义词与跨 group 问题上复跑 benchmark，而不是直接采用作者合成结果。

## 参考资料

- [GitHub 仓库](https://github.com/elstongun/leviathan)
- [GitHub REST API](https://api.github.com/repos/elstongun/leviathan)
- [README 与 Quickstart](https://github.com/elstongun/leviathan/blob/main/README.md)
- [Benchmark 方法与限制](https://github.com/elstongun/leviathan/blob/main/docs/BENCHMARKS.md)
- [字段映射配置](https://github.com/elstongun/leviathan/blob/main/docs/CONFIG.md)
- [Security threat model](https://github.com/elstongun/leviathan/blob/main/SECURITY.md)
- [Cargo manifest](https://github.com/elstongun/leviathan/blob/main/Cargo.toml)
- [`v0.1.0` tag](https://github.com/elstongun/leviathan/releases/tag/v0.1.0)
- [Apache-2.0 LICENSE](https://github.com/elstongun/leviathan/blob/main/LICENSE)
