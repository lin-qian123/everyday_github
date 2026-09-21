<!-- markdownlint-disable MD013 MD034 -->

# Crucix：聚合多源 OSINT 的本地个人情报终端

> 上游仓库：https://github.com/calesthio/Crucix · 归类：RAG、检索与知识处理 · 本页基于 2026-09-22 的 README、配置、许可证与 REST API 静态整理；未配置数据源、运行 sweep、验证告警或使用其交易想法。

## 定位

Crucix 将火情、航班、辐射、卫星、经济指标、市场、冲突、制裁、新闻与社交来源汇入同一 dashboard，按周期计算变化与跨源信号，并可选接入 LLM、Telegram / Discord 生成摘要和告警。它更像自托管 OSINT 聚合与监控工作台，不是权威情报源、金融终端或自动交易系统。

2026-09-22 的 GitHub 官方 JavaScript Trending 抓取显示约 `+37 stars today`；REST API 快照为 `11,837 stars / 1,840 forks / 79 open issues`，AGPL-3.0，无 GitHub Release，默认分支最后 push 为 2026-05-20。高关注回潮不等于近期代码更新。

## 用法

上游要求 Node.js 22+；不配置 key 也可使用部分公开源：

```sh
git clone https://github.com/calesthio/Crucix.git
cd Crucix
npm install
cp .env.example .env
npm run dev
```

Dashboard 默认位于 `http://localhost:3117`，首次 sweep 据 README 通常需 30--60 秒；Docker Compose 会把运行结果持久化到 `./runs/`。FRED、NASA FIRMS、EIA、ACLED、AIS、LLM 与消息机器人各有独立凭据和条款。

## 原理

- orchestrator 并行调用 27 个 source module，统一 timeout、retry、错误与结构化输出。
- 每轮结果与上次 snapshot 比较，形成新信号、升级 / 降级和 source health；浏览器通过 SSE 收到刷新。
- dashboard 用平面地图 / 3D globe 呈现地理信号，并合并 ticker、市场、辐射、太空与 OSINT 流。
- LLM 可生成交易想法并给 alert 分层；不可用时退回确定性规则，数据采集本身不依赖 LLM。
- Telegram / Discord bot 支持 `/brief`、`/sweep`、`/status` 等双向命令，因而同时是远程控制面。

## 价值

- 把分散开放数据的抓取、健康状态、变化检测与地理展示放进可自托管工作流。
- source 失败会结构化暴露，OpenSky 429 等情况下保留最近非空快照，比静默缺数更易诊断。
- 可选 LLM 与 rule fallback 分离，便于对“原始事实”和“模型解释”做分层审计。
- AGPL-3.0 与少量核心依赖方便审查，但实际数据权利仍由每个上游源决定。

## 风险边界

- README 的“zero cloud”只可理解为应用可本地托管；27 个外部 feed、LLM provider、Telegram / Discord 和公开 demo 都会产生网络与第三方数据流。
- OSINT 可能延迟、重复、误报、缺失或被对抗性内容污染；跨源相关和 LLM 置信度不是事实证明。
- trade idea、市场行情与冲突告警不是投资建议、应急指令或经过验证的专业情报产品。
- bot token、provider key、portfolio 与历史运行文件是高敏感资产；开放 dashboard / webhook 会扩大泄露和远程触发面。
- 默认分支数月未更新且没有 release；动态 API、模型名和源格式可能已经漂移，本页未运行验证。

## 补充建议

1. 先关闭 LLM、portfolio 与双向 bot，只对少量非敏感公开源建立 freshness / failure / duplicate 基线。
2. 为每条 signal 保存来源 URL、抓取时间、原始字段和转换规则；模型摘要与交易想法必须单独标层。
3. 用专用低权限 token、只绑定 loopback、反向代理鉴权，并对 `/sweep` 等远程命令做速率限制和审计。
4. 对高后果新闻至少回到两个独立一手来源人工确认，不让单个 Telegram / RSS / LLM 结果自动触发行动。

## 参考资料

- 上游 README：https://github.com/calesthio/Crucix
- Live demo：https://crucix.live
- X 上游账号：https://x.com/crucixmonitor
- GitHub REST API：https://api.github.com/repos/calesthio/Crucix
- LICENSE：https://github.com/calesthio/Crucix/blob/master/LICENSE
