# AI-Trader（HKUDS/AI-Trader）

- GitHub: <https://github.com/HKUDS/AI-Trader>
- 核心定位：面向 AI Agent 的交易协作平台，提供信号发布、讨论、跟单与多市场接入。

## 1. 它解决什么问题

当前“AI 做交易”的落地难点包括：
- agent 能生成观点，但难以形成标准化执行链路；
- 策略讨论、复制交易、绩效追踪分散在多个系统；
- 新手缺少低风险试错环境。

`AI-Trader` 尝试把“agent 研究 + 交易协作 + 执行反馈”放到同一平台。

## 2. 快速使用（实践向）

```bash
git clone https://github.com/HKUDS/AI-Trader.git
cd AI-Trader
# 按 README/.env.example 配置运行环境
# 参考 skills/ 与 docs/ 完成 agent 接入或用户侧使用
```

落地建议：
- 先用 paper trading 验证策略，不要直接上真实资金；
- 交易信号与风险参数（仓位、止损）一起版本化管理；
- 分离“信号质量评估”和“执行质量评估”两条指标线。

## 3. 原理拆解（简化）

- Agent 接入层：通过 skill 指令快速接入不同 agent；
- 服务层：后端任务异步处理行情、结算、历史统计；
- 协作层：支持讨论、信号共享、跟单与社区反馈。

## 4. 为什么值得关注

- 把“agent-native”概念推进到强反馈行业（交易）；
- 同时覆盖研究、执行、评估三环节，具备平台化潜力；
- 对 AI + FinTech 社区有示范意义。

## 5. 风险与边界

- 市场风险：任何自动策略都可能在极端行情下失效；
- 合规风险：不同地区对自动化交易与荐股边界要求不同；
- 系统风险：信号同步与执行延迟会放大滑点与回撤。

## 6. 我的补充建议

- 增加“场景化回放”与极端行情压力测试；
- 对策略发布引入可解释摘要（核心假设、失效条件）；
- 分层权限：研究者、执行者、跟单者权限与责任边界分开。

## 7. 参考资料

- 官方仓库：<https://github.com/HKUDS/AI-Trader>
- 官方站点与 skill 文档（见 README）
- GitHub Trending：<https://github.com/trending>
