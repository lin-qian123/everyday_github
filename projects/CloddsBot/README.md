<!-- markdownlint-disable MD013 -->

# CloddsBot（alsk1992/CloddsBot）中文解读

> 证据快照：2026-09-11（Asia/Shanghai）。GitHub REST API 显示 1,605 stars、253 forks、30 open issues，MIT；最新 release 与根 package 均为 `v1.9.0` / `1.9.0`。项目上游称它在 12 天 hackathon 周期内构建，本文未安装、回测或连接任何真实交易账户，不构成投资建议。

## 定位

CloddsBot 是一个把 LLM、消息渠道、预测市场、加密资产现货/永续合约、链上 DEX、策略、风险控制和自动化放进同一 gateway 的个人 AI 交易终端。用户可以从 WebChat、Telegram、Discord 等入口用自然语言查询行情、管理 portfolio，甚至触发真实下单、token launch、copy trading 和多钱包操作。

它的能力面很宽，但“可连接 1000+ 市场”“118+ strategies”是功能目录，不是收益、稳健性或监管合规证据。

## 用法

上游给出 Node.js 22+ 的全局安装路径：

```bash
npm install -g clodds --loglevel=error
clodds onboard
```

向导会配置模型 key、消息渠道并启动本地 gateway，WebChat 默认位于 `http://localhost:18789/webchat`。源码安装需要 `ANTHROPIC_API_KEY`；真实交易还要提供交易所凭据或 `SOLANA_PRIVATE_KEY`。安全起见，首次只能使用 paper trading、testnet、只读 API key 或空钱包。

## 原理

- gateway 统一 HTTP/WebSocket、消息渠道、认证和限流，把自然语言任务送入 Claude 为主的多 provider agent 层。
- 策略与风险层组合行情、arbitrage、whale/copy signals、position manager、VaR/CVaR、Kelly sizing、daily loss limit、circuit breaker 与 kill switch。
- SQLite 保存消息与交易记录，LanceDB 支持 semantic memory，PostgreSQL 可用于 analytics；每笔决策可写入 trade ledger。
- 交易适配器覆盖预测市场、CEX、Solana/EVM DEX 和 on-chain perps；另有外部 Compute API、agent forum、USDC escrow marketplace 和 token-launch surface。

## 价值

- 将分散的行情、策略、风险与执行接口组织为可查询、可审计的统一终端。
- 交易 ledger、回测入口、限额和 kill switch 为研究型 agent 提供比“模型直接下单”更可检查的控制点。
- 多渠道与本地存储便于在同一操作面查看状态，但仍需要强身份隔离。
- 对开发者而言，它是 agent 如何连接高后果金融工具、钱包和支付协议的高密度案例。

## 风险边界

- 这是能执行真实资产操作的高后果软件。LLM 错误、prompt injection、市场滑点、链上 MEV、合约漏洞、流动性不足或 API 失效都可能造成不可逆损失。
- 上游列出最高 200x leverage、copy trading、多钱包 swarm、token launch 和 72 小时 escrow auto-release；任何一个都不适合以默认自动化开启。
- 自报的 sandbox、AES-256-GCM、75 条扫描规则与风险模型未由本页独立审计。加密数据库仍依赖主密钥管理、进程权限、日志和备份安全。
- 文档称本地 gateway 默认端点可无认证；一旦 reverse proxy、消息 webhook 或公网入口配置错误，交易能力可能暴露。
- backtest、VaR/CVaR、Kelly sizing 与 arbitrage 检测不保证 future returns，也不覆盖所有尾部、制度、交易所或智能合约风险。
- 不同司法辖区对预测市场、衍生品、token launch、KYC、税务和自动交易的要求不同，开源许可不等于可合法使用。

## 补充建议

1. 将 research、proposal、approval 和 execution 分成不同进程/凭据；默认只读，真实下单必须 human-in-the-loop。
2. 使用独立低余额测试账户、无提现 key、IP allowlist、单笔/单日硬上限和外部 kill switch，绝不把主钱包 seed phrase 交给 agent。
3. 用冻结行情与已知答案回放策略，记录手续费、滑点、失败重试和 survivor bias，再做 testnet/paper 阶段。
4. 独立审计依赖、postinstall、消息渠道、数据库备份、webhook 签名和交易适配器，并按所在地咨询合规专业人士。

## 参考资料

- GitHub：<https://github.com/alsk1992/CloddsBot>
- GitHub REST API：<https://api.github.com/repos/alsk1992/CloddsBot>
- Releases：<https://github.com/alsk1992/CloddsBot/releases>
- 用户指南：<https://github.com/alsk1992/CloddsBot/blob/main/docs/USER_GUIDE.md>
- 交易说明：<https://github.com/alsk1992/CloddsBot/blob/main/docs/TRADING.md>
- 安全审计文档：<https://github.com/alsk1992/CloddsBot/blob/main/docs/SECURITY_AUDIT.md>
- LICENSE：<https://github.com/alsk1992/CloddsBot/blob/main/LICENSE>
