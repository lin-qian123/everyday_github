<!-- markdownlint-disable MD013 -->

# Scion（GoogleCloudPlatform/scion）中文解读

> 上游仓库：<https://github.com/GoogleCloudPlatform/scion> · 归类：Agent 框架与技能生态 · 证据快照：2026-10-17（Asia/Shanghai）。API：1,925 stars / 286 forks / 107 open issues；无 GitHub Release；tags 首项 `v0.3.0-preview.3`；main go.mod `1.26.1`；Apache-2.0；并非正式支持的 Google 产品。本页为上游资料与相关代码的静态整理，未安装运行、复测性能或完成全面安全审计。

## 定位

Scion 是 GoogleCloudPlatform 下的多 Agent 协作编排基础设施，可为 Claude Code、Codex、Antigravity、OpenCode 等 harness 配置身份、凭据与运行环境。它从本机 Workstation 延伸到 hosted Hub、Runtime Broker 和多种容器 / 云运行时，是 pre-1.0 的协作试验与工程平台。

## 用法

先选本机 Workstation 模式，用测试仓库和专用模型凭据开始。README 推荐的是社区 homebrew-scion tap，安装还包括 Telegram broker plugin，需审阅来源与镜像 registry；也可依官方安装文档从源码构建。运行 `scion server start` 在 localhost:8080 onboarding 检测 runtime，再在项目中 `scion init`、`scion start my-agent "Your task here"`。先单 Agent 验日志、停止与恢复，再增加协作。

## 原理

- Hub 管理身份、状态和调度，Runtime Broker 负责在 Docker / Podman / Apple Container / Kubernetes 等环境供应 worker；受支持的 managed agent 可使用 provider API。
- agent template 组合指令、skills、harness 配置与独立凭据；目录可共享，也可按任务用 worktree / clone。
- agents 用 CLI 通信、委派和报告；web、chat connectors、日志 / metrics 提供人类观察面，Skill Bank 和 A2A 扩展协作接口。

## 价值

将运行环境、消息、身份和可见性放在统一控制面，便于研究真实协作中的任务所有权、恢复和人工介入。它提供实验基础设施；团队数量、可视化或作者演示都不能直接证明吞吐、科学发现或产出质量提升。

## 风险边界

- 容器 / worktree 的隔离效果取决于 mount、network、runtime、共享目录和凭据；Hub / Broker 具有高信任权限，需按运行模式审阅。
- 安全文档将 agent role 区分 none / readonly / baseline / full；full 涉及 secret、service-account 与子 Agent 管理，不能无差别赋权。
- 文档特别说明 `server.auth.agent_run_scope=observe` 时 run_id 不匹配只记录、尚不因此拒绝请求；应区分观测与强制策略，不能把 token run_id 当成已强制撤销边界。
- 社区分发、cloud resources、chat connectors 和外部 skill registry 引入独立供应链、费用及数据出口；接口在 pre-1.0 仍会变，README 声明无正式 Google 产品支持。

## 补充建议

从单机和最低角色起步，分别测试越权拒绝、旧 token、停止 / 恢复、共享文件冲突和失败任务清理。固定 CLI、镜像与 harness 版本；增加 hosted Hub 前再核对 TLS、身份、broker 注册、secret scope、账单与审计保留。

## 参考资料

- 上游仓库：<https://github.com/GoogleCloudPlatform/scion>
- GitHub REST API：<https://api.github.com/repos/GoogleCloudPlatform/scion>
- README / 模式与安装：<https://github.com/GoogleCloudPlatform/scion/blob/main/README.md>
- 身份与权限安全参考：<https://github.com/GoogleCloudPlatform/scion/blob/main/docs-site/src/content/docs/reference/security.md>
- Go 版本：<https://github.com/GoogleCloudPlatform/scion/blob/main/go.mod>
- 许可：<https://github.com/GoogleCloudPlatform/scion/blob/main/LICENSE>
- Releases：<https://github.com/GoogleCloudPlatform/scion/releases>
