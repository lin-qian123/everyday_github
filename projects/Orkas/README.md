<!-- markdownlint-disable MD013 -->

# Orkas

## 定位

Orkas 是本地优先的桌面 AI 团队工作台。Commander 将目标拆为 to-do，协调内置 16 个专业 Agent，也能接入已安装的 Claude Code、Codex、OpenCode、OpenClaw 和 Hermes。它围绕项目、文档、媒体产物、定时自动化和连接器组织工作。

2026-10-31 采样：JavaScript daily +1,000 stars；API 累计 4,908 stars / 286 forks / 7 open issues（含 PR）。核读 main `31169370acee`；发行 API 首项 [v2026.10.27](https://github.com/Orkas-AI/Orkas/releases/tag/v2026.10.27)，2026-10-27 UTC。以下区分作者文档与有限源码核读，未做上游运行验收。

## 用法

macOS / Windows 有打包安装器，Linux 当前走源码；源码要求 Node `>=22.12`，Linux 要 glibc 2.34+。阅读固定 README 后，在单独 checkout 启动：

```bash
git clone https://github.com/Orkas-AI/Orkas.git
cd Orkas
./run.sh
```

Windows 使用 `run.cmd`。首启会准备 npm 树、Python / uv / Node、embedding、OfficeCLI、FFmpeg 与语音模型等资源，并建立本地工作区。先配置模型 / OAuth，再建测试项目、给出产物验收标准；源码运行路径与打包应用账号 / 云功能分开。本轮未运行上述命令。

## 原理

Commander 通过 `dispatch_to`、`hand_off_to` 和 `run_worker` 分别委派具名 Agent、交接剩余任务或运行匿名子任务；会话锁、并发和预算限制约束执行。项目记忆、Agent 经验、对话历史和 Library 文档索引各有范围，Library 使用本地 embedding 与 SQLite 向量索引。后台复盘可更新经验与技能，仍需审阅其修改。

## 价值

把编码、调研和 Office / 媒体交付放在同一工作区，适合有反复交接与跨天产物的个人 / 小团队。是否能保留文档可编辑性、提高质量或降低成本，需要固定任务对照；“任务已派发”不能作完成证据。

## 风险边界

- MIT 覆盖应用代码，模型、素材、外部 CLI 与随附组件另核。内置模型额度不等于长期免成本，具体套餐不在本页固化。
- README 的本地优先需结合具体路径：自备 key 调 provider，内置模型和麦克风识别可用 Orkas 服务，可选云同步 / 共享项目会存选定数据到服务器；官网另披露有限使用 analytics。本轮没有抓包或验证离线模式。
- 上游称 key 本地加密并排除云同步；这不能代替主机、备份与当前用户权限保护，也不能证明文档 / 对话从不外发。
- 静态核读外部 CLI 审批桥：无 renderer 或超时会拒绝；但 `full_access` 对原生 CLI 文件 / shell 操作自动允许，连接器仍有独立审批。应核每个 Agent 的实际策略，不由“有审批弹窗”推断全部操作逐次询问。
- 内置 bash 的任务授权为内存态、按身份 / 会话 / Agent 约束，与外部 CLI 协议不同。后台复盘、自动推进和定时作业会持续动作，权限与停止条件必须可见。

## 补充建议

选一份报告、一段短视频和一个代码修复做验收：回读文件、核引用、检查源文件可编辑性和导出效果。再测任务取消、断线重连、审批拒绝、后台学习 diff 和云同步选择；分别计内置 / 自备模型成本及人工返工。

## 参考资料

- [上游仓库](https://github.com/Orkas-AI/Orkas)、[仓库 API](https://api.github.com/repos/Orkas-AI/Orkas)。
- [README.md](https://github.com/Orkas-AI/Orkas/blob/31169370aceebd6a4bd49d92ea2a900a867529ee/README.md)。
- [LICENSE](https://github.com/Orkas-AI/Orkas/blob/31169370aceebd6a4bd49d92ea2a900a867529ee/LICENSE)。
- [package.json](https://github.com/Orkas-AI/Orkas/blob/31169370aceebd6a4bd49d92ea2a900a867529ee/package.json)。
- [src/main/features/local_agents/cli_permissions.ts](https://github.com/Orkas-AI/Orkas/blob/31169370aceebd6a4bd49d92ea2a900a867529ee/src/main/features/local_agents/cli_permissions.ts)。
- [src/main/model/core-agent/bash-permissions.ts](https://github.com/Orkas-AI/Orkas/blob/31169370aceebd6a4bd49d92ea2a900a867529ee/src/main/model/core-agent/bash-permissions.ts)。
- [官网安全与数据说明](https://orkas.ai/security/?source=gh-orkas)。
