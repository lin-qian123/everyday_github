<!-- markdownlint-disable MD013 -->

# Postiz：通过 API、Agent 和平台授权管理社媒排程

- 主上游：[gitroomhq/postiz-app](https://github.com/gitroomhq/postiz-app)；repository ID `664013991`。
- 采样日期：2026-10-27（Asia/Shanghai）；分类：办公、商业与行业应用。
- API 累计快照：38,407 stars / 7,454 forks / 222 open issues（含 PR 口径），与榜单日增分开。
- 默认分支 `main`；本页主线静态依据固定在 `a5affe62c74e39c1e7ac960d50d8418b807d532c`。发行 API 首项 [v2.25.3](https://github.com/gitroomhq/postiz-app/releases/tag/v2.25.3)，UTC 2026-10-24T14:16:43Z，正式发行标记。
- 核验层级：读取一手文档、许可、元数据与所列部分实现；未安装运行上游、调用模型或复现实验。

## 定位

Postiz 是社交媒体内容管理系统，覆盖排程、跨平台发布、团队协作与分析，也提供 AI 文案 / 图像 / 视频、Agent、API、MCP 和自动化接入。Postiz Cloud 与自托管开源版是两种部署方式；本页主要介绍当前仓库的自托管实现。

## 用法

从固定发行核对 compose、环境变量与数据库迁移，设置实际前后端 URL、随机 JWT secret、数据库 / Redis、存储，以及各社媒平台应用的 OAuth 回调和许可。AI 功能还需独立模型凭据与预算；只启动应用不代表已取得 Meta、YouTube 或 TikTok 的应用审核。

在审阅并修改 compose 配置后，上游源码入口可用下列命令启动，本轮未执行：

```bash
docker compose -f docker-compose.yaml up -d
```

先使用测试频道建草稿、校验媒体、排程时区和授权，再验证受控发布。Agent / MCP / CLI 接入应明确谁可创建草稿、排程和真正发布；不要把有 API 接口视为默认存在人工审批。

## 原理

pnpm monorepo 使用 Next.js、NestJS、Prisma / PostgreSQL，并结合 Redis 和 Temporal 等服务处理后台工作。平台 adapter 管理授权、发布及统计；模型功能走配置的 provider。外部自动化通过 API、SDK 或 MCP 驱动相同应用能力，因此账号凭据和重试逻辑会影响真实外部状态。

## 价值

适合多渠道内容团队把草稿、排程和分析集中管理，也便于将已有 n8n / Make 等流程接入。自托管可掌握部署与数据保存位置，但节省的订阅开销要与数据库、平台审核、备份、升级和模型费用一起计算；未核算本轮真实成本或增长效果。

## 风险边界

- **自托管不等于离线**：内容发布与模型调用会访问外部服务。README 的“数据不离开环境”等简述不能覆盖这些工作流。
- README 的合规段落称服务不存储 / 代理用户 token，但当前 Prisma `Integration` 明确有 `token`、`refreshToken` 等字段。这里确认的是源码数据模型，未检查云端实际落盘、加密或保留策略；不能照抄为“无凭据存储”。
- 仓库 compose 含示例 JWT / 数据库密码、注册开启、`4007:5000` 及调试 Spotlight 等端口，不能原样视为生产部署；需改秘密、注册策略和实际监听面。
- 托管版与自建版的平台应用、审批、统计 scope、AI key 和运维责任不同；“支持某平台”不保证所有账户、地区和媒体格式均可发布。
- AGPL-3.0 及社媒 / 素材 / 模型条款需分别核对。抓取、视频 clipping 等可选链路依赖另外服务，README 概括声明不能代替对具体路径的检查。

## 补充建议

用授权的测试频道验收草稿到发布，检查取消、重复重试、过期 token、时区与失败告警。备份数据库与媒体后再迁移；先清点 .env 中实际启用的第三方和计费链路，待发布权限与内容审核规则明确后再放行 Agent 批量操作。

## 参考资料

- [README.md](https://github.com/gitroomhq/postiz-app/blob/a5affe62c74e39c1e7ac960d50d8418b807d532c/README.md)。
- [.env.example](https://github.com/gitroomhq/postiz-app/blob/a5affe62c74e39c1e7ac960d50d8418b807d532c/.env.example)。
- [docker-compose.yaml](https://github.com/gitroomhq/postiz-app/blob/a5affe62c74e39c1e7ac960d50d8418b807d532c/docker-compose.yaml)。
- [libraries/nestjs-libraries/src/database/prisma/schema.prisma](https://github.com/gitroomhq/postiz-app/blob/a5affe62c74e39c1e7ac960d50d8418b807d532c/libraries/nestjs-libraries/src/database/prisma/schema.prisma)。
- [LICENSE](https://github.com/gitroomhq/postiz-app/blob/a5affe62c74e39c1e7ac960d50d8418b807d532c/LICENSE)。
- [仓库 API](https://api.github.com/repos/gitroomhq/postiz-app)、[发行 API](https://api.github.com/repos/gitroomhq/postiz-app/releases?per_page=1)；动态元数据仅代表本轮采样。
- 事实依据为以上一手材料；价值、风险判断与建议为本库工程分析，未写作实测结论。
