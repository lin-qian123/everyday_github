# circuit-framework

## 定位

`circuit-framework` 是一个 crypto-native 多 agent 研究与纸面交易框架，fork 自 `TradingAgents`。它让多个专门 agent 分析市场结构、衍生品、情绪、催化因素和市场 regime，再由确定性风险引擎批准或拒绝交易提案。

截至 2026-07-18 抓取时，仓库约 `478` stars、`18` forks，主要语言为 Python，许可证为 `Apache-2.0`。

## 用法

安装：

```bash
pip install -e ".[dev]"
```

CLI 示例：

```bash
tradingagents crypto analyze BTC
tradingagents crypto analyze ETH --strategy momentum
tradingagents crypto analyze HYPE --strategy derivatives --paper
tradingagents crypto portfolio
```

项目保留 upstream stock research mode，也支持 Python API 调用。测试命令在 README 中仍写作 `python3 -m pytest -q`，本机自动化使用时可按仓库约定优先尝试 `python`。

## 原理

系统先构建不可变的 `CryptoMarketSnapshot`，再交给 Market Structure、Derivatives、Sentiment、Catalyst、Regime、Bull / Bear Researcher、Research Manager、Trader、Risk Debate、Portfolio Manager 等角色。Trader 生成结构化 `CryptoTradeProposal`，最终由 deterministic risk gate 根据数据新鲜度、止损、R:R、spread、杠杆、波动率和置信度进行批准、缩放或拒绝。

公开数据当前只使用 Hyperliquid `POST https://api.hyperliquid.xyz/info`，不请求 wallet credentials，也不真实下单。

## 价值

- 把 multi-agent trading 从股票研究扩展到加密永续合约语境。
- 用确定性风险门控约束 LLM agent 的交易建议，避免把自然语言信心直接变成仓位。
- 对“AI 投研 + 可复核纸面交易 + 风险控制”路线有代表性。

## 风险边界

- README 明确声明 research only、not financial advice、paper results 不代表实盘。
- LLM analyst 可能出错，risk gate 也不能创造交易优势。
- 缺少链上数据，公开 Info API 的字段覆盖有限。
- fork 仍保留 upstream package 名称 `tradingagents`，集成时要注意命名和兼容性。

## 补充建议

- 后续观察是否能发布长期 paper trading leaderboard、回测基准和失败案例。
- 可与 `TradingAgents`、`Vibe-Research`、`ai-berkshire`、`daily_stock_analysis` 共同跟踪金融 agent 的证据边界。

## 参考资料

- GitHub: <https://github.com/PengZhang64/circuit-framework>
- Upstream TradingAgents: <https://github.com/TauricResearch/TradingAgents>
- TradingAgents paper: <https://arxiv.org/abs/2412.20138>
