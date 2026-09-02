<!-- markdownlint-disable MD013 MD034 -->

# Sequoia-X：基于规则策略与本地行情库的 A 股自动选股系统

## 项目概览

- 上游仓库：https://github.com/sngyai/Sequoia-X
- GitHub API 快照（2026-09-03）：6,020 stars、1,243 forks、22 个开放 issue
- 当前 release：未发布 GitHub Release；默认分支最近 push 为 2026-07-10
- 主要技术：Python、baostock、SQLite、向量化规则策略、飞书 Webhook
- 许可证：README 声明 MIT；仓库无独立 LICENSE 文件，GitHub API 未识别 SPDX

## 定位

Sequoia-X 是面向 A 股的日线规则选股系统：从 baostock 获取后复权 K 线，保存到本地 SQLite，收盘后运行六类技术形态策略，并把候选结果推送到飞书。

它是研究与信号筛选工具，不是券商交易接口、收益保证或经审计的投资顾问系统。当前公开说明没有提供独立样本外回测、交易成本、停牌/涨跌停可成交性或实盘结果。

## 用法

项目要求 Python 3.10+，支持 `uv sync` 或 `pip install .`。配置飞书 Webhook 后先回填历史数据，再日常增量运行：

```bash
python main.py --backfill
python main.py
```

上游建议在交易日收盘后通过 cron 自动执行。首次试用应关闭真实群推送，在固定日期和本地副本上生成候选 CSV / 日志，先核对复权、缺失值与策略实现。

## 原理

数据引擎并行拉取全市场历史和增量日 K，使用后复权价格写入 SQLite。策略层以独立类实现海龟突破、均线放量、高窄旗形、涨停洗盘、上升趋势跌停反包与 RPS 突破，入口汇总并推送结果。

这些规则编码的是候选形态，不包含自动交易、组合优化或完整风险模型。策略名称和历史图形也不能证明未来超额收益。

## 价值

- 数据、策略与通知分层清晰，适合阅读和扩展日线选股规则。
- baostock + SQLite 降低个人研究的行情接入和增量存储门槛。
- 多个经典技术形态集中在统一框架，便于做横向回测与消融。
- 属性测试、类型和工程化配置为继续补充质量 gate 提供基础。

## 风险边界

- 选股信号不是投资建议；没有样本外、成本后和风险调整证据时不能宣称有效策略。
- 后复权、幸存者偏差、未来函数、停复牌、ST、涨跌停和数据修订都会显著影响回测。
- README 的“2~3 分钟”“12 分钟”是上游环境描述，不是本轮实测，也不代表数据完整。
- 飞书 Webhook 是可写外部凭据，日志、`.env`、群权限和消息误发需要保护。
- README 写 MIT，但根目录没有独立 LICENSE 文件且 API 为未识别；复用代码前应先向上游确认许可文本。
- 本页只做静态资料核验，未运行数据回填、策略、回测或实盘。

## 补充建议

1. 固定行情截止日，检查股票池、复权、缺失交易日、退市与停牌处理，再建立可重放数据快照。
2. 采用 walk-forward / 时间切分与严格无未来函数测试，报告交易成本、换手、回撤和基准差异。
3. 将候选生成、人工研究与真实下单完全分离，默认不连接券商和真实通知群。
4. 给飞书 Webhook 设置专用低权限群、密钥轮换和日志脱敏，测试重复推送与失败重试。
5. 在分发、商用或大段复用前，要求上游补充独立 LICENSE 文件并明确版权主体。

## 参考资料

- 仓库与 README：https://github.com/sngyai/Sequoia-X
- GitHub API：https://api.github.com/repos/sngyai/Sequoia-X
- baostock：https://www.baostock.com/
- 策略目录：https://github.com/sngyai/Sequoia-X/tree/master/sequoia_x/strategy
- 测试目录：https://github.com/sngyai/Sequoia-X/tree/master/tests
