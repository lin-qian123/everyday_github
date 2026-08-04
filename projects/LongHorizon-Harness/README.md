# LongHorizon-Harness

- 仓库：[AMAP-ML/LongHorizon-Harness](https://github.com/AMAP-ML/LongHorizon-Harness)
- 快照：2026-08-05 抓取；GitHub API 显示其创建于 2026-08-04，约 173 stars、12 forks，MIT。数字会随时间变化。
- 分类：Agent 框架与技能生态

## 定位

面向长时程 computer-use 与终端任务的 agent harness。项目将管理、执行与审计分为独立角色，试图让跨桌面应用和 CLI 的任务在上下文刷新后仍保留已验证状态。

## 用法

按仓库说明安装后，以 `lh-harness run --task @task.md --agent ...` 启动任务；需要 GUI 操作时再显式传入兼容的 computer-use MCP 配置。先用隔离目录、测试账户和可逆任务验证，再接触真实工作区或远端主机。

## 原理

Manager 保存目标、已验证进展和下一步；Executor 每轮使用新上下文完成一个具体子任务；Auditor 独立检查文件、接口、日志和测试。只有通过审计的结果写入持久状态，失败则保留既有证据并继续处理剩余项。

## 价值

把“能做一次”与“可恢复、可审计地完成长任务”分开，适合需要跨工具、跨轮次交付的自动化。仓库还声明支持多 agent backend 与本地、SSH、Docker 等环境，便于比较不同执行边界。

## 风险边界

三角色架构不会自动限制 MCP 工具、凭据、网络或 GUI 权限；审计质量也取决于真实验收脚本。README 中的 benchmark/增益是项目主张，本页未独立复现；外接 computer-use server 可能扩大可操作面。

## 补充建议

先把任务验收写成可机读检查，并给 Manager 状态文件做版本控制；Auditor 应运行独立命令而非复述 Executor 输出。对 SSH、浏览器、支付和生产系统设最小权限、审批点与紧急停止。

## 参考资料

- [项目 README](https://github.com/AMAP-ML/LongHorizon-Harness)
- [项目论文](https://arxiv.org/abs/2608.01964)
- [GitHub API 元数据快照](https://api.github.com/repos/AMAP-ML/LongHorizon-Harness)
