<!-- markdownlint-disable MD013 -->

# infinite-canvas：图片创作与 Agent 编排画布

- 主上游：[basketikun/infinite-canvas](https://github.com/basketikun/infinite-canvas)；repository ID `1242967652`。
- 采样日期：2026-10-25（Asia/Shanghai）；分类：前端、UI 与 Agent 交互层。
- API 累计快照：9,000 stars / 2,109 forks / 19 open issues（含 PR 口径）；与榜单日增分开。
- 默认分支 `main`，本页静态依据固定在 `9f2bd9f1b27c45fd1b8f5323072b07243f9e0fac`。发行列表首项 `v0.20.0`，发布于 2026-10-10T08:47:20Z（正式）。
- 核验层级：直接读取上游文档、许可、元数据和下列部分实现；未安装运行、调用模型或复现性能。

## 定位

无限画布把图片生成、参考图编辑、对话、提示词与素材管理合入可视化工作台，并提供本地 Canvas Agent 接入 Codex / Claude Code。它是创作与编排界面，生成能力依赖配置的模型渠道。README 明示仍在开发，历史本地存储格式可能变化；不能据最新版本号推断数据迁移稳定。

## 用法

本地开发按上游说明运行：

```bash
git clone https://github.com/basketikun/infinite-canvas.git
cd infinite-canvas/web
bun install
bun run dev
```

也可在仓库根目录用 docker compose；README 的 Docker 入口默认 localhost:3000。进入配置填写可信供应商的 Base URL 与 API key。Canvas Agent 是另一个按独立包版本发行的本机服务，需要地址和 token；启动它并不会自动注册 Codex MCP。以上均未在本轮安装或执行。

## 原理

前端画布管理节点、素材和生成记录，经配置渠道调用生成接口；默认 API key、Base URL、画布和素材保存在浏览器本地。可选 Canvas Agent 默认监听 127.0.0.1，以连接 token 和首次绑定的网页 Origin 限制入口，再桥接本机 coding agent。WebDAV、代理、插件与本机 Agent 会引入额外的数据流，不能由“本地存储”推断所有处理离线。

## 价值

适合在同一创作上下文里组织参考图、比较多轮输出和复用提示词；本机 Agent 可让画布与工程工具衔接。模型质量、视频一致性和渠道稳定性需要用固定素材另测，本轮只确认文档与配置设计。

## 风险边界

SECURITY.md 明确远程节点插件在网页内执行，可访问页面数据和本地保存的 API key；这属于已声明的信任模型，安装确认不提供细粒度隔离。源代码为 MIT，但模型渠道、素材许可和商业服务条款另核。第三方赞助广告里的价格、折扣、模型同一性或稳定性不作本轮事实。Debug 日志会落盘，虽声明隐藏 token 与图片 Data URL，仍应检查任务信息与保留期。

## 补充建议

用专门浏览器 profile、低额度测试 key 和有权使用的素材起步；导出旧画布后再升级。只安装审核过的插件，核查 WebDAV 同步范围、服务端代理出口、Origin 撤销及本机 Agent 日志。将网页、Canvas Agent 包、模型渠道和资产版本分别记录。

## 参考资料

- [README.md](https://github.com/basketikun/infinite-canvas/blob/9f2bd9f1b27c45fd1b8f5323072b07243f9e0fac/README.md)。
- [SECURITY.md](https://github.com/basketikun/infinite-canvas/blob/9f2bd9f1b27c45fd1b8f5323072b07243f9e0fac/SECURITY.md)。
- [docs/content/docs/overview/quick-start.mdx](https://github.com/basketikun/infinite-canvas/blob/9f2bd9f1b27c45fd1b8f5323072b07243f9e0fac/docs/content/docs/overview/quick-start.mdx)。
- [canvas-agent/README.md](https://github.com/basketikun/infinite-canvas/blob/9f2bd9f1b27c45fd1b8f5323072b07243f9e0fac/canvas-agent/README.md)。
- [LICENSE](https://github.com/basketikun/infinite-canvas/blob/9f2bd9f1b27c45fd1b8f5323072b07243f9e0fac/LICENSE)。
- [仓库 API](https://api.github.com/repos/basketikun/infinite-canvas)、[发行 API](https://api.github.com/repos/basketikun/infinite-canvas/releases?per_page=3)；动态元数据只代表本轮采样。
- 事实来源为以上固定文件；价值、风险评估和验证建议为本库工程判断，未作为上游实测结果。
