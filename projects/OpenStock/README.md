<!-- markdownlint-disable MD013 MD034 -->

# OpenStock：带可选 AI 摘要的开源股票观察与提醒应用

> 上游仓库：https://github.com/Open-Dev-Society/OpenStock · 归类：办公、商业与行业应用 · 本页基于 2026-09-20 的 README、API 文档、manifest、LICENSE 与 REST API 静态整理；未接入真实行情、账户、邮件或 AI provider。

## 定位

`OpenStock` 是以 Next.js 构建的股票观察应用，提供行情搜索、自选股、TradingView 图表、公司资料、提醒、新闻摘要和可选跨来源 sentiment 卡片。AI 主要用于欢迎邮件与每日新闻摘要等辅助流程；它不是券商、量化交易系统或经验证的投资顾问。

2026-09-20 的 GitHub 官方综合 / TypeScript Trending 抓取显示约 `+477 stars today`；REST API 快照为 `15,999 stars / 2,082 forks / 29 open issues`，AGPL-3.0，未发布 GitHub Release。

## 用法

项目要求 Node.js 20+、MongoDB、Finnhub key 和邮件配置；Gemini 等 AI key 为可选项：

```sh
git clone https://github.com/Open-Dev-Society/OpenStock.git
cd OpenStock
npm install
npm run test:db
npm run dev
```

后台工作流可用 `npx inngest-cli@latest dev` 本地启动。仓库也提供 Docker Compose；生产环境不应沿用示例 MongoDB 凭据或个人 Gmail 密码。

## 原理

- Next.js 15 / React 19 提供页面与 API，Better Auth + MongoDB 保存用户、session、自选股和偏好。
- Finnhub 提供 symbol、公司资料和市场新闻；TradingView widget 提供图表、technical 与市场视图。
- 可选 Adanos API 聚合 Reddit、X、新闻和 Polymarket 的 sentiment 快照，不能替代原始来源核对。
- Inngest 接收用户创建事件并执行定时任务；Gemini、MiniMax 或 Siray provider 可生成个性化欢迎文本和每日新闻摘要。
- Nodemailer 负责发信，用户国家、投资目标、风险承受和行业偏好参与个性化。

## 价值

- 把行情、图表、自选股、提醒、新闻与轻量 AI 摘要组织成可自托管的完整应用样板。
- 前后端、认证、数据库、定时任务和邮件链路齐全，适合学习金融信息产品工程。
- AI provider 可选，不使用 AI 时仍保留主要行情与观察功能。
- AGPL-3.0 与公开代码便于审查应用如何处理用户偏好、市场数据和第三方接口。

## 风险边界

- 上游明确说明它不是券商，行情可能因 provider 规则或套餐延迟；任何摘要、sentiment 或图表都不能直接当作交易建议。
- AI 摘要可能遗漏时间、币种、公司事件或来源冲突；必须回看公告、交易所和原始新闻。
- 用户画像、自选股、邮件地址和风险偏好属于敏感财务兴趣数据；MongoDB、日志、Inngest 和邮件内容都需最小化与保留治理。
- Finnhub、TradingView、Adanos、AI provider、Gmail / SMTP 形成多条外部数据流，各自有额度、许可和隐私条款。
- AGPL-3.0 对修改、部署与网络服务有义务；项目无 GitHub Release，生产使用应 pin commit 并自建发布流程。
- 本页未验证行情实时性、提醒幂等、auth、API 限流、邮件退订、provider fallback 或投资内容准确性。

## 补充建议

1. 只用模拟用户和 watchlist 做部署演练，给每个外部 provider 配置低额度 key、超时和速率限制。
2. 在 UI 中同时展示来源、抓取时间、市场时区与延迟状态，AI 摘要必须链接回原文。
3. 对用户偏好、session、邮件与日志建立删除、导出和最短保留策略。
4. 将任何交易或提醒动作保持为只读观察与人工确认，不让生成文本直接触发下单。

## 参考资料

- 上游 README：https://github.com/Open-Dev-Society/OpenStock
- API 文档：https://github.com/Open-Dev-Society/OpenStock/blob/main/API_DOCS.md
- 市场支持说明：https://github.com/Open-Dev-Society/OpenStock/blob/main/MARKET_SUPPORT.md
- GitHub REST API：https://api.github.com/repos/Open-Dev-Society/OpenStock
- LICENSE：https://github.com/Open-Dev-Society/OpenStock/blob/main/LICENSE
