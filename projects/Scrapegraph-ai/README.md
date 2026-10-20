<!-- markdownlint-disable MD013 -->

# ScrapeGraphAI（Scrapegraph-ai）

> 更新：2026-10-21（Asia/Shanghai）。分类：RAG、检索与知识处理。上游 `ScrapeGraphAI/Scrapegraph-ai`；快照 `194055e203af`（main）。本文为官方资料与源码静态研究；热度、发行时间及社媒限制见[当日日报](../../daily/2026-10-21/ai-hotspots.md)。

## 定位

Python 网页与本地文档提取库，以提示词、来源和模型配置构建 scraping graph。开源 `scrapegraphai` 与另行托管的 ScrapeGraph API / SDK 是不同部署与计费路径。[README.md](https://github.com/ScrapeGraphAI/Scrapegraph-ai/blob/194055e203afce41ed4e70365dbc416bad756115/README.md)

## 用法

当前 pyproject 要求 Python `>=3.12,<4.0`；在独立环境安装 `scrapegraphai` 并准备 Playwright 浏览器。常用 `SmartScraperGraph(prompt=..., source=..., config=...)` 后调用 `.run()`；README 示例使用 Ollama，也支持云模型配置。[pyproject.toml](https://github.com/ScrapeGraphAI/Scrapegraph-ai/blob/194055e203afce41ed4e70365dbc416bad756115/pyproject.toml) [README.md](https://github.com/ScrapeGraphAI/Scrapegraph-ai/blob/194055e203afce41ed4e70365dbc416bad756115/README.md)

在导入包及处理数据前，显式设置 `SCRAPEGRAPHAI_TELEMETRY_ENABLED=false`，再核实际网络行为。使用本地模型仍可能存在浏览器抓取、下载及其他出站。[scrapegraphai/telemetry/telemetry.py](https://github.com/ScrapeGraphAI/Scrapegraph-ai/blob/194055e203afce41ed4e70365dbc416bad756115/scrapegraphai/telemetry/telemetry.py)

## 原理

SmartScraperGraph 将抓取、解析、生成回答等节点按 graph 串接；BaseGraph 保存状态与执行信息，调用模型将非结构文本转成目标字段。schema 约束输出形状，但不能保证每个值与源文一致。[scrapegraphai/graphs/smart_scraper_graph.py](https://github.com/ScrapeGraphAI/Scrapegraph-ai/blob/194055e203afce41ed4e70365dbc416bad756115/scrapegraphai/graphs/smart_scraper_graph.py) [scrapegraphai/graphs/base_graph.py](https://github.com/ScrapeGraphAI/Scrapegraph-ai/blob/194055e203afce41ed4e70365dbc416bad756115/scrapegraphai/graphs/base_graph.py)

## 价值

工程判断：适合网页结构变动较多、字段定义可用自然语言表达的低量提取原型。与固定选择器比较时，应同时计准确率、缺失率、重试、延迟和模型成本；不能只比较代码行数。

## 风险边界

- README 称收集匿名用量，但当前源码默认启用遥测，payload 可包含 `user_prompt`、`json_schema`、`website_content`、`llm_response`、模型名和 URL，发往外部 tracing 服务。BaseGraph 在 URL 成功回答路径传入正文与结果；字段齐全才构造 payload，错误 / 缺字段路径跳过。不能称每次调用都上传，也不能称只上传匿名计数。[README.md](https://github.com/ScrapeGraphAI/Scrapegraph-ai/blob/194055e203afce41ed4e70365dbc416bad756115/README.md) [scrapegraphai/telemetry/telemetry.py](https://github.com/ScrapeGraphAI/Scrapegraph-ai/blob/194055e203afce41ed4e70365dbc416bad756115/scrapegraphai/telemetry/telemetry.py) [scrapegraphai/graphs/base_graph.py](https://github.com/ScrapeGraphAI/Scrapegraph-ai/blob/194055e203afce41ed4e70365dbc416bad756115/scrapegraphai/graphs/base_graph.py)
- 网页正文可能包含提示注入或敏感数据；云模型与托管 API 是额外数据出口。生成 Python 脚本的其他 graph 需单独审查执行权限，不能由结构化提取结果推断安全。[README.md](https://github.com/ScrapeGraphAI/Scrapegraph-ai/blob/194055e203afce41ed4e70365dbc416bad756115/README.md)
- 开源库 MIT，托管服务另有账户、计费和条款。网站授权、访问规则及内容再利用需逐源核实；模型补全与“查无数据”必须区分。[LICENSE](https://github.com/ScrapeGraphAI/Scrapegraph-ai/blob/194055e203afce41ed4e70365dbc416bad756115/LICENSE) [README.md](https://github.com/ScrapeGraphAI/Scrapegraph-ai/blob/194055e203afce41ed4e70365dbc416bad756115/README.md)

## 补充建议

先用一组有人工真值的授权静态页面，保留字段的原文位置与缺失状态；对比 Ollama 和云模型的数据流、准确率与账单。遥测行为本轮仅做调用链静态核查，没有执行抓取或证明任何实际数据外发。

## 参考资料

- [README.md](https://github.com/ScrapeGraphAI/Scrapegraph-ai/blob/194055e203afce41ed4e70365dbc416bad756115/README.md)
- [LICENSE](https://github.com/ScrapeGraphAI/Scrapegraph-ai/blob/194055e203afce41ed4e70365dbc416bad756115/LICENSE)
- [pyproject.toml](https://github.com/ScrapeGraphAI/Scrapegraph-ai/blob/194055e203afce41ed4e70365dbc416bad756115/pyproject.toml)
- [scrapegraphai/telemetry/telemetry.py](https://github.com/ScrapeGraphAI/Scrapegraph-ai/blob/194055e203afce41ed4e70365dbc416bad756115/scrapegraphai/telemetry/telemetry.py)
- [scrapegraphai/graphs/smart_scraper_graph.py](https://github.com/ScrapeGraphAI/Scrapegraph-ai/blob/194055e203afce41ed4e70365dbc416bad756115/scrapegraphai/graphs/smart_scraper_graph.py)
- [scrapegraphai/graphs/base_graph.py](https://github.com/ScrapeGraphAI/Scrapegraph-ai/blob/194055e203afce41ed4e70365dbc416bad756115/scrapegraphai/graphs/base_graph.py)
- [仓库 API](https://api.github.com/repos/ScrapeGraphAI/Scrapegraph-ai)
- [v2.3.1 Release](https://github.com/ScrapeGraphAI/Scrapegraph-ai/releases/tag/v2.3.1)
