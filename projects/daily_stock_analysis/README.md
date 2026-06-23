# daily_stock_analysis（ZhuLinsen/daily_stock_analysis）

- GitHub: https://github.com/ZhuLinsen/daily_stock_analysis
- 官网: https://dsa.zhulinsen.tech
- 记录日期: 2026-06-23 (Asia/Shanghai)

## 定位

`daily_stock_analysis` 是一个用大模型驱动的多市场股票分析系统，覆盖 A 股、港股、美股、日股、韩股等市场，把行情、新闻、技术指标、风险提示和通知渠道整合成一个“每日决策仪表盘”工作流。

## 热度信号

1. GitHub API 在 2026-06-23 抓取时显示约 `45.8k stars`、`41.9k forks`，`updated_at` 为 `2026-06-23T01:01:09Z`。
2. GitHub Trending 的 Python 日榜在 2026-06-23 抓取时出现该项目，当日新增星标约 `1,557 stars today`。
3. 官方 README 直接强调多市场行情、实时新闻、决策看板、GitHub Actions 定时运行和多渠道自动推送。

## 用法

### 1) 最轻量的方式是直接用 GitHub Actions

README 把 GitHub Actions 作为推荐入口，核心流程是：

1. Fork 仓库。
2. 在 GitHub Secrets 中配置模型 API Key、通知渠道和 `STOCK_LIST`。
3. 手动运行或按工作日定时执行。

这种做法的重点不是本地量化回测，而是用最低运维成本生成定时股票分析报告。

### 2) 也支持本地运行或 Docker

README 提供的本地入口是：

```bash
git clone https://github.com/ZhuLinsen/daily_stock_analysis.git
cd daily_stock_analysis
pip install -r requirements.txt
cp .env.example .env
python main.py
```

常用模式包括：

```bash
python main.py --dry-run
python main.py --stocks 600519,hk00700,AAPL
python main.py --webui
python main.py --schedule
```

### 3) 输出不只是一段文字，而是完整工作台

README 展示的交付物包括：

- 每日决策仪表盘
- 大盘复盘
- Web 工作台
- Agent 策略问股
- 多渠道推送到企微、飞书、Telegram、Discord、Slack、邮箱

## 原理

1. 先汇总多市场行情、新闻搜索、社交舆情和技术指标，再交给 LLM 生成带评分、风险、催化因素和行动建议的分析报告。
2. 模型层支持多个云端 API 和本地模型，数据层则整合 AkShare、Tushare、YFinance 等来源。
3. 调度层同时覆盖 GitHub Actions、本地定时任务、Docker 和 FastAPI / WebUI，说明它是“分析系统”而不是单纯 prompt 模板。
4. 它还把“问股 agent”做进 Web 入口，允许用户围绕策略、题材、趋势和事件做多轮追问。

## 价值

- 这是少见把 LLM 分析、市场数据、自动化调度和通知交付打成完整闭环的开源项目。
- 对个人投资者和小团队来说，价值不在“替你决定买什么”，而在于节省每日信息整理和固定格式报告时间。
- 它也体现了一个趋势：AI 金融工具开始从聊天问答转向可重复、可定时、可投递的 operational workflow。

## 风险边界

- 股票分析属于高风险场景，任何模型输出都不能替代投资决策，更不能把评分当成可直接执行的交易信号。
- 新闻源、舆情源、市场接口和模型本身都可能引入误差、延迟或幻觉，结果适合作辅助判断，不适合作唯一依据。
- 项目虽然强调低成本部署，但要真正长期使用，仍要处理 API 配额、新闻质量、通知稳定性和市场节假日边界。

## 补充建议

1. 如果只是想做日报推送，优先用 GitHub Actions 跑最小闭环，不要一开始就追求全量功能。
2. 如果你更关心策略验证而非信息整合，可把它与回测/选股工具分开使用，不要混淆“分析报告”和“可验证策略”。
3. 最值得评估的不是文案是否流畅，而是数据源覆盖、市场适配边界、风险提示是否稳定可复核。

## 参考资料

- https://github.com/ZhuLinsen/daily_stock_analysis
- https://dsa.zhulinsen.tech
- https://github.com/trending/python?since=daily
