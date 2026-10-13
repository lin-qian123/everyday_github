<!-- markdownlint-disable MD013 -->

# EdgeQuake（raphaelmansuy/edgequake）中文解读

> 上游仓库：<https://github.com/raphaelmansuy/edgequake> · 归类：RAG、检索与知识处理 · 本页基于 2026-10-14 的 README、架构 / auth / security / benchmark 文档、Release、许可证与 GitHub REST API 静态整理；未上传私有文档、启动数据库、调用模型或复测 GraphRAG 结果。

## 定位

EdgeQuake 是 Rust 实现的 GraphRAG 平台，将文档转成 entity / relationship graph，并组合 pgvector 相似度与 Apache AGE 图遍历生成带来源答案。系统提供单 binary、PostgreSQL、Web UI、REST / SSE、MCP 和多语言 SDK，可连接本地或云端 LLM / embedding provider。

## 用法

快速启动脚本用 Docker 拉起 UI、API 与 PostgreSQL，默认只绑定 `127.0.0.1`；用户上传文档后选择 naive / local / global / hybrid / mix / bypass 查询模式。生产环境必须关闭 dev mode、开启 auth、设置强 JWT / secrets key、显式 CORS 和 TLS proxy；快速启动的 open demo 配置不能原样发布。

## 原理

- 文档切块后由 LLM 抽取 entity / relation，embedding 写入 pgvector，关系写入 Apache AGE。
- 查询阶段组合 keyword、vector search 与 graph walk，再由 LLM 合成引用来源的答案。
- workspace 为模型角色和 provider 分配独立连接；connection key 加密保存并通过 doctor / health 检查可达性和安全 posture。
- 显式 migration、schema replay、tenant isolation、audit 与 ingestion control 面向长期运行和升级。

## 价值

- 用单一 PostgreSQL 同时承载关系、向量与业务数据，简化多存储 GraphRAG 的运维面。
- 文档公开同条件 benchmark，并明确 accuracy 是 statistical tie、evidence recall 仍落后 LightRAG，避免只宣传优势。
- 本地 provider、云 provider、角色拆分与 MCP / SDK 入口较完整，适合搭建可观测 RAG 对照实验。

## 风险边界

- quickstart Compose 默认 `EDGEQUAKE_DEV_MODE=true`、关闭登录；即使只绑定 loopback，也不能在共享主机、隧道或反向代理后假设安全。
- entity / relation 是模型抽取结果，不是原文事实；带 citation 也可能引用不支持结论的 chunk。
- provider key、原文、embedding、graph 与 query log 都可能包含敏感信息；本地部署不代表没有云模型出口。
- README badge 仍显示 0.34.0，而 GitHub 最新 Release 为 0.35.0；镜像、数据库 schema、UI 和 SDK 必须统一固定。

## 补充建议

- 用带 gold relation / answer / citation 的私有 holdout 比较 vector-only、LightRAG 与各 EdgeQuake mode，分开统计 accuracy、evidence recall、延迟和成本。
- 先运行 auth-enabled compose，执行 `edgequake doctor`，再测试跨 workspace query、delete、recovery、备份和 key rotation。
- 保留 raw document、chunk、entity / edge、retrieval trace、answer 与人工复核，使图谱错误可定位和可删除。

## 参考资料

- GitHub 仓库：<https://github.com/raphaelmansuy/edgequake>
- GitHub REST API：<https://api.github.com/repos/raphaelmansuy/edgequake>
- `v0.35.0` Release：<https://github.com/raphaelmansuy/edgequake/releases/tag/v0.35.0>
- Architecture：<https://github.com/raphaelmansuy/edgequake/blob/edgequake-main/docs/architecture/overview.md>
- Auth quickstart：<https://github.com/raphaelmansuy/edgequake/blob/edgequake-main/docs/operations/auth-quickstart.md>
- Benchmark：<https://github.com/raphaelmansuy/edgequake/blob/edgequake-main/docs/comparisons/eq-vs-lightrag-acc-bench.md>
- LICENSE：<https://github.com/raphaelmansuy/edgequake/blob/edgequake-main/LICENSE>
