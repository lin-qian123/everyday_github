<!-- markdownlint-disable MD013 -->

# Claude Quickstarts

> 更新：2026-10-19（Asia/Shanghai）。分类：AI 学习与教育资源。上游 `anthropics/claude-quickstarts`；本文基于官方榜单、认证 API 与文档 / 源码静态核验，未安装运行。源码快照 `9ec32b91df50`；Release 与主分支行为分别说明。热度见[当日官方榜单](https://github.com/trending/typescript?since=daily)。

## 定位

Anthropic 的应用参考实现集合，包含客服、财务数据可视化、computer / browser use、长时程 coding agent 及 Managed Agents 示例。每个子目录有独立依赖、认证与运行说明，不能当作同一套生产应用安装。[来源 1](https://github.com/anthropics/claude-quickstarts/blob/9ec32b91df50b0d4906cae64b13c6298055ff40d/README.md)

官方 TypeScript Trending 约 +453 当日 stars；API 为 18,621 / 3,183 / 228（stars / forks / open issues），无 GitHub Release / tag，根代码 MIT。[来源 2](https://api.github.com/repos/anthropics/claude-quickstarts)[来源 7](https://github.com/anthropics/claude-quickstarts/blob/9ec32b91df50b0d4906cae64b13c6298055ff40d/LICENSE)

## 用法

按想验证的能力只选一个子项目，先读其 README 再配置 Anthropic / 对应 provider 凭据。长时程 coding 示例可在一次性目录限制迭代数：[来源 3](https://github.com/anthropics/claude-quickstarts/blob/9ec32b91df50b0d4906cae64b13c6298055ff40d/autonomous-coding/README.md)

```bash
# 安装该子项目依赖、配置凭据后，在 autonomous-coding/ 中执行
python autonomous_agent_demo.py --project-dir ./demo-project --max-iterations 3
```

上游默认初始化 200 个 feature 测试项，完整过程可能耗时数小时；首次实验应缩小规格并记录费用。computer-use-demo 是 Linux Docker 桌面；computer-use-best-practices 原生操作 macOS，作者建议一次性 VM。两者不能混用权限假设。[来源 3](https://github.com/anthropics/claude-quickstarts/blob/9ec32b91df50b0d4906cae64b13c6298055ff40d/autonomous-coding/README.md)[来源 5](https://github.com/anthropics/claude-quickstarts/blob/9ec32b91df50b0d4906cae64b13c6298055ff40d/computer-use-demo/README.md)[来源 6](https://github.com/anthropics/claude-quickstarts/blob/9ec32b91df50b0d4906cae64b13c6298055ff40d/computer-use-best-practices/README.md)

本轮没有安装 SDK、调用模型、启动桌面或部署任何 bot。

## 原理

各示例展示应用 harness：准备上下文和工具 → 调用模型 → 执行工具 → 回传结果 → 继续或结束。autonomous-coding 将 initializer 与后续 coding sessions 分开，以 feature_list.json 和 Git 保存进展；新 session 的上下文依赖这些产物重建。[来源 3](https://github.com/anthropics/claude-quickstarts/blob/9ec32b91df50b0d4906cae64b13c6298055ff40d/autonomous-coding/README.md)

其 client 显式配置 SDK sandbox、项目目录 permissions 和 Bash PreToolUse hook；computer-use 则通过截图 / GUI 动作循环操作桌面。配置存在是静态事实，不能等同于本轮已经验证隔离。[来源 4](https://github.com/anthropics/claude-quickstarts/blob/9ec32b91df50b0d4906cae64b13c6298055ff40d/autonomous-coding/client.py)[来源 5](https://github.com/anthropics/claude-quickstarts/blob/9ec32b91df50b0d4906cae64b13c6298055ff40d/computer-use-demo/README.md)

## 价值

适合学习完整应用中怎样接工具、处理会话、持久状态和检查结果，比孤立 API 片段更接近集成工作。不同子项目便于对照桌面、浏览器和托管 Agent 的职责；示例完整度不能替代自己的错误处理与验收。

## 风险边界

- API 账户、模型 token、云服务和 Managed Agents 有各自费用与数据边界；参考实现的 MIT 不覆盖外部服务条款。
- computer-use-demo 明示 Agent loop 与被控容器分隔较弱，单 session 使用，必要时重启 / 重置；网页和图片里的注入可导致错误行动。需一次性环境和无敏感登录态。[来源 5](https://github.com/anthropics/claude-quickstarts/blob/9ec32b91df50b0d4906cae64b13c6298055ff40d/computer-use-demo/README.md)
- macOS best-practices 的 sandboxed shell 不会自动收窄桌面 GUI 已获的 Accessibility / Screen Recording 权限；trajectory 会保存 transcript 与图片，应单独治理留存。[来源 6](https://github.com/anthropics/claude-quickstarts/blob/9ec32b91df50b0d4906cae64b13c6298055ff40d/computer-use-best-practices/README.md)
- coding hook 放行 npm、node、git 等开发工具；命令白名单不是对任意依赖脚本行为的证明，仍需实际 SDK sandbox 与网络约束。[来源 4](https://github.com/anthropics/claude-quickstarts/blob/9ec32b91df50b0d4906cae64b13c6298055ff40d/autonomous-coding/client.py)
- Managed Agents 示例可能发送 Slack / Linear 消息或操作远端资源。阅读或运行 quickstart 不应隐含授予这些外部写入权限；需限定测试账户和动作范围。[来源 1](https://github.com/anthropics/claude-quickstarts/blob/9ec32b91df50b0d4906cae64b13c6298055ff40d/README.md)

## 补充建议

以一次性仓库和 mock 工具做一条最小流程，验成功、超时、失败恢复、重复 webhook、权限拒绝及最终产物。保留 SDK / 模型 / toolset 版本和费用；feature 标为 pass 后，还需独立检查产物与真实需求。computer use 的 shell、浏览器和桌面权限分开验证。

## 参考资料

1. [可选 Quickstarts](https://github.com/anthropics/claude-quickstarts/blob/9ec32b91df50b0d4906cae64b13c6298055ff40d/README.md)
2. [仓库 API](https://api.github.com/repos/anthropics/claude-quickstarts)
3. [Autonomous Coding 运行说明](https://github.com/anthropics/claude-quickstarts/blob/9ec32b91df50b0d4906cae64b13c6298055ff40d/autonomous-coding/README.md)
4. [SDK client 与权限配置](https://github.com/anthropics/claude-quickstarts/blob/9ec32b91df50b0d4906cae64b13c6298055ff40d/autonomous-coding/client.py)
5. [Computer Use Demo 与安全边界](https://github.com/anthropics/claude-quickstarts/blob/9ec32b91df50b0d4906cae64b13c6298055ff40d/computer-use-demo/README.md)
6. [原生 macOS 参考实现](https://github.com/anthropics/claude-quickstarts/blob/9ec32b91df50b0d4906cae64b13c6298055ff40d/computer-use-best-practices/README.md)
7. [LICENSE](https://github.com/anthropics/claude-quickstarts/blob/9ec32b91df50b0d4906cae64b13c6298055ff40d/LICENSE)
