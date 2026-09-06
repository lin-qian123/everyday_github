<!-- markdownlint-disable MD013 -->

# AutoHedge（The-Swarm-Corporation/AutoHedge）

> 记录日期：2026-09-07（Asia/Shanghai）。本页依据上游 README、源码目录、LICENSE 与 GitHub REST API 做静态整理；本轮未安装包、未连接钱包或交易所、未回测，也未执行任何真实或模拟交易。

## 定位

`AutoHedge` 是把交易研究、量化分析、风险管理和执行拆成多 agent 流水线的金融自动化项目。上游当前声明支持 Solana 全自动交易，Coinbase 和其他中心化交易所仍在 roadmap。

2026-09-07 的 GitHub 官方综合/Python Trending 抓取显示约 `+137 stars today`；REST API 快照为 `4,684 stars / 774 forks / 17 open issues`。仓库 API 识别许可证为 MIT；没有 GitHub release，最新 push 停在 2026-05-11。

## 用法

上游提供 PyPI 安装和最小命令入口：

```bash
pip install -U autohedge
autohedge
```

配置涉及 Jupiter API key、可选模型 provider key 与 `WALLET_PRIVATE_KEY`。安全评估只能在隔离环境、测试钱包和无真实资金的 paper/simulation 路径中进行；不要把主钱包私钥写入未经审计的 `.env`。

## 原理

- **Director Agent**：生成策略方向与交易 thesis。
- **Quant Agent**：处理技术和统计分析，为 thesis 提供量化输入。
- **Risk Management Agent**：在执行前给出仓位和风险约束。
- **Execution Agent**：把上游结果转换为订单或交易输出。
- **外部数据与模型**：通过 Jupiter 获取代币价格/搜索，并可接 OpenAI、Anthropic 等 provider。
- **结构化与日志**：README 声称使用 JSON 输出和详细日志，便于下游集成与审计。

## 价值

- 将研究、风控与执行职责显式分层，便于替换策略或在中间加入人工 gate。
- 结构化输出可以用于 paper trading、回放和规则验证，而不必直接接真实钱包。
- MIT 代码适合阅读多 agent 金融流水线的基本组织方式。
- README 直接列出当前 venue 与 roadmap，有助于区分已声明支持和未来计划。

## 风险边界

- “enterprise-grade”“risk-first”与“autonomous hedge fund”是上游定位，不是收益、可靠性、监管合规或机构级控制的独立证据。
- 仓库没有公开 release，且最新 push 距本次观察约四个月；Trending 热度不能抵消维护、依赖或安全时效风险。
- LLM 交易 thesis、agent 互相验证和风险角色都可能一致性失败；角色数量不是独立风险控制。
- 钱包私钥、provider key、RPC 与交易权限构成高价值攻击面；prompt injection、依赖供应链、日志泄露或配置错误可能直接产生资金损失。
- 滑点、MEV、流动性、费用、延迟、链上拥堵、报价过期和失败重试都会让研究结论与成交结果偏离。
- 金融、税务、牌照、受托义务和市场操纵规则因地区与用途而异；开源许可证不授予金融业务许可。

## 补充建议

- 先把 execution adapter 替换为不可联网的 mock，保存相同行情快照并做可重复回放。
- 建立确定性硬风控：最大仓位、最大日损、token allowlist、滑点、价格时效、交易频率和全局 kill switch，不让 LLM 覆盖。
- 使用新建、低余额、可撤销权限的测试钱包；私钥放硬件或专用签名服务，agent 只提交受限交易提案。
- 分别记录信号时间、报价时间、签名时间、上链时间与成交回执，避免把回测价格写成真实成交。
- 在任何真实资金前完成依赖锁定、secret scan、威胁建模、长时间 paper trading 与人工审批；若无独立收益/风险证据则保持研究用途。

## 参考资料

- [GitHub 仓库](https://github.com/The-Swarm-Corporation/AutoHedge)
- [GitHub REST API](https://api.github.com/repos/The-Swarm-Corporation/AutoHedge)
- [README](https://github.com/The-Swarm-Corporation/AutoHedge/blob/main/README.md)
- [源码目录](https://github.com/The-Swarm-Corporation/AutoHedge/tree/main/autohedge)
- [MIT License](https://github.com/The-Swarm-Corporation/AutoHedge/blob/main/LICENSE)
