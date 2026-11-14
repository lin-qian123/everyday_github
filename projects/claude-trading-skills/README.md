<!-- markdownlint-disable MD013 -->

# Claude Trading Skills

- 上游：[tradermonty/claude-trading-skills](https://github.com/tradermonty/claude-trading-skills)
- 分类：办公、商业与行业应用。
- 核验：2026-11-15（Asia/Shanghai）；仓库 ID `1079356098`，固定主线 `fdfff010e1efe181ebe9c11a0109ef5f8b736147`；release 列表为空，项目清单的 `0.1.0` 不代表已有可下载稳定发行。
- 证据范围：官方 API、固定 SHA 文档、工作流及仓位脚本相关段落的静态核读；未安装技能、调用模型 / 行情服务、连接券商、回测或下单。

## 定位

面向时间有限的个人投资者，将市场复盘、风险检查、候选筛选、计划、记录和事后复盘组织成技能与工作流。上游明确以长期持有 / ETF / 股息组合为核心、纪律化波段为补充；它是教育和研究流程工具，不承诺收益，也不把买卖判断交给 AI。[README](https://github.com/tradermonty/claude-trading-skills/blob/fdfff010e1efe181ebe9c11a0109ef5f8b736147/README.md)

这里评估的是工程组织方式，不提供投资建议，也没有证据证明使用这些技能能获得超额收益。

## 用法

1. 先按任务选择 `workflows/` 清单，逐项核实必需技能、输入和人工决策点。上游明确 `skills-index.yaml` 是技能元数据权威入口，工作流以对应 YAML 为准。
2. Claude Code 用户可把单个已审核技能目录复制到项目 `.claude/skills/`；Web 用户采用对应源目录打包路径。README 提供 release 安装入口，但本次 API 无发行，不能声称现成资产和校验清单已发布。
3. 初步可选公开 CSV / 截图与本地记录路径；“不需付费行情 API”仍需要外部数据，Agent 本身也可能使用云模型。Alpaca、FMP、FINVIZ 等要求由具体工作流决定。

例如，只查看仓位计算器的接口：

```bash
python skills/position-sizer/scripts/position_sizer.py --help
```

该命令为源仓库内的使用示例，本轮未执行。共享开发环境声明 `>=3.11.5,<3.14`，单独打包技能保留 Python 3.9 源码下限；根项目环境、某个脚本与跨平台 CI 支持不能混为一谈。[清单](https://github.com/tradermonty/claude-trading-skills/blob/fdfff010e1efe181ebe9c11a0109ef5f8b736147/pyproject.toml)、[发布兼容策略](https://github.com/tradermonty/claude-trading-skills/blob/fdfff010e1efe181ebe9c11a0109ef5f8b736147/docs/dev/release-compatibility.md)

## 原理

工作流 YAML 把每步绑定一个技能，并声明输入制品、输出、依赖和 `decision_gate`。例如 `market-regime-daily` 先分析市场宽度和上涨参与度，可选 FMP 顶部风险步骤，最后给 exposure posture 并要求人工复核；约 15 分钟是作者的流程估计，不是本轮计时。[工作流说明](https://github.com/tradermonty/claude-trading-skills/blob/fdfff010e1efe181ebe9c11a0109ef5f8b736147/workflows/README.md)、[日常市场清单](https://github.com/tradermonty/claude-trading-skills/blob/fdfff010e1efe181ebe9c11a0109ef5f8b736147/workflows/market-regime-daily.yaml)

仓位技能组合固定风险、ATR 或 Kelly 方法与集中度约束；抽读脚本可见使用 Decimal 向下取整，并选更严格的持仓限制。计算器不请求实时行情，但实际生成 JSON / Markdown 报告，因此“纯计算”不等于没有文件写入。[技能定义](https://github.com/tradermonty/claude-trading-skills/blob/fdfff010e1efe181ebe9c11a0109ef5f8b736147/skills/position-sizer/SKILL.md)、[脚本](https://github.com/tradermonty/claude-trading-skills/blob/fdfff010e1efe181ebe9c11a0109ef5f8b736147/skills/position-sizer/scripts/position_sizer.py)

## 价值

可复用之处是“先检查风险、明确输入来源、留下决策与复盘制品”的流程约束，适合研究和教学中审查 AI 输出的来源与假设。人工关卡和可读清单有助于发现缺数据或越权，但仍需宿主真正执行这些限制。

项目的元数据 / 工作流兼容策略也值得借鉴：源技能、包和工作流应来自同一提交或发行，不能把最新文档与旧 `.skill` 包混用。

## 风险边界

1. **流程门控不是券商权限控制。** `decision_gate: true` 和提示词要求不会自动限制宿主 MCP / API 权限。涉及 Alpaca 等连接时，另核纸面 / 实盘环境、token scope 和账户边界；本轮未连接任何账户。
2. **方法正确不等于执行或收益成立。** 输入的价格时间、拆股 / 复权口径、缺失行情与模型推断会影响结果。仓位公式与止损价也不能保证成交价格或最大实际损失；回测、示例和 AI 报告不能证明未来收益。
3. **无行情 key 不等于离线。** 公开 CSV 仍有来源与时效要求，截图可被误读，模型请求及账户持仓材料可能出本机；本地 YAML 记录另需备份与访问控制。
4. **维护自动化具有额外副作用。** 贡献者工具的 dry-run 仍可写日志、状态和报告；正常流程可能调用 Claude、修改技能、提交、推送和开 PR。周度挖掘会把会话派生信号与限长用户消息送入模型，不能描述为“原始文件在本机所以全程本地”。launchd 包装器还会在专用 checkout 执行 reset / clean。[自动化边界](https://github.com/tradermonty/claude-trading-skills/blob/fdfff010e1efe181ebe9c11a0109ef5f8b736147/docs/dev/skill-automation.md)
5. **开发快照与稳定发行分开。** 兼容表目前仅有 Unreleased；发布策略提到首个 1.0.0 仍依赖待办。本次只确认该静态说明和空 release 列表，没有据此逐一复核所有关联 issue。
6. 根许可 MIT，行情、券商、模型和第三方内容仍有独立条款；README 中的价格、账户可用性与监管表述未作为本页核实结论。[许可](https://github.com/tradermonty/claude-trading-skills/blob/fdfff010e1efe181ebe9c11a0109ef5f8b736147/LICENSE)

## 补充建议

以虚构或脱敏数据演练单一流程，固定整个提交，保留数据日期、输入缺失、报告和人工决定。先检验每一步是否真实满足输入与门控，再评估方法；不要用技能数量、GitHub stars 或报告排版代替收益证据。

初次使用只安装所需技能，维护者的自改进、会话挖掘和排程另作选择。对输出 JSON / Markdown、日志与记忆一起设置保存和清理策略。

## 参考资料

- [仓库 API](https://api.github.com/repos/tradermonty/claude-trading-skills)、[发行列表](https://github.com/tradermonty/claude-trading-skills/releases)。
- [固定 README](https://github.com/tradermonty/claude-trading-skills/blob/fdfff010e1efe181ebe9c11a0109ef5f8b736147/README.md)、[项目环境](https://github.com/tradermonty/claude-trading-skills/blob/fdfff010e1efe181ebe9c11a0109ef5f8b736147/pyproject.toml)、[MIT 许可](https://github.com/tradermonty/claude-trading-skills/blob/fdfff010e1efe181ebe9c11a0109ef5f8b736147/LICENSE)。
- [工作流说明](https://github.com/tradermonty/claude-trading-skills/blob/fdfff010e1efe181ebe9c11a0109ef5f8b736147/workflows/README.md)、[市场流程](https://github.com/tradermonty/claude-trading-skills/blob/fdfff010e1efe181ebe9c11a0109ef5f8b736147/workflows/market-regime-daily.yaml)、[仓位定义](https://github.com/tradermonty/claude-trading-skills/blob/fdfff010e1efe181ebe9c11a0109ef5f8b736147/skills/position-sizer/SKILL.md)、[仓位脚本](https://github.com/tradermonty/claude-trading-skills/blob/fdfff010e1efe181ebe9c11a0109ef5f8b736147/skills/position-sizer/scripts/position_sizer.py)。
- [发布兼容](https://github.com/tradermonty/claude-trading-skills/blob/fdfff010e1efe181ebe9c11a0109ef5f8b736147/docs/dev/release-compatibility.md)、[维护自动化](https://github.com/tradermonty/claude-trading-skills/blob/fdfff010e1efe181ebe9c11a0109ef5f8b736147/docs/dev/skill-automation.md)。
