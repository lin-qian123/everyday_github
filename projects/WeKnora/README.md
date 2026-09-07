<!-- markdownlint-disable MD013 MD034 -->

# WeKnora（Tencent/WeKnora）

> 记录日期：2026-09-08（Asia/Shanghai）。本页依据上游 README、CHANGELOG、release、LICENSE 与 GitHub REST API 做静态整理；本轮未部署 Docker / Kubernetes、未导入文档、未连接模型或 IM，也未验证 RAG、权限、加密、sandbox 或评测指标。

## 定位

`WeKnora` 是腾讯开源的 LLM 知识平台，将文档解析、混合检索、RAG 问答、ReACT agent、自动 Wiki、长期记忆、MCP / skills、Web 搜索与多租户工作区合到一套 Web / API / CLI 系统。它既可本地或私有云部署，也能连接大量模型、向量库、对象存储、IM 和企业内容源。

2026-09-08 的 GitHub Go Trending 抓取显示约 `+156 stars today`；REST API 快照为 `21,693 stars / 3,143 forks / 674 open issues`，最新 release 为 `v0.8.0`（2026-09-03）。GitHub API 的许可证字段为 `NOASSERTION`，但仓库 `LICENSE` 明确给主项目 MIT，并列出第三方组件的其他许可证；采用时应读完整清单，而不是把 API 字段或“MIT”二字单独当结论。

## 用法

上游最小 Docker Compose 入口为：

```bash
git clone https://github.com/Tencent/WeKnora.git
cd WeKnora
cp .env.example .env
docker compose pull
docker compose up -d
```

启动后默认访问 `http://localhost`。真实资料入库前应先固定 `v0.8.0`、检查 `.env`、镜像 digest、默认账号、暴露端口与数据卷，只启用一个本地模型、一个解析器和一个测试知识库。

## 原理

- **文档流水线**：支持多格式解析、chunk 编辑 / 版本、parent-child chunk、BM25、dense、GraphRAG、rerank 与多种向量库。
- **Agent 与知识**：ReACT 按轮组合知识检索、Web、MCP 和 skill sandbox；Wiki mode 从资料生成可编辑、可 diff / rollback 的 Markdown 页面。
- **长期记忆**：跨 session 抽取 profile、preference、fact、task、interest，并要求用户确认后供 `search_memory` 使用。
- **可替换基础设施**：模型、embedding、rerank、vector DB、object storage、search、parser 和 IM channel 均可配置多种后端。
- **多租户控制面**：Workspace RBAC、每 KB ownership、审计、scoped API key、queue / concurrency、Langfuse trace 和管理面板组成运营层。
- **v0.8.0 sandbox**：skill 可运行在 session-persistent Docker / E2B / Cube backend，支持网络策略；上游称已移除 local host-process backend，Docker 需要显式启用。

## 价值

- 将知识入库、检索、生成、引用、Wiki 与 agent tool use 放在同一可观察流程，减少多套系统之间的 glue code。
- chunk / Wiki revision、引用抽屉和 RAG stage progress 为“答案从哪里来”提供了更好的人工复核入口。
- 丰富后端与私有部署选项适合做企业数据主权、成本和模型替换的架构比较。
- RBAC、scoped key、审计、queue 和 sandbox 说明项目已覆盖不少生产运维问题，而不只是一个演示聊天框。

## 风险边界

- 功能面非常大，674 个 open issues 也是复杂度信号；README 列出安全能力不等于每个 connector、parser、redirect、tenant 与升级路径都已无漏洞。
- RAG 引用、BLEU / ROUGE、hit rate 或自动 Wiki 不能证明事实完整、推理正确或资料没有 prompt injection。
- SkillHub / git / zip 安装、shell 工具与持久 sandbox 会执行第三方内容；容器 / E2B / Cube 的隔离强度和网络策略需要分后端验证。
- 文档、长期记忆、IM、trace、object storage 与外部模型形成多条数据路径；“local / private cloud”只有在每个 provider 都关闭或受控时才成立。
- `resource_urls=public`、网站 embed、IM 与 scoped API keys 提升集成性，也扩大了配置错误、越权和意外公开的表面。
- API `NOASSERTION` 与仓库复合 LICENSE 表达不同；二进制镜像、模型、解析器和第三方组件仍各有许可证与数据条款。

## 补充建议

- 用两租户、两个知识库和 canary 文档做权限矩阵；覆盖 API、Web、IM、embed、MCP、search、public resource URL 与删除后的 cache。
- 给解析 / 检索建立带页码、表格、OCR、冲突事实和恶意 prompt 的 golden set，分别测 recall、citation、unsupported claim 与成本。
- Skill 默认无网络、只读数据卷和无生产 secret；逐个 backend 做逃逸、跨 tenant、snapshot、恢复和资源上限测试。
- 生产前固定镜像 digest，备份 PostgreSQL / object storage / key encryption material，并实测 v0.7 到 v0.8 的升级与回滚。

## 参考资料

- GitHub 仓库：https://github.com/Tencent/WeKnora
- GitHub REST API：https://api.github.com/repos/Tencent/WeKnora
- 最新 release：https://github.com/Tencent/WeKnora/releases/tag/v0.8.0
- CHANGELOG：https://github.com/Tencent/WeKnora/blob/main/CHANGELOG.md
- Security Notice：https://github.com/Tencent/WeKnora#security-notice
- LICENSE：https://github.com/Tencent/WeKnora/blob/main/LICENSE
