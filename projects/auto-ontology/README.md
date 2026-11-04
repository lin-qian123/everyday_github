<!-- markdownlint-disable MD013 -->

# Auto Ontology：给数据查询补上业务语义与来源

- 主上游：[NVIDIA/auto-ontology](https://github.com/NVIDIA/auto-ontology)；repository ID `1222953295`。
- 采样日期：2026-11-05（Asia/Shanghai）；分类：RAG、检索与知识处理。
- API 累计快照：4,829 stars / 387 forks / 42 open issues（含 PR 口径），综合 daily +2,053，与累计口径分开。
- 默认分支 `main`；主线依据固定在 `2a24f5d34ef6b6e168a7f22d308504d3ab36a198`。发行 API 本轮返回空列表；此状态不代表没有源码标签或其他分发渠道。
- 核验层级：一手文档、元数据和所列部分实现的静态阅读；未安装运行、调用模型、复现基准或验证真实用户效果。

## 定位

Auto Ontology 从企业元数据与既有语义模型构建 ontology / catalog，给 Agent 提供指标定义、实体关系和来源，再通过 Web、CLI、API 与 MCP 接入查询。它是数据语义与 NL-to-SQL 的工程框架，生成的定义仍需领域人员认证。

## 用法

先准备测试数据库、Docker Compose v2 和模型端点。上游默认使用 NVIDIA NIM，可选托管或自托管端点；Python 后端要求 3.12+。在固定源码目录中：

```bash
cp .env.example .env
# 填写数据库、模型端点 / key、AUTH_SECRET 与 APP_URL
docker compose up -d --build
```

Web 默认 3000，后端 3001，ingestion 3002，MCP 3003，另有 Postgres、pgAdmin。先调整宿主端口绑定与网络，再导入合成表、核对业务术语、提问并追溯 SQL；本轮没有部署或查询真实数据。脚本 API token 可设过期时间，未设置时默认永不过期，权限跟随 token 所属用户。MCP 包当前从 GitHub 安装，独立服务以 OAuth 让每个客户端用户登录；公开 MCP origin 必须与 token resource 完全一致。

## 原理

Next.js / Better Auth 处理前端与身份，FastAPI 处理目录、检索和 NL-to-SQL，Postgres / pgvector 保存应用元数据、ontology 与向量。模型角色用 endpoint / key / model 三元组配置，未填字段会回退到共享默认值；ingest 与 query 的 embedding 模型必须一致。框架把检索到的定义与关系送入推理，再执行连接库查询，供使用者检查来源。当前 MCP 暴露只读工具并经前端公共 API 查询；用户角色 / grant 与模型执行结果仍需分别验证。

## 价值

适合跨库同名指标、口径不一致和复杂表关系的分析系统；可将“模型猜测含义”转为可审阅、可修订的语义资产。存在 catalog、lineage 或验证步骤，并不保证每条 SQL 的业务含义正确；收益需与没有语义层的基线比较。

## 风险边界

- 连接文档明确：UI 新建连接在没有 Vault 时，把含口令的完整连接对象以明文 JSON 存入 Postgres。Vault 必须同时具备 `VAULT_ADDR`、`VAULT_NAMESPACE`、`VAULT_ROLE_ID`、`VAULT_SECRET_ID`；当前实现对部分配置发警告后按未加密处理。
- README 明确后端信任前端转发的 `x-auto-ontology-user-id`，ingestion 的 ingest / delete / reset / compile 端点本身无认证，3001 / 3002 必须在私网。Compose 的宿主映射未限定 loopback，pgAdmin 也被映射；部署前限制网络和示例口令，不能只依赖 Web 登录。
- 自托管 Web 不代表模型输入不离开内网；元数据、问题、检索内容与查询结果的发送范围应按所选模型和代码路径审计。
- API token 默认无期限且继承用户角色，应显式限时、轮换。当前文档规定 token 自身不能创建 / 撤销 token；这不代替数据库只读账号、查询超时和结果量限制，也不保证生成 SQL 的业务正确。
- MCP 默认绑定 `0.0.0.0:3003`，OAuth 是用户身份边界，不会自动收窄数据库权限、元数据可见性或外网暴露；本轮没有验证实际部署的授权与工具行为。
- Apache-2.0，第三方组件另列 notices；README 当前声明不接受外部贡献。本轮未重现 text-to-SQL benchmark，不能引用品牌或 benchmark 入口证明本地准确率。

## 补充建议

先做一个包含同名字段、时间口径差异与错误定义的小型验收集，保存术语审批记录、期望 SQL / 结果、实际 SQL / 结果和来源。凭据存储、模型出口、查询权限与语义准确率分别验收，再扩大数据范围。

## 参考资料

- [README.md](https://github.com/NVIDIA/auto-ontology/blob/2a24f5d34ef6b6e168a7f22d308504d3ab36a198/README.md)。
- [.env.example](https://github.com/NVIDIA/auto-ontology/blob/2a24f5d34ef6b6e168a7f22d308504d3ab36a198/.env.example)。
- [docker-compose.yml](https://github.com/NVIDIA/auto-ontology/blob/2a24f5d34ef6b6e168a7f22d308504d3ab36a198/docker-compose.yml)。
- [LICENSE](https://github.com/NVIDIA/auto-ontology/blob/2a24f5d34ef6b6e168a7f22d308504d3ab36a198/LICENSE)。
- [auto_ontology/connectors/vault.py](https://github.com/NVIDIA/auto-ontology/blob/2a24f5d34ef6b6e168a7f22d308504d3ab36a198/auto_ontology/connectors/vault.py)。
- [auto_ontology/connectors/base.py](https://github.com/NVIDIA/auto-ontology/blob/2a24f5d34ef6b6e168a7f22d308504d3ab36a198/auto_ontology/connectors/base.py)。
- [身份、SSO 与 API token](https://github.com/NVIDIA/auto-ontology/blob/2a24f5d34ef6b6e168a7f22d308504d3ab36a198/docs/authentication.md)、[MCP 用户授权](https://github.com/NVIDIA/auto-ontology/blob/2a24f5d34ef6b6e168a7f22d308504d3ab36a198/docs/mcp.md)、[连接凭据](https://github.com/NVIDIA/auto-ontology/blob/2a24f5d34ef6b6e168a7f22d308504d3ab36a198/docs/connections.md)。
- [token 验证实现](https://github.com/NVIDIA/auto-ontology/blob/2a24f5d34ef6b6e168a7f22d308504d3ab36a198/frontend/auth/api-token.ts)、[模型配置回退](https://github.com/NVIDIA/auto-ontology/blob/2a24f5d34ef6b6e168a7f22d308504d3ab36a198/auto_ontology/utils/model_config.py)。
- [仓库 API](https://api.github.com/repos/NVIDIA/auto-ontology)、[发行 API](https://api.github.com/repos/NVIDIA/auto-ontology/releases?per_page=1)；动态字段只代表本轮采样。
- 事实依据为以上一手材料；价值、风险推论与补充建议为本库工程分析。
