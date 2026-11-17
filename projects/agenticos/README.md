<!-- markdownlint-disable MD013 -->

# agenticos（AgenticOS）

- 上游：[vstorm-co/agenticos](https://github.com/vstorm-co/agenticos)；分类：**办公、商业与行业应用**。
- 核验：2026-11-18（Asia/Shanghai）07 时段；仓库 ID `1318197751`，main `a6d66f650017747cac312c87bf02201d3a66c744`。本页为文档与源码抽样核读，未部署或运行 Agent。
- 热度：官方 Python daily **+42**；[API](https://api.github.com/repos/vstorm-co/agenticos)累计 **406 stars / 72 forks / 58 open issues（含 PR）**，均为采样值。
- 版本：[v1.82.1](https://github.com/vstorm-co/agenticos/releases/tag/v1.82.1)，UTC 2026-11-17 22:29 发布，非预发行；修复 README 开发者链接、Compose 服务名和浏览器健康检查，不等于整个平台在本轮通过验收。

## 定位

面向企业团队的自托管 Agent 平台，把共享聊天、知识库、技能、浏览器、代码执行、MCP、预算和审批放在同一控制台。它建立在 FastAPI、Pydantic AI、PostgreSQL / pgvector、Redis 和 Next.js 上；不是一个新的基础模型。适合需要统一运营多个 Agent、并有人员负责部署与权限维护的团队。[固定 README](https://github.com/vstorm-co/agenticos/blob/a6d66f650017747cac312c87bf02201d3a66c744/README.md)

## 用法

1. 已有组织部署时，先通过组织网址登录；桌面应用也是服务器的客户端。
2. 本地试用需 Docker Compose 与模型来源。README 给出远程脚本安装入口，脚本会询问模型 key、登录和组织信息，拉取镜像并启动服务；先下载核读脚本、确认版本和写入位置，再运行。
3. 先建一个低权限文档问答 Agent，上传无敏感信息的手册，检查引用、拒答和运行记录；随后再增加工具、审批与发布范围。
4. 公司部署按生产指南配置 HTTPS、身份、数据库、vault key 和备份。README 的手动部署示例仍写 `v1.38.2`，不能直接当成本轮 `v1.82.1` 的完整操作清单；升级应对照目标发行版配置和迁移说明。

[安装脚本](https://github.com/vstorm-co/agenticos/blob/a6d66f650017747cac312c87bf02201d3a66c744/scripts/quickstart.sh)会查询最新 release 以取得相应 Compose 文件；脚本地址、发行标签、镜像版本和本机已有部署须一起固定。[部署文档](https://github.com/vstorm-co/agenticos/blob/a6d66f650017747cac312c87bf02201d3a66c744/docs/deploy.md)

## 原理

- **知识处理**：文件或同步来源经过 parser、分块、embedding 后进入 pgvector，查询时检索再生成带引用的回答。PyMuPDF / LiteParse 可本地处理，LlamaParse 是云服务；embedding 与生成模型分别决定数据出口。
- **执行环境**：API 经带 token 的 HTTP 调用 `sandboxd`；Docker socket 在 `sandboxd`，不在 API 或任务容器。容器由宿主 Docker daemon 创建，是同级容器。
- **治理**：角色和资源共享控制谁能用 Agent；敏感工具可等待审批；运行历史记录工具、版本、token 与成本。模型请求前检查预算，但这不是对所有并发支出的原子预留。

机制来自 [README](https://github.com/vstorm-co/agenticos/blob/a6d66f650017747cac312c87bf02201d3a66c744/README.md)、[sandbox](https://github.com/vstorm-co/agenticos/blob/a6d66f650017747cac312c87bf02201d3a66c744/docs/sandbox.md) 与 [governance](https://github.com/vstorm-co/agenticos/blob/a6d66f650017747cac312c87bf02201d3a66c744/docs/governance.md)，不是本轮运行测量。

## 价值

把模型接入、可复用知识和日常运营放进统一对象与记录中，便于组织追踪“谁在何时使用哪个版本、调用什么工具、花了多少”。对多个部门重复建设聊天机器人、缺少审批和观测的场景有参考价值。上游的功能数量、准备好的界面示例及教程不构成客户生产效果或安全认证。

## 风险边界

- **自托管与零外发分开**：模型、embedding、parser、搜索、MCP、聊天渠道和可选 tracing 都可能访问外部服务；逐个核对，不能只看控制台部署位置。[安全与数据流](https://github.com/vstorm-co/agenticos/blob/a6d66f650017747cac312c87bf02201d3a66c744/docs/security.md)
- **随附沙箱并非默认断网**：文档说明两种随附 runtime 都请求网络，常规执行使用 `runc`，gVisor 可另配；`sandboxd` 服务 token 具有相当于宿主 root 的控制能力。开发 Compose 公开数据库 / Redis 端口，文档列有 `postgres/postgres`，生产文件不公开这些端口。不能把本地开发部署复制为多租户生产环境。[隔离范围](https://github.com/vstorm-co/agenticos/blob/a6d66f650017747cac312c87bf02201d3a66c744/docs/sandbox.md)
- **预算有并发窗口**：文档明确并发 run 看不到彼此尚未完成的费用，可共同超出 cap；上下文压缩的模型调用先计费、下一次请求才受超额限制。需要严格支出门槛时须另设队列、供应商额度和并发控制。[预算说明](https://github.com/vstorm-co/agenticos/blob/a6d66f650017747cac312c87bf02201d3a66c744/docs/governance.md)
- **共享 Agent 会借出能力**：源系统 ACL 不会自动逐用户镜像。delegate 在父 Agent 发布时检查引用权限，随后对能运行父 Agent 的人提供能力；发布前应审查绑定知识和委派链。[授权模型](https://github.com/vstorm-co/agenticos/blob/a6d66f650017747cac312c87bf02201d3a66c744/docs/permissions.md)
- **恢复依赖密钥**：备份须包含 vault key；HIPAA profile 是配置检查而非认证，原生 MFA / SAML / SCIM 的缺口须按当前文档评估。Apache-2.0 主许可不替代模型、第三方组件与商标各自条款。

## 补充建议

先用一组带权限差异的任务做小试点：跨部门知识问题、被撤销的工具权限、并发预算耗尽、工具超时、审批后配置变化、数据库与 vault 联合恢复。分别核对答案质量、越权、外发目的地、账单和恢复结果。控制台可操作、doctor 检查通过与完整业务验收应分别记录。

## 参考资料

- [官方 Python daily](https://github.com/trending/python?since=daily)、[仓库 API](https://api.github.com/repos/vstorm-co/agenticos)、[v1.82.1](https://github.com/vstorm-co/agenticos/releases/tag/v1.82.1)。
- [固定 Apache-2.0 许可](https://github.com/vstorm-co/agenticos/blob/a6d66f650017747cac312c87bf02201d3a66c744/LICENSE)。
- 固定 SHA 的安装、部署、沙箱、治理与权限资料见各段；本轮未安装、连接账户、调用模型、上传文档、执行工具或验证容器隔离。
