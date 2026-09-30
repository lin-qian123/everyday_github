<!-- markdownlint-disable MD013 -->

# Claude SEO（AgriciDaniel/claude-seo）

> 上游仓库：<https://github.com/AgriciDaniel/claude-seo> · 归类：办公、商业与行业应用 · 本页基于 2026-10-01 的 GitHub API、README、architecture、privacy、security、Release 与 LICENSE 静态整理，未安装 Claude Code plugin、抓取客户站点或验证 SEO 成效。

- 抓取快照：18,049 stars、2,652 forks、18 open issues。
- 热度信号：GitHub Python Trending 抓取时约 +72 当日 stars。
- 版本与许可：MIT；latest Release 与 tag 均为 `v2.4.1`。

## 定位

Claude SEO 是 Claude Code 的开源 SEO plugin，包含 26 个 sub-skill、19 个 specialist agent 和一组本地 Python 工具，覆盖技术 SEO、内容 / E-E-A-T、Schema、GEO、local / ecommerce / international SEO 与报告。另有 Google API 与 9 类可选扩展，将外部排名、backlink、crawl、AI visibility 和 analytics 数据接入 workflow。

## 用法

Claude Code 1.0.33+ 可通过 plugin marketplace 安装，再执行 `/seo setup` 建立隔离 Python 环境并下载 Playwright Chromium；也可 clone 后审阅安装脚本。`/seo audit <url>` 启动全站并行审计，`page`、`technical`、`schema`、`geo`、`agentic` 等命令处理专项任务。扩展和 Google API 需单独账号、密钥与配置。

## 原理

orchestrator 将站点发现、HTML / rendered page 获取、schema、内容、性能和外部数据拆给不同 Agent / deterministic script，再汇总优先级、score、可证伪检查和 Markdown / PDF / JSON 报告。核心默认不联系 Claude SEO 自有后端，但会访问用户指定站点；Playwright 用于 hydration，SQLite 保存 drift snapshot。扩展可调用 Google、DataForSEO、Firecrawl、Ahrefs、SE Ranking、Profound、Bing、Matomo 等服务。

## 价值

它把一次性“让模型看网页”提升为可重复命令、分工和报告模板，适合建立站点基线、回归 drift 和审查 Schema / 搜索可访问性。对工程团队，primary-source ledger、明确的 third-party heuristic 标记和可证伪条目比只有笼统建议更便于复核。

## 风险边界

- 项目方的速度、成本、增长案例、410 tests 和效果图均未在本轮独立复验；SEO score 不是 Google 排名保证。
- full audit 会产生大量 Claude Agent 调用，README 已说明部分任务使用更高价模型；必须先限定 URL、并发、预算和客户授权。
- core 虽“本地默认”，仍会抓取目标站点并在 Claude Code 会话中处理内容；启用扩展后 URL、关键词、品牌或文本会交给第三方。
- Google / Bing Indexing 等接口可产生真实外部写入；审计建议与自动提交必须分开授权。
- 安装器会创建持久 plugin 环境、下载浏览器并写用户级配置；远程脚本、MCP server 和凭据目录应在执行前审阅。
- 重客户端渲染、交互后内容、登录页和地区化输出可能产生误判；LLM 对 E-E-A-T、内容质量和“可引用性”的评分带主观性。

## 补充建议

先在自有测试站点只运行 read-only、无扩展的 page / schema 命令，保存原始 HTML、浏览器截图和工具版本；再逐个开放 API。对每条高优先级结论回到 Google / Schema / web.dev 一手文档和真实 Search Console 数据，并设置 URL allowlist、并发 / 费用上限与写操作审批。客户报告应披露数据时间窗、抓取覆盖和不确定性。

## 参考资料

- [GitHub 仓库](https://github.com/AgriciDaniel/claude-seo)
- [GitHub REST API](https://api.github.com/repos/AgriciDaniel/claude-seo)
- [README](https://github.com/AgriciDaniel/claude-seo/blob/main/README.md)
- [Architecture](https://github.com/AgriciDaniel/claude-seo/blob/main/docs/ARCHITECTURE.md)
- [Privacy](https://github.com/AgriciDaniel/claude-seo/blob/main/PRIVACY.md)
- [Security Policy](https://github.com/AgriciDaniel/claude-seo/blob/main/SECURITY.md)
- [v2.4.1 Release](https://github.com/AgriciDaniel/claude-seo/releases/tag/v2.4.1)
- [LICENSE](https://github.com/AgriciDaniel/claude-seo/blob/main/LICENSE)
