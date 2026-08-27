<!-- markdownlint-disable MD013 -->

# OpenBB

> 上游仓库：[OpenBB-finance/OpenBB](https://github.com/OpenBB-finance/OpenBB) · 归类：办公、商业与行业应用 · 本页基于 2026-08-28 的上游 README、许可证文件与 GitHub API 快照整理。

## 定位

OpenBB Open Data Platform（ODP）是面向分析师、量化人员和 AI agent 的金融数据集成层。它把专有、授权和公共数据源接入统一接口，再向 Python、OpenBB Workspace、Excel、MCP server 和 REST API 等表面提供数据。GitHub Python Trending 当日页面显示约 58 个当日 stars；API 快照为 72,384 stars、7,466 forks、108 个开放 issue，2026-08-27 有仓库活动。API 的 SPDX 字段为 `NOASSERTION`，但仓库 `LICENSE` 与 README 说明为 AGPLv3；数据源、插件和下游服务还需单独审查条款。

## 用法

最短的 Python 使用路径是：

```sh
pip install openbb
```

```python
from openbb import obb

output = obb.equity.price.historical("AAPL")
df = output.to_dataframe()
print(df.tail())
```

需要 API 服务或更多 provider 时，按官方文档配置数据源和依赖：

```sh
pip install "openbb[all]"
openbb-api
```

上游示例会在 `127.0.0.1:6900` 启动 FastAPI 服务；接入 Workspace、MCP 或 agent 前，先确认 provider 凭据、调用范围、缓存和日志策略。这里的示例只展示数据访问，不构成投资建议或交易信号。

## 原理

- provider 适配器把不同金融数据源的认证、请求、字段和异常转换为统一的 ODP 接口。
- 同一份数据可以通过 Python、CLI、Workspace、Excel、REST 和 MCP 暴露，形成“连接一次、到处消费”的集成层。
- AI agent 通过工具或 MCP 调用数据端点，再由上层模型生成摘要、筛选、比较或研究面板；模型并不自动提高原始数据的准确性。
- 时间范围、市场、单位、币种、公司 corporate actions、交易日历和数据延迟等语义由 provider 和查询参数共同决定。
- Workspace 与 agent integration 属于不同表面；连接器、OAuth/API key、权限和数据保留策略需分别配置和审计。

## 价值

- 减少为每个数据源重复实现认证、请求和字段适配的工作。
- 为量化脚本、研究 dashboard、Excel 用户和 agent 提供一致的数据入口。
- 适合构建可追溯的行情查询、公司研究、宏观数据分析和内部研究工具原型。
- 开源 provider/extension 机制便于团队增加领域数据源或内部接口，但也把许可证和数据质量责任带给集成方。

## 风险边界

- 数据的实时性、完整性、修订、企业行动、历史回填和许可范围取决于具体 provider；“统一 API”不等于统一质量或统一授权。
- 金融数据被 agent 摘要后可能出现单位、时间、币种、公司实体和因果关系错误；必须回到原始字段、时间戳和 provider 文档复核。
- API key、OAuth、MCP server、Workspace 连接器和 REST 服务会扩大数据出口；不要把交易账户或敏感研究数据直接暴露给默认 agent 工具链。
- AGPLv3 可能对网络服务、修改和再分发产生合规义务；插件、数据源和企业 Workspace 还可能有额外商业条款。
- 仓库提供数据访问能力，不是投资顾问、交易执行器或收益保证；自动下单必须有独立风险门、额度和人工确认。

## 补充建议

1. 用公开或沙盒 provider 固定一个查询，记录请求参数、响应时间、数据时间戳、字段定义和原始响应，再接入 agent。
2. 对每个 provider 建立许可、速率限制、费用、地域、保留期和失败回退清单；密钥使用最小权限环境变量。
3. 将“原始数据—确定性计算—模型解释—人工结论”分层保存，避免把生成文本当作数据事实。
4. 先做只读研究和 paper trading，禁用真实交易写权限；发布服务前单独完成 AGPL、数据许可、审计日志和访问控制审查。

## 参考资料

- [上游 README / ODP 架构](https://github.com/OpenBB-finance/OpenBB)
- [OpenBB Python 文档](https://docs.openbb.co/python/installation)
- [Python API 参考](https://docs.openbb.co/python/reference)
- [Agents for OpenBB](https://github.com/OpenBB-finance/agents-for-openbb)
- [仓库许可证](https://github.com/OpenBB-finance/OpenBB/blob/develop/LICENSE)
- [GitHub API 元数据](https://api.github.com/repos/OpenBB-finance/OpenBB)
