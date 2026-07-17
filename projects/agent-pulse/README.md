# agent-pulse

## 定位

`agent-pulse` 是一个证据驱动的 AI 行业情报项目，面向需要做判断而不只是“刷新闻”的读者。它把官方发布、论文、资本动作、政策变化和公开传播信号整理成可追溯 Events、行业判断和下一步观察信号。

截至 2026-07-18 抓取时，仓库约 `205` stars、`23` forks，主要语言为 TypeScript，许可证为 `MIT`。

## 用法

- 直接访问 GitHub Pages 站点查看 latest material shift、strategic views、evidence timeline、source activity、coverage and sources、Scout 等视图。
- 作为代码项目，它用 GitHub Actions 做数据刷新、source audit 和质量守门。
- 适合把公开 AI 行业信号整理成长期 evidence graph，而不是一次性日报。

## 原理

项目把来源目录、事件、判断和刷新流程拆开：allowlist 观察层负责收集，经过门槛后才形成公开 Event；行业判断只在证据变化时更新。README 强调每日刷新 public data，但 source audit、monitor 和 weekly brief 仍有不同频率和质量门槛。

## 价值

- 对 AI 行业情报工作流提供了“证据链优先”的开源样本。
- 把 source coverage、timeline 和 judgment 分离，有助于避免把单条消息误读成趋势。
- 与本仓库的每日热点日报目标高度相关，可作为后续改造日报结构的参考。

## 风险边界

- 公开来源覆盖必然不完整，尤其是社媒、闭门会议、付费报告和地区性信源。
- Scout 视图本身是 evidence-linked hypotheses，不应直接当事实或投资建议。
- 自动刷新不等于自动验证，仍需要人工抽查关键结论。

## 补充建议

- 本仓库后续可借鉴其 source activity / coverage 字段，为日报增加“可复核状态”和“证据等级”。
- 继续观察其 weekly brief 是否能长期稳定输出，而不是只在发布初期活跃。

## 参考资料

- GitHub: <https://github.com/barretlee/agent-pulse>
- Live site: <https://barretlee.github.io/agent-pulse/>
