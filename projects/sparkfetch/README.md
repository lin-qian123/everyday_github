# SparkFetch

- 仓库：[Sparkfetch/sparkfetch](https://github.com/Sparkfetch/sparkfetch)
- 快照：2026-08-06 抓取；GitHub API 显示其创建于 2026-08-05，约 37 stars、8 forks，MIT。数字会随时间变化。
- 分类：RAG、检索与知识处理

## 定位

可自托管的网页抓取与内容提取 API，面向 RAG、研究工具和 Agent，把 URL 转为清理后的 Markdown、JSON 或纯文本。

## 用法

仓库要求 Node.js 18+ 与 pnpm 9+；克隆后执行 `pnpm install`，再用 `pnpm --filter @workspace/api-server run dev` 启动 API。通过 `POST /api/v1/scrape` 抓单页、`POST /api/v1/crawl` 提交限深度爬取任务、`GET /api/v1/crawl/:jobId` 读取状态，或用 `POST /api/v1/map` 发现站内链接。

## 原理

服务抓取 HTML 后去除导航、广告等样板内容，按 `includeTags`/`excludeTags` 限定正文，再连同标题、描述、链接和抓取时间返回。递归 crawl 使用深度、条数与路径排除条件限制范围，便于接入后续 chunk、向量化或引用链路。

## 价值

将网页接入层独立为可替换 API，能减少每个 RAG/Agent 项目重复编写 HTML 清洗逻辑；输出保留来源 URL 与元数据，利于再做可追溯引用。

## 风险边界

网页可访问不代表获准抓取、再分发或用于训练；登录态、个人数据、robots/站点条款、速率和反爬限制必须单独处理。Markdown 清洗也不保证正文完整、表格正确、时效一致或免受网页 prompt injection 影响。

## 补充建议

在 allowlist、限速、最大页数和出站网络隔离下先跑；保存原始响应哈希和抓取时间，以便纠错。把抽取结果视为不可信输入，交给 LLM 前删除隐藏指令并标注来源与可信度。

## 参考资料

- [项目 README](https://github.com/Sparkfetch/sparkfetch)
- [项目站点](https://sparkfetch.site)
- [GitHub API 元数据快照](https://api.github.com/repos/Sparkfetch/sparkfetch)
