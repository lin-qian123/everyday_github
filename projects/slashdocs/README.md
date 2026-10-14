<!-- markdownlint-disable MD013 -->

# slashdocs（razorpay/slashdocs）中文解读

> 上游仓库：<https://github.com/razorpay/slashdocs> · 归类：办公、商业与行业应用 · 本页基于 2026-10-15 的 README、self-host / security 入口、Compose、MCP / OAuth 说明、Release、许可证与 GitHub REST API 静态整理；未部署真实组织、上传内部文档或验证浏览器隔离与权限模型。

## 定位

slashdocs 是供人和 Agent 协作审阅 HTML 文档的自托管工作区。Agent 发布报告、规格、仪表盘或图表，人可以对具体文字评论、解决 / 重开讨论，再由 Agent 读取反馈并发布新版本；系统保留不可变版本、分享权限、文件夹、CLI、REST 与远程 MCP。

## 用法

本地试用可执行 `docker compose up`，在 `localhost:8080` 使用开发账号；生产部署需要独立配置 PostgreSQL、S3 兼容存储、OIDC、session secret、app / render 两个主机名和 TLS，并固定镜像版本或 digest。Agent 可用 CLI 登录，也可连接 `/mcp`，通过浏览器 OAuth + PKCE 或专用 service-account bearer token 工作。

## 原理

- 单个自包含 HTML 是文档版本单元，图片可内嵌，评论锚定到正文并随版本保存。
- Go server 同时提供 REST、前端、MCP 和 CLI 下载；PostgreSQL 存元数据 / 评论 / grants / sessions，S3 存不可变 HTML。
- 应用 UI 与文档渲染使用不同 hostname / origin，并在 sandboxed frame 中显示不可信 HTML，避免文档读取登录 cookie。
- OAuth token 短时、绑定 audience；MCP 覆盖文档、版本、评论、分享和既有 service account 管理，但不允许经 MCP 新建 key。

## 价值

- 将长篇 Agent 输出从聊天窗口移到可版本化、可评论的共享对象，适合设计评审、事故报告和决策记录。
- 人类反馈、版本、分享和 Agent 重写在同一对象上闭环，比复制粘贴 Markdown 更容易保留审阅上下文。
- 上游明确列出数据存储、OIDC 与无 telemetry 边界，便于自托管团队做威胁建模。

## 风险边界

- HTML 是主动内容；sandbox iframe 不能弥补错误的同源部署。上游明确要求 app 与 render 使用不同 hostname，只有 scheme / port 不同不足以隔离 cookie。
- Compose 使用 `admin@example.com/password`、固定数据库 / blob / OIDC secret、`:latest` 镜像和开发 Dex，只能用于本地评估。
- MCP / CLI 可创建、读取、更新、评论和分享文档；service-account key、默认 sharing、组织 OIDC 与 token rotation 需要外部最小权限和撤销流程。
- “无 telemetry”只描述 slashdocs 自身；OIDC、Slack、数据库、对象存储、宿主 Agent 与模型 provider 仍有各自日志和数据流。

## 补充建议

- 先用无敏感 HTML 测试脚本、iframe escape、外链、超大 data URL、并发版本冲突和 comment anchoring。
- 生产固定 `v0.2.1` 镜像 digest，替换全部开发 secret，分离 app / render 域和 cookie，并做 CSP、备份、恢复与权限回读。
- 为 Agent service account 单独建身份，默认 private，提交后检查 applied grant；对公开分享和组织外访问设置人工审批。

## 参考资料

- GitHub 仓库：<https://github.com/razorpay/slashdocs>
- GitHub REST API：<https://api.github.com/repos/razorpay/slashdocs>
- `v0.2.1` Release：<https://github.com/razorpay/slashdocs/releases/tag/v0.2.1>
- README / security model：<https://github.com/razorpay/slashdocs/blob/master/README.md>
- Self-hosting：<https://github.com/razorpay/slashdocs/blob/master/docs/self-hosting.md>
- Compose：<https://github.com/razorpay/slashdocs/blob/master/docker-compose.yml>
- SECURITY：<https://github.com/razorpay/slashdocs/blob/master/SECURITY.md>
- LICENSE：<https://github.com/razorpay/slashdocs/blob/master/LICENSE>
