<!-- markdownlint-disable MD013 -->

# edgeever

## 定位

EdgeEver 是可自托管的笔记与个人知识库，结合富文本 / Markdown、图表、表格、海报、网页剪藏、离线客户端和 MCP。适合让人和 Agent 共用可编辑资料库；同步、模型调用、备份和内容发布是不同的数据路径。

- 上游：[tianma-if/edgeever](https://github.com/tianma-if/edgeever)，仓库 ID `1281033762`。
- 2026-11-20 07 时段：官方 TypeScript daily **+57**；API stars / forks / open issues（含 PR）为 **3,437 / 1,788 / 67**。[API](https://api.github.com/repos/tianma-if/edgeever)
- 最新核到的非预发行版：[v2.30.0](https://github.com/tianma-if/edgeever/releases/tag/v2.30.0)，UTC 11-18；main 静态快照 `ca891dc2795c46b728e37a4ed1763f0c0d5707dd`，包版本同为 2.30.0，但不据此认为分发制品已经过本轮测试。
- 分类：`记忆层与个人 AI 基础设施`。今天首次建档，不代表今天首发。

## 用法

已有 Docker 的试用主机可按官方 Compose 手动部署，先固定版本并限制入口。以下示例未在本轮执行：

```bash
curl -fsSL https://raw.githubusercontent.com/tianma-if/edgeever/ca891dc2795c46b728e37a4ed1763f0c0d5707dd/compose.yaml -o compose.yaml
export EDGE_EVER_VERSION=v2.30.0
export EDGE_EVER_AUTH_PASSWORD='请替换为足够长的随机密码'
export EDGE_EVER_PORT='127.0.0.1:8787'
docker compose up -d
docker compose ps
```

访问本机 8787 端口，核 `/api/health` 与登录；正式远程访问按部署文档配置 HTTPS。开发用 `bun install`、`bun run dev`，仓库固定包管理器 `bun@1.3.14`；开发默认自动登录及公开示例密码不可直接当生产配置。[Compose](https://github.com/tianma-if/edgeever/blob/ca891dc2795c46b728e37a4ed1763f0c0d5707dd/compose.yaml)、[Docker 文档](https://github.com/tianma-if/edgeever/blob/ca891dc2795c46b728e37a4ed1763f0c0d5707dd/docs/deploy-docker.zh-CN.md)、[README](https://github.com/tianma-if/edgeever/blob/ca891dc2795c46b728e37a4ed1763f0c0d5707dd/README.zh-CN.md)、[包配置](https://github.com/tianma-if/edgeever/blob/ca891dc2795c46b728e37a4ed1763f0c0d5707dd/package.json)

接 Agent 时，在“个人中心 → API / MCP”为每个客户端创建独立 Token，搜索 / 总结先选只读；实例的 `/mcp` 使用 Bearer Token。先调用 `get_current_user` 核账号、工作区与权限，再读笔记；需要编辑时才选完全访问。[MCP 指南](https://github.com/tianma-if/edgeever/blob/ca891dc2795c46b728e37a4ed1763f0c0d5707dd/docs/mcp-guide.zh-CN.md)

## 原理

1. **共享应用、不同存储**：Cloudflare 和 Docker 执行同一个 Hono 应用及迁移；前者使用 Workers / D1 / R2，后者使用 Bun / SQLite / 本地文件或 S3。PostgreSQL 只是预留接口，当前没有实现。
2. **本地镜像与同步**：桌面和移动客户端保留本地数据库 / 草稿 / 同步队列，联网后增量同步。笔记同时保存结构化编辑内容、Markdown 和检索文本，支持编辑及导出。
3. **工具授权**：MCP 使用笔记本、笔记、附件、标签及 AI 等 scope；抽读的 `request-auth.ts` 检查 Token scope，交互用户会话另按用户身份处理。这是辅助鉴权代码观察，未逐路由证明全部权限覆盖。
4. **AI 请求路径**：架构文档明确默认由客户端直连配置的模型接口；Web 初始请求遇到网络 / CORS 限制时，可经已认证实例中转至已保存并启用的模型服务。桌面与原生移动端继续直连。

来源：[架构](https://github.com/tianma-if/edgeever/blob/ca891dc2795c46b728e37a4ed1763f0c0d5707dd/docs/self-hosting-architecture.zh-CN.md)、[README](https://github.com/tianma-if/edgeever/blob/ca891dc2795c46b728e37a4ed1763f0c0d5707dd/README.zh-CN.md)、[权限辅助实现](https://github.com/tianma-if/edgeever/blob/ca891dc2795c46b728e37a4ed1763f0c0d5707dd/apps/api/src/request-auth.ts)。

## 价值

- 用统一知识库承载人工笔记与 Agent 读写，便于把生成结果留在可编辑、可导出的工作区。
- Cloudflare 与 Docker 共用业务实现，方便按网络、存储和运维条件选部署方式。
- v2.30.0 特别修复桌面附件下载中断、合并笔记同步与 Evernote 异常附件恢复；这提示选型应重点测资料完整性，而不仅看编辑器功能数量。[发行说明](https://github.com/tianma-if/edgeever/releases/tag/v2.30.0)

## 风险边界

- **“免费”有条件。** README 的 Cloudflare 免费运行以配额为前提，且写明 R2 subscription 要绑定付款方式；模型、域名、超额用量与自托管设备另计。本轮未重新核云平台价格，也未开通服务。
- **自托管不等于模型请求留在本地。** 笔记内容可能随 AI 功能发往所选模型接口；网页中转还经过实例。7 月隐私政策的适用范围是移动 App / Web Clipper，不能把其无广告 / 遥测声明外推为所有 AI、图床、插件和第三方服务都没有数据出口。[政策源码](https://github.com/tianma-if/edgeever/blob/ca891dc2795c46b728e37a4ed1763f0c0d5707dd/apps/site/src/pages/privacy.astro)
- **安装器会安排后续更新。** 官方一键脚本文档称默认在服务器本地时间 04:17 通过 crontab 更新，通常跟随 `latest`；可固定版本或关闭自动更新。镜像回退不会撤销数据库 migration，升级前需备份，恢复应停机并使用空卷。[运维说明](https://github.com/tianma-if/edgeever/blob/ca891dc2795c46b728e37a4ed1763f0c0d5707dd/docs/deploy-docker.zh-CN.md)
- **备份与权限需要实际验证。** `/data` 包含数据库、附件及凭据加密根密钥副本，应作为敏感整体保护；选用 S3 还需单独备份桶。只读 / 完全访问 Token、同步副本、导出覆盖规则均须用测试实例确认，未做多用户隔离或恢复实验。
- **许可为 AGPL-3.0。** API 与根 LICENSE 一致；修改、提供网络服务和再分发时按对应版本与组件核条款。[LICENSE](https://github.com/tianma-if/edgeever/blob/ca891dc2795c46b728e37a4ed1763f0c0d5707dd/LICENSE)

## 补充建议

用一组包含公式、图片、异常附件和重复 ID 的脱敏笔记测试导入、离线编辑、双端冲突、ZIP 导出与独立恢复。先用只读 MCP 做检索，核引用是否来自全文；再在测试库逐项开放写入。分别记录模型服务、实例中转、对象存储与图床的内容流向，并用实际费用与恢复耗时评价长期价值。

## 参考资料

- [固定版本 MCP 使用与上传限制](https://github.com/tianma-if/edgeever/blob/ca891dc2795c46b728e37a4ed1763f0c0d5707dd/docs/mcp-guide.zh-CN.md)
- [发行列表](https://github.com/tianma-if/edgeever/releases)；其余固定 SHA 来源见各节。本页是资料与少量代码核读，未部署或连接个人知识库。
