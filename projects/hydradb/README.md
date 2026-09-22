<!-- markdownlint-disable MD013 -->

# hydradb（hydra-db/hydradb）

- GitHub：<https://github.com/hydra-db/hydradb>
- 抓取快照：2026-09-23，4,192 stars、1,218 forks、146 open issues
- 热度信号：GitHub Rust Trending 抓取时约 +794 当日 stars
- 版本与许可：AGPL-3.0；GitHub 无正式 Release，tags 有 `v0.1.1` / `v0.1.0`；默认分支最后 push 为 2026-08-19

## 定位

HydraDB 是以 S3-compatible object storage 为持久层的分布式图数据库，提供 snapshot-consistent OpenCypher、GraphBLAS traversal、Neo4j-compatible Bolt 和 HTTPS API。它把 query / mutation data node 与后台 indexer 拆分，希望让计算节点无状态替换或独立扩缩。

## 用法

本地可拉取 GHCR 镜像或从源码编译，按 README 启动单节点后必须实际写入并查询，不能只看 `/readyz`。生产路径通过 Helm 配置对象存储、TLS、身份认证、网络策略、cache volume、data node 和 indexer；客户端可使用 Neo4j driver、typed JSON 或 NDJSON API，并在 `causal` / `strong` read consistency 间选择。

## 原理

WAL、manifest、graph record 和 immutable traversal index 放在 object storage；data node 用本地 SSD / NVMe 作可丢弃缓存，indexer 异步生成 CSC index。读取把已发布 index 与可见 WAL tail 合并并固定在同一 SlateDB snapshot；对象存储 CAS lease 与 writer epoch 用于 active writer handoff / stale-writer fencing。

## 价值

对超大图或云原生 workload，存储 / 计算分离可降低迁移数据的扩缩成本；Neo4j Bolt 兼容与 OpenCypher 也降低应用迁移门槛。仓库同时提供 consistency、Jepsen、formal model、bug casebook 和 benchmark 入口，便于继续做证据型审计。

## 风险边界

- Trending 的 +794 只是短期关注信号；默认分支一个多月未 push、无 GitHub Release，仅有 tags，不能据此推断维护节奏或生产成熟度。
- object storage 一致性、lease / fencing、index lag、WAL overlay、cache recovery 和跨区故障是核心正确性边界，需在目标 S3 实现上重跑。
- `causal` 与 `strong` 模式有不同新鲜度 / 成本，应用若误配 bookmark 或 consistency 可能读到不符合业务预期的视图。
- AGPL-3.0 对网络服务部署有源码提供义务；Bolt / OpenCypher 兼容也不代表所有 Neo4j 语义、扩展和运维工具等价。
- 上游 benchmark 与 formal evidence 仍是作者提供材料，本轮未在当前 revision 重跑；README 当前列出的 Jepsen 报告相对链接在默认分支返回 404，属于文档 / 证据漂移。

## 补充建议

锁定 commit、镜像 digest、对象存储实现和故障注入脚本，复测 writer handoff、网络分区、延迟 / 丢失 index、对象存储读后写、节点重启和全量恢复。另以 Neo4j compatibility corpus 对 query / transaction / error 语义做差分，不只比较吞吐。

## 参考资料

- [GitHub 仓库](https://github.com/hydra-db/hydradb)
- [GitHub REST API](https://api.github.com/repos/hydra-db/hydradb)
- [架构说明](https://github.com/hydra-db/hydradb/blob/main/architecture.md)
- [Benchmark 站点](https://hydra-db.github.io/benchmark/)
- [README 文档索引](https://github.com/hydra-db/hydradb#documentation)
- [LICENSE](https://github.com/hydra-db/hydradb/blob/main/LICENSE)
