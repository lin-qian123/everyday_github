# zeromem

- 仓库：[ptaranat/zeromem](https://github.com/ptaranat/zeromem)
- 快照：2026-08-06 抓取；GitHub API 显示其创建于 2026-08-05，约 8 stars、0 forks，MIT。数字会随时间变化。
- 分类：记忆层与个人 AI 基础设施

## 定位

Rust 实现的 Zero-Mem agent memory，声称除最终问答外的记忆操作不调用 LLM、消耗零 token；提供 Rust crate、`zm` CLI、PyO3 Python 模块及 Hermes Agent memory provider。

## 用法

按仓库要求运行 `just test` 做离线测试或 `cargo build --release` 编译；用 `zm --db mem.db ingest turns.jsonl` 写入带 session、speaker、text、timestamp 的记录，之后以 `zm --db mem.db query "..."` 查询。启用默认 fastembed 时首次可能下载约 130 MB 模型；需要纯离线时可使用 `--no-default-features`。

## 原理

原始对话 turn 是唯一记录源；系统在 SQLite 中存 turn 与 embedding cache，并在打开时重建实体-上下文图、时间层级及 BM25/向量索引。查询先形成确定性 profile，再路由、融合图与层级检索、补足邻近证据并可选校准答案；实现自述与论文公式逐项映射。

## 价值

把摘要型“记忆”替换为可回到原始 turn 的检索证据，适合需要控制上下文 token、保留可解释召回路径或希望离线运行的 agent 实验。SQLite 单文件也便于备份和审计。

## 风险边界

“零 token”仅描述该仓库的记忆操作，不包括最终模型回答、嵌入下载、宿主 agent 或其他工具成本；启发式 NER、默认 embedding 和检索融合可能遗漏、误连或放大敏感对话。README 说明这是基于论文的独立 clean-room 实现，本页未复现实验结果。

## 补充建议

先用合成且可删除的会话测试召回精度、跨 session 泄漏、重建耗时和离线模式；将 SQLite 加密、访问控制、保留期限与删除流程作为产品功能，而非只看检索效果。对涉及人事、医疗或凭据的数据默认不入库。

## 参考资料

- [项目 README](https://github.com/ptaranat/zeromem)
- [Zero-Mem 论文](https://arxiv.org/abs/2607.29377)
- [GitHub API 元数据快照](https://api.github.com/repos/ptaranat/zeromem)
