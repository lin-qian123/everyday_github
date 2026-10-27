<!-- markdownlint-disable MD013 -->

# Auto Ontology：给数据查询补上业务语义与来源

- 主上游：[NVIDIA/auto-ontology](https://github.com/NVIDIA/auto-ontology)；repository ID `1222953295`。
- 采样日期：2026-10-28（Asia/Shanghai）；分类：RAG、检索与知识处理。
- API 累计快照：333 stars / 44 forks / 28 open issues（含 PR 口径），与榜单日增分开。
- 默认分支 `main`；主线依据固定在 `eb8dd0621d07db3033fe3fddc68f62ff72614610`。发行 API 本轮返回空列表；此状态不代表没有源码标签或其他分发渠道。
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

Web 默认 3000，后端 3001，另有 ingestion、Postgres、pgAdmin。先调整宿主端口绑定与网络，再导入合成表、核对业务术语、提问并追溯 SQL；本轮没有部署或查询真实数据。脚本 API token 可设过期时间，未设置时默认永不过期，权限跟随 token 所属用户。

## 原理

Next.js / Better Auth 处理前端与身份，FastAPI 处理目录、检索和 NL-to-SQL，Postgres / pgvector 保存应用元数据、ontology 与向量。模型角色用 endpoint / key / model 三元组配置，未填字段会回退到共享默认值；ingest 与 query 的 embedding 模型必须一致。框架把检索到的定义与关系送入推理，再执行连接库查询，供使用者检查来源。

## 价值

适合跨库同名指标、口径不一致和复杂表关系的分析系统；可将“模型猜测含义”转为可审阅、可修订的语义资产。存在 catalog、lineage 或验证步骤，并不保证每条 SQL 的业务含义正确；收益需与没有语义层的基线比较。

## 风险边界

- README 明确：UI 新建连接在没有 Vault 时，把含口令的完整连接对象以明文 JSON 存入 Postgres。Vault 必须同时具备 `VAULT_ADDR`、`VAULT_NAMESPACE`、`VAULT_ROLE_ID`、`VAULT_SECRET_ID`；当前实现对部分配置发警告后按未加密处理。
- Compose 多个端口未限定到 loopback，pgAdmin 也被映射；Web 登录不能替代数据库、后端和网络边界。部署前逐个核对公开面及示例口令。
- 自托管 Web 不代表模型输入不离开内网；元数据、问题、检索内容与查询结果的发送范围应按所选模型和代码路径审计。
- API token 默认无期限且继承用户角色，应显式限时、轮换，并使用数据库只读账号、查询超时和结果量限制；不能仅依赖模型生成的 SQL。
- Apache-2.0，第三方组件另列 notices；README 当前声明不接受外部贡献。本轮未重现 text-to-SQL benchmark，不能引用品牌或 benchmark 入口证明本地准确率。

## 补充建议

先做一个包含同名字段、时间口径差异与错误定义的小型验收集，保存术语审批记录、期望 SQL / 结果、实际 SQL / 结果和来源。凭据存储、模型出口、查询权限与语义准确率分别验收，再扩大数据范围。

## 参考资料

- [README.md](https://github.com/NVIDIA/auto-ontology/blob/eb8dd0621d07db3033fe3fddc68f62ff72614610/README.md)。
- [.env.example](https://github.com/NVIDIA/auto-ontology/blob/eb8dd0621d07db3033fe3fddc68f62ff72614610/.env.example)。
- [docker-compose.yml](https://github.com/NVIDIA/auto-ontology/blob/eb8dd0621d07db3033fe3fddc68f62ff72614610/docker-compose.yml)。
- [LICENSE](https://github.com/NVIDIA/auto-ontology/blob/eb8dd0621d07db3033fe3fddc68f62ff72614610/LICENSE)。
- [auto_ontology/connectors/vault.py](https://github.com/NVIDIA/auto-ontology/blob/eb8dd0621d07db3033fe3fddc68f62ff72614610/auto_ontology/connectors/vault.py)。
- [auto_ontology/connectors/base.py](https://github.com/NVIDIA/auto-ontology/blob/eb8dd0621d07db3033fe3fddc68f62ff72614610/auto_ontology/connectors/base.py)。
- [仓库 API](https://api.github.com/repos/NVIDIA/auto-ontology)、[发行 API](https://api.github.com/repos/NVIDIA/auto-ontology/releases?per_page=1)；动态字段只代表本轮采样。
- 事实依据为以上一手材料；价值、风险推论与补充建议为本库工程分析。
