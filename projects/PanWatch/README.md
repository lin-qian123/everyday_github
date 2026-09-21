<!-- markdownlint-disable MD013 MD034 -->

# PanWatch：自托管的多市场 AI 持仓与盯盘工作台

> 上游仓库：https://github.com/TNT-Likely/PanWatch · 归类：办公、商业与行业应用 · 本页基于 2026-09-22 的 README、release、许可证与 REST API 静态整理；未连接券商 / 行情、导入持仓、运行 TradingAgents 或验证收益表现。

## 定位

PanWatch 面向 A 股、港股和美股，将持仓、自选、技术指标、新闻、定时 Agent、提醒、模拟盘与多渠道通知放进自托管 Web / PWA，并可调用 TradingAgents 的多 Agent 分析流程。它是研究与监控界面，不是券商、持牌投顾或经审计的自动交易系统。

2026-09-22 的 GitHub 官方 Python Trending 抓取显示约 `+45 stars today`；REST API 快照为 `1,156 stars / 252 forks / 63 open issues`，MIT，最新 release 为 `0.14.0`（9 月 21 日）。

## 用法

上游提供 Docker 快速入口：

```sh
docker run -d \
  --name panwatch \
  -p 127.0.0.1:8000:8000 \
  -v panwatch_data:/app/data \
  sunxiao0721/panwatch:0.14.0
```

本页将上游示例的 `latest` 改为固定版本并绑定 loopback，避免无意暴露服务或滚动升级。首次使用应生成强 `JWT_SECRET`，只添加合成持仓，并为行情、LLM 与通知渠道配置低权限凭据。

## 原理

- FastAPI、SQLAlchemy 与 APScheduler 负责持仓 / 行情 / Agent 运行、持久化和定时任务，React / TypeScript 提供 PWA 界面。
- 盘前、盘中、盘后与新闻任务把技术指标、行情和内容交给所配置模型生成摘要或建议。
- TradingAgents 流程串联技术、情绪、新闻、基本面、看多 / 看空辩论、风险审查与 PM 汇总。
- 价格、涨跌幅、成交额、量比等规则以 AND / OR 组合触发，再发送到 Telegram、企业微信、钉钉、飞书、Bark 或 webhook。
- 内部 `trace_id`、agent run 表、LLM token / cost 和节点进度可选导出到 OpenTelemetry backend。

## 价值

- 将观察、持仓语境、Agent 运行、提醒和运行成本聚合到同一可追溯界面。
- 自托管有利于控制数据库与部署位置，版本化 Docker / release 便于固定实验环境。
- 多市场、多账户、模拟盘和可选 OTel 为策略观察与系统调试提供统一入口。
- 明确的规则告警可与 LLM 解释并列，便于区分确定性触发和生成式判断。

## 风险边界

- 自托管不等于数据不外发：行情 / 新闻、LLM provider、通知平台、浏览器下载和 OTel endpoint 都可能接收持仓或派生信息。
- 多 Agent 辩论与“风控审查”仍由模型和输入源驱动，不是独立风控、合规审查或可重复投资回测。
- 技术指标、新闻摘要和 AI score 可能滞后、过拟合、引用错误或形成伪确定性；模拟盘结果也不代表实盘。
- Web 登录、JWT、webhook、代理、浏览器自动化与持仓数据库构成高敏感攻击面；公网部署必须额外加固。
- 本页未核验行情授权、延迟、复权、交易日历、费用 / 滑点或任何收益主张。

## 补充建议

1. 先用合成 watchlist 与模拟数据测试，禁止真实下单，保存每次模型、prompt、数据时间与输出。
2. 对行情延迟、复权、停牌、跨市场时区、费用和缺失值建立确定性测试，不让 LLM填补未知数据。
3. 只绑定内网或 loopback，启用反向代理 TLS、强凭据、备份和最小权限通知 token。
4. 所有投资结论回到原始公告、行情与专业意见；任何交易由用户独立判断并承担风险。

## 参考资料

- 上游 README：https://github.com/TNT-Likely/PanWatch
- `0.14.0` release：https://github.com/TNT-Likely/PanWatch/releases/tag/0.14.0
- TradingAgents：https://github.com/TauricResearch/TradingAgents
- GitHub REST API：https://api.github.com/repos/TNT-Likely/PanWatch
- LICENSE：https://github.com/TNT-Likely/PanWatch/blob/main/LICENSE
