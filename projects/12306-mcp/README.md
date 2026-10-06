<!-- markdownlint-disable MD013 -->

# 12306 MCP（Joooook/12306-mcp）

> 上游仓库：<https://github.com/Joooook/12306-mcp> · 归类：办公、商业与行业应用 · 本页基于 2026-10-07 的 GitHub API、README、原理 / 架构文档、package manifest 与 LICENSE 静态整理，未向 12306 发起查询、登录账号或尝试购票。

- 抓取快照：2,230 stars、325 forks、10 open issues。
- 热度信号：GitHub JavaScript Trending 抓取时约 +310 当日 stars；最后 push 为 2026-07-31，属于旧项目重新上榜。
- 版本与许可：Release / tag / npm manifest 均为 `v0.3.10` / `0.3.10`，MIT；本页固定审计 commit `ff6439da6f63`。

## 定位

12306 MCP 是让大模型查询中国铁路车站、余票、中转和经停信息的 MCP server。它把公开查询数据包装为工具调用，方便自然语言规划行程；它不是中国铁路官方产品，也不负责账号登录、下单、支付或出票。

## 用法

上游支持 `npx -y 12306-mcp@0.3.10` 的 stdio 模式，也可指定端口启动 HTTP 模式，运行时要求 Node.js 18+。更稳妥的接入方式是固定版本、优先 stdio、只授权查询类工具，并让用户在 12306 官方渠道重新确认日期、车次、席别、价格和余票后自行购票。

## 原理

服务启动时从 12306 首页定位车站数据脚本，构建车站 code、城市和名称映射；MCP 的基础工具负责日期与车站编码，核心工具再调用余票 `/otn/leftTicket/query`、中转 `/lcquery/queryU` 与经停 `/otn/czxx/queryByTrainNo` 等接口，格式化为模型可读文本。架构是 LLM → MCP server → 查询 API，不包含交易闭环。

## 价值

项目把自然语言中的城市、日期、车次筛选拆成明确的工具步骤，比让模型直接猜时刻表更可审计；同时提供 stdio、HTTP 和 Docker 路径，便于个人行程助手或教学演示接入。

## 风险边界

- 这是第三方学习项目，不能把输出当 12306 官方承诺；余票、价格、临时调整与列车状态随时变化，关键决策必须回到官方页面 / App。
- 查询接口与页面结构可能变更，频繁自动请求还受服务条款、限流与反自动化机制约束；不应绕过验证、压测或扩大抓取。
- 项目只查询，不完成预订；Agent 不得声称“已锁票 / 已购票”，也不能替用户处理身份证、联系人、Cookie 或支付信息。
- HTTP 模式扩大网络面，README 未把它描述成面向公网的认证服务；应优先 stdio 或只绑定 loopback，并加反向代理认证与速率限制。
- 模型对“后天”、多站同城、中转与车次过滤的理解可能错误；工具返回成功也不等于行程可达、换乘时间合理或无障碍需求满足。
- `npx -y` 的浮动版本会扩大供应链变化；应固定 `0.3.10`、核验 npm provenance，并分别审计代码依赖与外部 12306 数据条款。

## 补充建议

用固定日期和合成车站 fixture 测日期边界、多站城市、跨日、中转、无座与空结果；所有面向用户的回答附查询时间与“请在官方渠道确认”。若启用 HTTP，只在 loopback / 私网运行，禁止保存身份信息和 Cookie，并对每个 tool 设置请求频率、超时和最大返回量。

## 参考资料

- [GitHub 仓库](https://github.com/Joooook/12306-mcp)
- [GitHub REST API](https://api.github.com/repos/Joooook/12306-mcp)
- [README 与安装说明](https://github.com/Joooook/12306-mcp/blob/main/README.md)
- [服务原理](https://github.com/Joooook/12306-mcp/blob/main/docs/principle.md)
- [架构说明](https://github.com/Joooook/12306-mcp/blob/main/docs/architecture.md)
- [package.json](https://github.com/Joooook/12306-mcp/blob/main/package.json)
- [v0.3.10 Release](https://github.com/Joooook/12306-mcp/releases/tag/v0.3.10)
- [MIT License](https://github.com/Joooook/12306-mcp/blob/main/LICENSE)
