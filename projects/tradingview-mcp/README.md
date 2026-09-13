<!-- markdownlint-disable MD013 -->

# TradingView MCP Bridge（tradesdontlie/tradingview-mcp）中文解读

> 证据快照：2026-09-14（Asia/Shanghai）。GitHub REST API 显示 6,166 stars、2,674 forks、245 open issues，没有 GitHub Release；API 许可证字段为 `NOASSERTION`，根 `LICENSE` 是 MIT，并附加 TradingView 关联、商标、数据与条款声明。根 `package.json` 为 `1.0.0`。README 称 78 个 MCP tools，`RESEARCH.md` 写 84 个，工具数量应以固定 commit 的实际 server 清单为准。本文未安装、未开启 TradingView debug port、未读取行情或执行任何图表操作。

## 定位

TradingView MCP Bridge 通过 Chrome DevTools Protocol（CDP）连接用户本机的 TradingView Desktop，把图表读取、Pine Script 编译、指标、绘图、提醒、回放与截图暴露为 MCP 和 `tv` CLI。目标是让 Claude Code 等 agent 能观察并操作现有金融图表界面。

它不是 TradingView 官方项目，也不是交易机器人。上游明确要求有效订阅，声明不绕过付费墙且不执行真实交易；Replay 交易只是模拟。任何投资结论仍由用户负责。

## 用法

基础流程是安装依赖、以 CDP 调试模式启动 TradingView，再把 server 加入 MCP 配置：

```bash
git clone https://github.com/tradesdontlie/tradingview-mcp.git
cd tradingview-mcp
npm install
./scripts/launch_tv_debug_mac.sh
node src/cli/index.js status
```

MCP 配置将 `node /path/to/tradingview-mcp/src/server.js` 注册为本地 server。先用 `tv_health_check` / `tv status` 只读验证，再考虑 symbol、timeframe、drawing 或 alert 等写操作。

## 原理

- TradingView Desktop 以 `--remote-debugging-port=9222` 启动，bridge 连接 Electron/Chromium 的 CDP endpoint。
- 工具从页面内部状态提取 quote、OHLCV、indicator、Pine line/label/table/box 等结构化数据，也可截图供视觉分析。
- 通过小粒度工具和 `CLAUDE.md` 决策树控制 context；上游研究笔记称紧凑默认输出可把一次分析从约 80 KB 降到 5–10 KB，但这是项目自述。
- Pine 工作流把写入源码、编译、读取错误与修复组成循环；stream 命令以 JSONL 轮询本地应用状态。
- draw、alert、layout、tab 和 replay 等工具会改变界面状态；真实行情持续变化，agent 响应可能在完成推理前已过时。

## 价值

- 将复杂桌面金融 UI 转成结构化、可组合的 agent 工具，减少纯截图操作的脆弱性。
- Pine Script 的 compile→error→fix 回路适合保留明确工具结果和可回读状态。
- CLI 与 JSON 输出便于把相同动作接入人工脚本、日志和回归测试。
- `RESEARCH.md` 主动记录 temporal consistency、tool granularity 和 human-in-the-loop 等开放问题，方便评估而非只看功能清单。

## 风险边界

- CDP debug port 是高权限控制面；若绑定或转发不当，同机进程或网络访问者可能读取/操作登录中的桌面应用。
- README 所说“本地处理”描述 bridge 自身；如果 tool result、截图或 prompt 交给云模型，相关内容仍可能离开本机。
- 使用未公开的 TradingView 内部 API，任意桌面更新都可能破坏 selector、数据含义和写操作；README 与研究文档的工具数量已不一致。
- 行情会变化，LLM 可能误读指标、忽略延迟或生成 repainting Pine Script；不得用自然语言流畅度替代价格、时间戳和代码回测。
- 程序化消费市场数据、提醒和界面自动化可能受 TradingView 条款、数据许可和当地金融规则约束；MIT 只覆盖本仓库源码。
- 245 个 open issues 是维护负担信号，不等于缺陷率；项目没有正式 release，默认分支也不能视为稳定 API。

## 补充建议

1. 使用专用 TradingView profile、测试 watchlist 与 loopback-only debug port；不要暴露 9222 或真实券商凭据。
2. 先固定 Desktop、仓库 commit、symbol、timeframe 与历史区间，做只读 golden-state 回读和截图比对。
3. 将 chart mutation、alert、Pine save 与 replay action 分级，默认要求人工确认并记录前后状态。
4. 投资研究输出必须带行情时间戳、数据来源、延迟与非投资建议声明；禁止连接真实下单链路。

## 参考资料

- GitHub：<https://github.com/tradesdontlie/tradingview-mcp>
- GitHub REST API：<https://api.github.com/repos/tradesdontlie/tradingview-mcp>
- README：<https://github.com/tradesdontlie/tradingview-mcp/blob/main/README.md>
- 研究笔记：<https://github.com/tradesdontlie/tradingview-mcp/blob/main/RESEARCH.md>
- `package.json`：<https://github.com/tradesdontlie/tradingview-mcp/blob/main/package.json>
- LICENSE：<https://github.com/tradesdontlie/tradingview-mcp/blob/main/LICENSE>
- 作者 X：<https://x.com/Tradesdontlie>
