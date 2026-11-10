<!-- markdownlint-disable MD013 -->

# Claude Quickstarts

> 更新：2026-11-11（Asia/Shanghai）。分类：AI 学习与教育资源。上游 `anthropics/claude-quickstarts`；本文基于官方榜单、认证 API 与文档 / 源码静态核验，未安装运行。源码快照 `4a4224bdf0e9`；Release 与主分支行为分别说明。仓库 ID `849553306`。热度见[当日官方榜单](https://github.com/trending?since=daily)。

## 定位

Anthropic 的应用参考实现集合，包含客服、财务数据可视化、computer / browser use、长时程 coding agent 及 Managed Agents 示例。每个子目录有独立依赖、认证与运行说明，不能当作同一套生产应用安装。[来源 1](https://github.com/anthropics/claude-quickstarts/blob/4a4224bdf0e9cfb3332167b69c90457403813625/README.md)

官方综合及 Python Trending 为 +530 当日 stars；API 为 20,464 / 3,468 / 241（stars / forks / open issues，含 PR），发行列表为空，根代码 MIT。[来源 2](https://api.github.com/repos/anthropics/claude-quickstarts)[来源 7](https://github.com/anthropics/claude-quickstarts/blob/4a4224bdf0e9cfb3332167b69c90457403813625/LICENSE)

## 用法

按想验证的能力只选一个子项目，先读其 README 再配置 Anthropic / 对应 provider 凭据。长时程 coding 示例可在一次性目录限制迭代数：[来源 3](https://github.com/anthropics/claude-quickstarts/blob/4a4224bdf0e9cfb3332167b69c90457403813625/autonomous-coding/README.md)

```bash
# 安装该子项目依赖、配置凭据后，在 autonomous-coding/ 中执行
python autonomous_agent_demo.py --project-dir ./demo-project --max-iterations 3
```

上游默认初始化 200 个 feature 测试项，完整过程可能耗时数小时；首次实验应缩小规格并记录费用。computer-use-demo 是 Linux Docker 桌面；computer-use-best-practices 原生操作 macOS，作者建议一次性 VM。两者不能混用权限假设。[来源 3](https://github.com/anthropics/claude-quickstarts/blob/4a4224bdf0e9cfb3332167b69c90457403813625/autonomous-coding/README.md)[来源 5](https://github.com/anthropics/claude-quickstarts/blob/4a4224bdf0e9cfb3332167b69c90457403813625/computer-use-demo/README.md)[来源 6](https://github.com/anthropics/claude-quickstarts/blob/4a4224bdf0e9cfb3332167b69c90457403813625/computer-use-best-practices/README.md)

本轮没有安装 SDK、调用模型、启动桌面或部署任何 bot。

新增路线可选 Knowledge Wiki：Python ≥3.11、anthropic SDK ≥2.0，需 Managed Agents beta 权限；先读取 notebook 的已记录输出，再决定是否下载 SEC 资料和执行付费构建。上游仅记录 core 档，换语料 / 档位前清空旧输入目录，固定文件清单；运行记录默认写系统临时目录，需要留证时另设 `COOKBOOK_RECORDS_DIR`。[Wiki 运行说明](https://github.com/anthropics/claude-quickstarts/blob/4a4224bdf0e9cfb3332167b69c90457403813625/managed-agents/knowledge-wiki/README.md)

## 原理

各示例展示应用 harness：准备上下文和工具 → 调用模型 → 执行工具 → 回传结果 → 继续或结束。autonomous-coding 将 initializer 与后续 coding sessions 分开，以 feature_list.json 和 Git 保存进展；新 session 的上下文依赖这些产物重建。[来源 3](https://github.com/anthropics/claude-quickstarts/blob/4a4224bdf0e9cfb3332167b69c90457403813625/autonomous-coding/README.md)

其 client 显式配置 SDK sandbox、项目目录 permissions 和 Bash PreToolUse hook；computer-use 则通过截图 / GUI 动作循环操作桌面。配置存在是静态事实，不能等同于本轮已经验证隔离。[来源 4](https://github.com/anthropics/claude-quickstarts/blob/4a4224bdf0e9cfb3332167b69c90457403813625/autonomous-coding/client.py)[来源 5](https://github.com/anthropics/claude-quickstarts/blob/4a4224bdf0e9cfb3332167b69c90457403813625/computer-use-demo/README.md)

Knowledge Wiki 在一次动态工作流中分批提取、解决缺口并整理 Markdown memory store，再为每个问题以只读方式挂载；事实保留来源，口径冲突和被替代数字继续标注。Daily Brief 则以只读 preferences、可写 state、来源 bookmarks 与重复 ledger 组织定期汇总，无法读取的来源明确报告受限。[Wiki](https://github.com/anthropics/claude-quickstarts/blob/4a4224bdf0e9cfb3332167b69c90457403813625/managed-agents/knowledge-wiki/README.md) / [Daily Brief](https://github.com/anthropics/claude-quickstarts/blob/4a4224bdf0e9cfb3332167b69c90457403813625/managed-agents/daily-brief/README.md)

## 价值

适合学习完整应用中怎样接工具、处理会话、持久状态和检查结果，比孤立 API 片段更接近集成工作。不同子项目便于对照桌面、浏览器和托管 Agent 的职责；示例完整度不能替代自己的错误处理与验收。

知识库路线适合变化较慢、反复查询的语料；可以比较一次构建成本与每问检索成本。作者的基准声称每问成本约为大模型直接检索的 1/15，但约 $19 平均建库成本、约 240 问盈亏平衡依赖其语料、评分和当时计价，不能外推为当前价格或普遍收益，本轮未复跑。[作者实验范围](https://github.com/anthropics/claude-quickstarts/blob/4a4224bdf0e9cfb3332167b69c90457403813625/managed-agents/knowledge-wiki/README.md)

## 风险边界

- API 账户、模型 token、云服务和 Managed Agents 有各自费用与数据边界；参考实现的 MIT 不覆盖外部服务条款。
- computer-use-demo 明示 Agent loop 与被控容器分隔较弱，单 session 使用，必要时重启 / 重置；网页和图片里的注入可导致错误行动。需一次性环境和无敏感登录态。[来源 5](https://github.com/anthropics/claude-quickstarts/blob/4a4224bdf0e9cfb3332167b69c90457403813625/computer-use-demo/README.md)
- macOS best-practices 的 sandboxed shell 不会自动收窄桌面 GUI 已获的 Accessibility / Screen Recording 权限；trajectory 会保存 transcript 与图片，应单独治理留存。[来源 6](https://github.com/anthropics/claude-quickstarts/blob/4a4224bdf0e9cfb3332167b69c90457403813625/computer-use-best-practices/README.md)
- coding hook 放行 npm、node、git 等开发工具；命令白名单不是对任意依赖脚本行为的证明，仍需实际 SDK sandbox 与网络约束。[来源 4](https://github.com/anthropics/claude-quickstarts/blob/4a4224bdf0e9cfb3332167b69c90457403813625/autonomous-coding/client.py)
- Managed Agents 示例可能发送 Slack / Linear 消息或操作远端资源。阅读或运行 quickstart 不应隐含授予这些外部写入权限；需限定测试账户和动作范围。[来源 1](https://github.com/anthropics/claude-quickstarts/blob/4a4224bdf0e9cfb3332167b69c90457403813625/README.md)

- Knowledge Wiki 文档主动披露共享页面并发覆盖：最繁忙实体页约 5% 已写入行丢失，单 store 文件上限 100 KB。引用来源和只读查询不能补回构建时已丢内容；大页需拆分并核完整性。[已知限制](https://github.com/anthropics/claude-quickstarts/blob/4a4224bdf0e9cfb3332167b69c90457403813625/managed-agents/knowledge-wiki/README.md)
- Wiki 的真实 SEC 文件未随仓库提供，两个辅助文件明确为合成数据；不可把该混合样例当成全真实资料上的独立研究结果。Office 解析与远端 store 上传另有输入 / 数据边界。[语料组成](https://github.com/anthropics/claude-quickstarts/blob/4a4224bdf0e9cfb3332167b69c90457403813625/managed-agents/knowledge-wiki/README.md)
- Daily Brief 的 Slack bot 能向其加入的频道发消息，目标频道限制主要是 prompt 规则；文档建议将读源与写目标拆成两个 app。$5 单次预算触顶会暂停，外观上的静默需查运行状态，不能解释为当天没有事项。[权限与失败状态](https://github.com/anthropics/claude-quickstarts/blob/4a4224bdf0e9cfb3332167b69c90457403813625/managed-agents/daily-brief/README.md)

## 补充建议

以一次性仓库和 mock 工具做一条最小流程，验成功、超时、失败恢复、重复 webhook、权限拒绝及最终产物。保留 SDK / 模型 / toolset 版本和费用；feature 标为 pass 后，还需独立检查产物与真实需求。computer use 的 shell、浏览器和桌面权限分开验证。

对 Wiki 追加逐源事实清单、冲突保留、并发前后行数 / 哈希和引用回指检查；分别记建库、更新、查询成本与准确率，验证换档后无旧资料混入。Daily Brief 另验重复事件、不可读来源、预算暂停与凭据撤权。

## 参考资料

1. [可选 Quickstarts](https://github.com/anthropics/claude-quickstarts/blob/4a4224bdf0e9cfb3332167b69c90457403813625/README.md)
2. [仓库 API](https://api.github.com/repos/anthropics/claude-quickstarts)
3. [Autonomous Coding 运行说明](https://github.com/anthropics/claude-quickstarts/blob/4a4224bdf0e9cfb3332167b69c90457403813625/autonomous-coding/README.md)
4. [SDK client 与权限配置](https://github.com/anthropics/claude-quickstarts/blob/4a4224bdf0e9cfb3332167b69c90457403813625/autonomous-coding/client.py)
5. [Computer Use Demo 与安全边界](https://github.com/anthropics/claude-quickstarts/blob/4a4224bdf0e9cfb3332167b69c90457403813625/computer-use-demo/README.md)
6. [原生 macOS 参考实现](https://github.com/anthropics/claude-quickstarts/blob/4a4224bdf0e9cfb3332167b69c90457403813625/computer-use-best-practices/README.md)
7. [LICENSE](https://github.com/anthropics/claude-quickstarts/blob/4a4224bdf0e9cfb3332167b69c90457403813625/LICENSE)
8. [Knowledge Wiki：动态工作流与限制](https://github.com/anthropics/claude-quickstarts/blob/4a4224bdf0e9cfb3332167b69c90457403813625/managed-agents/knowledge-wiki/README.md)
9. [Daily Brief：状态、权限与失败处理](https://github.com/anthropics/claude-quickstarts/blob/4a4224bdf0e9cfb3332167b69c90457403813625/managed-agents/daily-brief/README.md)
