<!-- markdownlint-disable MD013 -->

# TSP / tick-stock-panel（shy3130/tick-stock-panel）

> 上游仓库：<https://github.com/shy3130/tick-stock-panel> · 归类：办公、商业与行业应用 · 本页基于 2026-09-26 的 GitHub API、README、配置、tag、VERSION 与 LICENSE 静态整理，未部署服务、连接行情源、调用 LLM 或进行回测 / 交易。

- 抓取快照：5,159 stars、1,259 forks、17 open issues。
- 热度信号：GitHub 综合 / Python Trending 抓取时约 +44 当日 stars。
- 版本与许可：MIT；无 GitHub Release，latest tag 为 `v0.3.1`，根 `VERSION` 仍为 `v0.2.2`。

## 定位

TSP 是自托管的 A 股选股、因子研究、回测、行情监控和 AI 数据问答工作台。它把多数据源能力路由、统一 enriched 数据、Polars 计算、Parquet / DuckDB 存储、策略 / 因子 DSL、异动提醒和盘后复盘放进同一个本地应用。

## 用法

上游提供 Docker 单容器与 compose 路径。用户需要按实际数据源配置 API key、同步历史 / 实时数据，再在选股、因子、回测、监控与 AI 助手页面建立研究流程。README 明确项目只供学习和量化研究，不内置 AI 荐股或涨停预测；真实资金决策不应由该系统自动执行。

## 原理

数据源插件声明不同数据集能力，router 依据运行时探测选择 quote、日 K、分钟 K、财务等通道；数据进入本地 Parquet / DuckDB 后，经 Polars 指标流水线形成统一字段。策略、因子、回测和监控复用同一口径，回测放在子进程运行；AI 助手通过只读工具查询站内数据并显示调用足迹。

## 价值

它把数据接入、研究、监控和复盘的口径集中管理，减少各脚本间字段和复权不一致；自托管、可扩展数据源、样本外验证和显式发布候选等设计适合建立可复查的个人量化研究环境。工具足迹和只读助手也比直接让 LLM 生成交易指令更可审计。

## 风险边界

- 数据、策略和 AI 输出都可能错误、滞后或存在幸存者 / 前视偏差；回测收益不代表未来表现，本项目不是投资顾问、券商或自动交易系统。
- tag `v0.3.1` 与根 `VERSION=v0.2.2` 漂移，部署必须按 commit / image digest 固定；README 功能表不等于当前 artifact 全部可用。
- `tiers.yaml` 明示部分套餐速率沿用旧快照或由规律推断，不能作为数据商正式额度与价格依据。
- 自托管不等于零外发：TickFlow、fuyao、stock-sdk、LLM provider 和飞书通知都会改变数据流；行情、持仓、key 与对话历史都是敏感数据。
- AI 生成策略与只读回答仍会发生数据挖掘、多重检验和错误解释；T+1、费用、滑点模型也不能覆盖真实成交、停牌、涨跌停、流动性和公司行为全部边界。

## 补充建议

仅用延迟公开数据和合成持仓部署副本，固定 `v0.3.1` tag 对应 commit，先核对复权、交易日、停牌和分钟数据。建立 walk-forward、严格样本外、费用 / 滑点敏感性和多重检验流程；逐数据源记录条款、延迟、缺失和修订，并禁止 AI / 监控直接触发真实订单。

## 参考资料

- [GitHub 仓库](https://github.com/shy3130/tick-stock-panel)
- [GitHub REST API](https://api.github.com/repos/shy3130/tick-stock-panel)
- [v0.3.1 tag](https://github.com/shy3130/tick-stock-panel/tree/v0.3.1)
- [配置文档](https://github.com/shy3130/tick-stock-panel/blob/main/docs/configuration.md)
- [自定义数据源](https://github.com/shy3130/tick-stock-panel/blob/main/docs/custom-data-source.md)
- [tiers.yaml](https://github.com/shy3130/tick-stock-panel/blob/main/tiers.yaml)
- [LICENSE](https://github.com/shy3130/tick-stock-panel/blob/main/LICENSE)
