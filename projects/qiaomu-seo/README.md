# qiaomu-seo

- 仓库：[joeseesun/qiaomu-seo](https://github.com/joeseesun/qiaomu-seo)
- 快照：2026-08-04 抓取；GitHub API 显示其创建于 2026-08-03，约 114 stars、12 forks，MIT。数字会随时间变化。
- 分类：办公、商业与行业应用

## 定位

面向 Google、Bing 与 AI 搜索入口的 Agent Skill。它把技术 SEO、关键词—页面规划、流量诊断、迁移和验证串成可审阅流程，明确区分直接观察、推断与缺失证据。

## 用法

在支持 Agent Skills 的客户端执行 `npx skills add joeseesun/qiaomu-seo`，先以“审计/诊断/比较”方式输入 URL、sitemap、渲染页面或站长平台导出；只有在站点所有者明确授权后，才让 agent 改动 robots、canonical、重定向或代码。仓库提供 `scripts/validate_skill.py` 与知识时效校验命令。

## 原理

按“发现与抓取 → 渲染 → 可索引性 → canonical/hreflang → 意图与内链 → 搜索表现”拆解问题。它把实验室性能、真实用户指标、Schema 语法、搜索功能资格与实际展示分别处理，并为 AI Search 单列供应商与 crawler 边界。

## 价值

适合把零散 SEO 检查表变成可复核的诊断交付：问题可按影响、置信度、工作量和依赖排序，也能留下迁移映射、测试和回滚线索。

## 风险边界

robots、sitemap、IndexNow、结构化数据与 AI crawler 设置都不保证收录、排名或模型引用。Search Console、日志及受控站点信息可能敏感；不应把没有授权的站点、账户或生产配置交给自动化修改。

## 补充建议

先在 staging 对一组 URL 做只读审计，固定抓取日期、页面样本和数据口径；上线修改应包含回滚、监控窗口与人工验收。对“AI 搜索可见性”只报告可观测证据，不承诺引用结果。

## 参考资料

- [项目 README](https://github.com/joeseesun/qiaomu-seo)
- [GitHub API 元数据快照](https://api.github.com/repos/joeseesun/qiaomu-seo)
