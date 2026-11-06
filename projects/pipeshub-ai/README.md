<!-- markdownlint-disable MD013 -->

# pipeshub-ai（PipesHub 企业上下文层）

- 更新：2026-11-07（Asia/Shanghai）；官方 Python daily +76，为读取快照，不是自然日结算。
- GitHub API：4,025 stars / 648 forks / 221 open issues（含 PR）；仓库 ID `944080744`。
- 核读基线：`94eb1712963e459b6dd684e644eb64a09718edad`；仅文档与抽样实现核验，未安装运行或独立评测。

## 定位

PipesHub 将企业文档、聊天、工单和代码接入统一上下文层，提供带引用的搜索、问答、Agent、SDK 与 MCP。上游列出 Slack、Drive、Jira、GitHub、Microsoft 365 等 50+ 连接器，并以用户权限约束检索。适合评估企业知识访问与溯源，连接器数量和权限宣传仍需逐源验收。[README](https://github.com/pipeshub-ai/pipeshub-ai/blob/94eb1712963e459b6dd684e644eb64a09718edad/README.md)

## 用法

最新稳定发行 [v1.0.0](https://github.com/pipeshub-ai/pipeshub-ai/releases/tag/v1.0.0) 于 UTC 2026-10-27 发布。推荐先固定源码 / 镜像，审查安装器，再在专用目录用 Docker Compose v2 部署。官方入口支持先下载阅读：

```bash
curl -fsSL https://get.pipeshub.com/install -o pipeshub-install.sh
less pipeshub-install.sh
```

阅读后再执行安装；这不是本轮已运行的命令。默认交互安装生成 .env / 随机 secrets、拉取镜像并启动服务，浏览器入口为 localhost:3000。独立包装器的 `PIPESHUB_REF` 与安装器 `--version` 分别涉及部署文件和镜像选择，不能只固定其中之一。Slim 首次使用仍下载 embedding，Full 带模型，Eval 是缩减拓扑且无 run_code；不是三者都完全离线。[部署细则](https://github.com/pipeshub-ai/pipeshub-ai/blob/94eb1712963e459b6dd684e644eb64a09718edad/deployment/docker-compose/ADVANCED_DEPLOYMENT.md)

升级到 1.0 时留意 SAML / generic OAuth sign-in 移除、client_credentials 绑定 service account、Helm Qdrant API key 不再有默认值，以及 MCP 默认启用。先用测试账户接一个授权数据源，再创建最小范围 PAT / 应用身份。

## 原理

连接器同步内容与权限，索引链做解析、切块、embedding 与图关系构建；问答 Agent 迭代使用混合搜索、grep、关系导航和全文读取，再生成块级引用。

抽样 `ViewerScopeService` 按 org / viewer / 权限版本缓存 scope；查询不在该层等待图计算，miss 会后台填充并抛出 unavailable，由调用方走旧过滤。版本递增后旧条目不再命中。它说明缓存一致性设计，尚不能证明所有连接器撤权及时或所有读取路径都正确过滤。[权限 scope 实现](https://github.com/pipeshub-ai/pipeshub-ai/blob/94eb1712963e459b6dd684e644eb64a09718edad/backend/python/app/services/permissions/service.py)

## 价值

把分散工具的搜索和上下文收集集中起来，便于记录某条回答究竟基于哪些原始块、哪个用户的授权。与逐应用 MCP 相比，可评估权限一致性、检索召回、引用正确率、索引延迟和调用成本，而非只比较回答流畅度。

README 引述第三方榜单截至 2026-11-03 的名次，也列团队自行运行的 FRAMES、内部工作问题与代码图测试。本轮未重核榜单数据或复现实验，不将其推广为所有企业数据上的效果结论。

## 风险边界

- 自托管不保证模型出口留在企业网络；模型、embedding、解析、网页检索及连接器端点需要分别配置。代码执行工具和 MCP 又增加独立权限面。
- PAT、service account 与用户身份的权限不能混用；需测试分享链接、附件、删除、组成员变更、撤权和缓存失效。
- Python telemetry 总开关未设置时使用 edition 默认，本次源码该默认为 true；`TELEMETRY_COLLECTION_FLAG=false` 关闭该包。KV 的 `enableMetricCollection` 是另一个同意层，不能把总开关开启等同于已发生外发。[总开关](https://github.com/pipeshub-ai/pipeshub-ai/blob/94eb1712963e459b6dd684e644eb64a09718edad/backend/python/app/telemetry/flag.py)、[edition 默认](https://github.com/pipeshub-ai/pipeshub-ai/blob/94eb1712963e459b6dd684e644eb64a09718edad/backend/python/app/edition.py)
- 根代码为 Apache-2.0；模型、依赖与外部服务各有条件。未运行安装器、容器、连接器或真实权限测试，不作安全认证。

## 补充建议

用两个权限不同的测试账户和可公开样本，建立“可见 / 不可见 / 刚撤权”矩阵，核对搜索、全文、引用与 MCP 返回的一致性。固定镜像 digest、源码与 provider / 模型版本，保存引用原文和延迟。生产迁移前备份 .env、索引与数据库，先在副本验证恢复，量化评估 API 费用和 telemetry 数据流。

## 参考资料

- [仓库](https://github.com/pipeshub-ai/pipeshub-ai)、[v1.0.0 发行与迁移说明](https://github.com/pipeshub-ai/pipeshub-ai/releases/tag/v1.0.0)。
- [固定 README](https://github.com/pipeshub-ai/pipeshub-ai/blob/94eb1712963e459b6dd684e644eb64a09718edad/README.md)、[LICENSE](https://github.com/pipeshub-ai/pipeshub-ai/blob/94eb1712963e459b6dd684e644eb64a09718edad/LICENSE)、[部署选项](https://github.com/pipeshub-ai/pipeshub-ai/blob/94eb1712963e459b6dd684e644eb64a09718edad/deployment/docker-compose/ADVANCED_DEPLOYMENT.md)。
- [权限缓存](https://github.com/pipeshub-ai/pipeshub-ai/blob/94eb1712963e459b6dd684e644eb64a09718edad/backend/python/app/services/permissions/service.py)、[telemetry 总开关](https://github.com/pipeshub-ai/pipeshub-ai/blob/94eb1712963e459b6dd684e644eb64a09718edad/backend/python/app/telemetry/flag.py)、[默认设置](https://github.com/pipeshub-ai/pipeshub-ai/blob/94eb1712963e459b6dd684e644eb64a09718edad/backend/python/app/edition.py)。
