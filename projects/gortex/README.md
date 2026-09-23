<!-- markdownlint-disable MD013 -->

# gortex（zzet/gortex）

- GitHub：<https://github.com/zzet/gortex>
- 抓取快照：2026-09-24，1,723 stars、162 forks、82 open issues
- 热度信号：GitHub Go Trending 抓取时约 +71 当日 stars
- 版本与许可：Apache-2.0；latest GitHub Release 为 `v0.64.5`

## 定位

Gortex 是面向 Coding Agent 与 IDE 的本地代码智能引擎，将多仓库源码解析为 symbol / dependency / dataflow / infrastructure graph，再通过 CLI、MCP Server、API 与 Web UI 暴露检索、影响分析、上下文和编辑验证能力。

## 用法

可下载单二进制或用 Homebrew 安装，先在 workspace 运行初始化 / index，再让 daemon 持久维护 SQLite graph；Agent 侧配置 MCP 后调用 symbol search、source、callers、usages、impact、smart context 等工具。可选 LSP / LLM enrichment、PR review 与 remote daemon 会接触网络，默认本地 indexing 路径不需要外部服务。

## 原理

Gortex 以 Tree-sitter 家族 parser 构造节点和 calls、imports、dataflow、test、infra、cross-repo 等 edges，SQLite 同时作为 graph store 与增量持久层。daemon 启动时按仓库变更选择 incremental、scoped 或 full retrack；MCP 查询从 graph、全文 / symbol ranking 与可选语义 enrichment 组合最小上下文。

## 价值

对于大代码库，它提供比逐文件 grep / read 更结构化的入口，并能在跨仓库 API、调用链、测试、配置和基础设施之间建立连接。单机 SQLite、默认关闭网络功能和可复现 benchmark harness 便于在受控环境评估真实 token / latency / recall 收益。

## 风险边界

- README 的 257 languages、50× token reduction、大仓库速度与内存数字是作者报告，依赖 parser 覆盖、硬件、repo 和 query，本轮未重跑。
- graph 是静态 / 增量近似；动态 dispatch、生成代码、宏、reflection、runtime config 与未支持 parser 可能产生漏边或错边。
- benchmark 部分有过时证据：daemon latency 明写来自已退役的 in-memory backend，SWE-bench 结果表仍为 `TBD`，不能写成 Agent 修复能力证明。
- 本地 graph 会集中源码结构、路径、notes、feedback 与可能的业务语义；remote daemon、LLM enrichment、forge review 和 model download 会改变数据边界。
- 自动编辑 / verify 工具仍以当前用户权限工作；检索命中和 graph impact 不能替代编译、测试、安全审查与人工验收。

## 补充建议

在目标 monorepo 建立一组真实 symbol、跨仓调用、动态语言和配置查询金标，记录 recall@k、token、冷 / 热索引时间、SQLite 大小与峰值内存。对每次升级固定 commit 与 parser 版本，并将 Gortex 输出和 `rg`、LSP、编译 / 测试结果做差分；敏感仓库默认关闭所有网络可选项。

## 参考资料

- [GitHub 仓库](https://github.com/zzet/gortex)
- [GitHub REST API](https://api.github.com/repos/zzet/gortex)
- [v0.64.5 Release](https://github.com/zzet/gortex/releases/tag/v0.64.5)
- [架构说明](https://github.com/zzet/gortex/blob/main/docs/architecture.md)
- [Benchmark 与限制](https://github.com/zzet/gortex/blob/main/BENCHMARK.md)
- [SWE-bench 待完成结果](https://github.com/zzet/gortex/blob/main/BENCHMARK-SWE.md)
- [LICENSE](https://github.com/zzet/gortex/blob/main/LICENSE.md)
