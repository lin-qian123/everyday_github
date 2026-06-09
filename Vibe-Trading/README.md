# Vibe-Trading

## 项目定位
`Vibe-Trading` 是一个面向金融研究与量化策略实验的 AI Trading Agent 项目，试图把自然语言研究、数据拉取、策略生成、回测、风险校验和多代理讨论整合到同一条工作流里。

- GitHub：https://github.com/HKUDS/Vibe-Trading
- 适用人群：量化研究者、交易自动化实验者、希望把 LLM 接进投研流程的工程团队。

## 用法

官方 README 给了四条使用路径，主线比较清楚：

1. 最快安装：`pip install vibe-trading-ai`
2. 初始化环境：`vibe-trading init`
3. 直接运行单次任务：
   - `vibe-trading run -p "Backtest a BTC-USDT 20/50 moving-average strategy for 2024 and summarize return and drawdown"`
4. 按需要选择：
   - `vibe-trading`：交互式 CLI / TUI
   - `vibe-trading serve --port 8899`：启动 Web UI / API
   - `vibe-trading-mcp`：作为 MCP 服务接入外部 Agent

如果想本地完整跑起来，官方还提供 Docker 和本地开发两条路；如果想把它嵌进现有 Agent 工具链，则可以直接走 MCP 模式。

## 原理

这个项目的重点不是“让模型预测涨跌”，而是把投研流程拆成可验证的工程步骤：

- 路由层：根据用户问题选择对应市场、数据源、技能和 swarm preset。
- 数据层：拉取 A 股、港美股、加密货币、期货、外汇、文档和网页上下文。
- 执行层：生成策略代码、调用工具、跑回测或分析工作流。
- 校验层：补充基准对比、Monte Carlo、Bootstrap、Walk-Forward 和风险提示。
- 交付层：输出报告、执行痕迹、可导出指标和后续会话上下文。

README 中最值得注意的是三块资产：

- `77` 个 finance skills：覆盖数据、策略、分析、风险、加密等类别。
- `29` 个 swarm presets：把投委会、技术分析组、宏观 desk 等 workflow 做成可复用模板。
- `452` 个预置 alpha：强调因子实验和批量评分能力。

这说明它定位的是“金融 Agent 操作系统”，不是单一回测脚本。

## 价值

- 对 AI 投研赛道，它把自然语言、策略实验和可追溯执行日志串起来了，明显比只会生成 Pine Script 的 demo 更完整。
- MCP、CLI、Web UI 三种入口都给了，便于接入现有 Agent 体系。
- 即使不直接用于真实交易，也适合作为“研究助手 + 回测工厂”的原型底座。

## 风险边界

- 交易类 Agent 最容易被过度包装，README 里的能力并不等于稳定盈利能力，更不等于可直接实盘。
- 数据源虽然很多，但免费源回测和真实交易之间仍有延迟、缺口和清洗差异。
- LLM 参与策略生成时，最大风险不是不会写代码，而是可能生成看似合理、实则含未来函数或过拟合的逻辑。
- 如果暴露成远程 API，官方也明确建议设置 `API_AUTH_KEY`，说明权限和执行面本身就是风险点。

## 补充建议

- 使用时先把它当“研究与验证工具”，不要默认它能替代交易决策。
- 最值得复用的是流程骨架：数据路由、策略生成、回测校验、风险审查，而不是某个具体 alpha 或 swarm 名字。
- 如果团队想做垂直金融 Agent，可以先拿它验证交互和流程，再把真实风控、权限、审计和券商接口独立重做。

## 参考资料

- 仓库主页：https://github.com/HKUDS/Vibe-Trading
- GitHub Trending：https://github.com/trending
- PyPI 包入口：https://pypi.org/project/vibe-trading-ai/
