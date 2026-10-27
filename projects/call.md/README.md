<!-- markdownlint-disable MD013 -->

# Call.md：把会议录制接入实时助手与工作流

- 主上游：[video-db/call.md](https://github.com/video-db/call.md)；repository ID `1166606658`。
- 采样日期：2026-10-28（Asia/Shanghai）；分类：办公、商业与行业应用。
- API 累计快照：1,935 stars / 227 forks / 8 open issues（含 PR 口径），与榜单日增分开。
- 默认分支 `main`；主线依据固定在 `ba53ebed3643920bb9ef9d08ee33e59bd708c930`。发行 API 本轮返回空列表；此状态不代表没有源码标签或其他分发渠道。
- 核验层级：一手文档、元数据和所列部分实现的静态阅读；未安装运行、调用模型、复现基准或验证真实用户效果。

## 定位

Call.md 是 Electron 会议工具，采集麦克风 / 系统音频与屏幕，结合 VideoDB 实时转写、会中建议、MCP 工具和会后摘要。它把会议接成 Agent 工作流；“local-first”描述本地存储的一部分，转写与 AI 处理需要联网。

## 用法

README 提供 macOS 12+ 的远程安装脚本，应先下载审阅并核验来源。源码开发要求 Node.js 22.12+ / npm 10+；在固定 checkout 中：

```bash
npm install
npm run rebuild
npm run dev
```

登录 VideoDB API key 后，以合成对话测试并授予必要系统权限。macOS arm64 / x64 与 Windows x64 支持录制，Windows 当前需源码构建；Linux 和 Windows ARM64 可用部分 UI，但不支持录制。本轮未安装、录音、调用模型或连接日历。

## 原理

Electron 主进程管理录制、SQLite 和服务，React 提供界面；双通道音频区分本人和系统声音，通过 VideoDB 进行实时转写。转写进入建议、指标与 MCP agent loop；结束后生成概述、主题要点和行动项，可导出 Markdown 或发送配置的 webhook。当前 MCP 实现可根据模型返回自动执行工具调用，并限制单轮工具调用数；次数上限不是外部写入审批。

## 价值

适合需要当场检索信息、保留行动项并接入后续系统的团队，也可作为桌面采集与实时 Agent 编排参考。转写说话人归属、建议质量与摘要完整性须单独测量，不能以功能列表推断沟通或销售效果。

## 风险边界

- 先取得参会者对采集及云处理的适用授权。README 说明录制、转写与 AI 输入会送往 VideoDB；Google Calendar、远程 MCP 与 webhook 还增加其他接收方。本地 SQLite 不构成离线处理保证。
- 主进程 HTTP 绑定 `127.0.0.1`，允许部分 loopback / null origins；文档还描述访问 token 与 OS 凭据保护。这些只是分层控制，本轮没有验证所有认证路径、系统密钥库行为或发布包。
- 接入可写 MCP 后，会议中的话语可能触发真实动作；应从只读工具开始，并在宿主或服务端限定权限。不能把会中模型判断当作执行授权。
- webhook 实现固定到已批准的 DNS 地址、返回重定向而不跟随，并使用超时；不等于数据可任意外发。需审核接收端、传送字段与删除 / 保留策略。
- package.json 声明 MIT，README 徽章也写 MIT，但本轮完整 tree 没有发现独立 LICENSE 文件，API license 为空；再分发前补核完整授权文本与 VideoDB SDK / 服务条款。

## 补充建议

用虚构会议依次核对权限拒绝、双通道归属、语言回退、暂停 / 睡眠与两小时录制上限，再测试摘要导出、注销和凭据轮换。先关闭自动 webhook 和可写 MCP，明确数据保留期限后再接真实会议。

## 参考资料

- [README.md](https://github.com/video-db/call.md/blob/ba53ebed3643920bb9ef9d08ee33e59bd708c930/README.md)。
- [package.json](https://github.com/video-db/call.md/blob/ba53ebed3643920bb9ef9d08ee33e59bd708c930/package.json)。
- [src/main/lib/webhook-request.ts](https://github.com/video-db/call.md/blob/ba53ebed3643920bb9ef9d08ee33e59bd708c930/src/main/lib/webhook-request.ts)。
- [src/main/server/index.ts](https://github.com/video-db/call.md/blob/ba53ebed3643920bb9ef9d08ee33e59bd708c930/src/main/server/index.ts)。
- [src/main/services/mcp/mcp-agent.service.ts](https://github.com/video-db/call.md/blob/ba53ebed3643920bb9ef9d08ee33e59bd708c930/src/main/services/mcp/mcp-agent.service.ts)。
- [仓库 API](https://api.github.com/repos/video-db/call.md)、[发行 API](https://api.github.com/repos/video-db/call.md/releases?per_page=1)；动态字段只代表本轮采样。
- 事实依据为以上一手材料；价值、风险推论与补充建议为本库工程分析。
