<!-- markdownlint-disable MD013 MD034 -->

# Memoh：为每个 Agent 提供持久工作区的多智能体平台

> 上游仓库：https://github.com/felinics/Memoh · 归类：记忆层与个人 AI 基础设施 · 本页基于 2026-09-19 的中英文 README、deployment / codebase map、release、LICENSE 与 REST API 静态整理；未部署 Cloud 或自托管栈，也未验证 workspace 隔离强度。

## 定位

Memoh 是一个面向长期运行个人与团队 Agent 的控制面。每个 Bot 可以拥有文件系统、终端、浏览器、桌面、网络、长期记忆、MCP、定时任务和外部渠道，并可运行内置 Agent、Claude Code、Codex 或自定义 ACP Agent。它与普通聊天前端的区别，是把会话、执行工作区和渠道接入作为持续在线资源管理。

2026-09-19 的 GitHub 官方 Go Trending 抓取显示约 `+35 stars today`；REST API 快照为 `2,499 stars / 236 forks / 58 open issues`，AGPL-3.0。最新 release 为 `v0.20.0`（9 月 15 日）。

## 用法

可直接使用 Memoh Cloud，或自托管完整服务：

```sh
git clone --depth 1 --recurse-submodules --shallow-submodules https://github.com/felinics/Memoh.git
cd Memoh
cp conf/app.docker.toml config.toml
export MEMOH_INTERNAL_RPC_SHARED_SECRET="$(openssl rand -hex 32)"
docker compose up -d
```

上游也提供 `curl -fsSL https://memoh.sh | sh` 安装入口。生产部署前应审阅脚本和 Compose、固定镜像 digest，并妥善保存内部 RPC shared secret；官方说明不应对整个安装脚本直接使用 `sudo`。

## 原理

- Go Server 负责用户、Bot、thread、memory、tool approval、workspace、connector、channel 与 schedule；Channel 可内嵌或以 shared-secret RPC 拆成独立进程。
- 每个 Bot 可拥有独立 workspace container，用于文件编辑、命令执行、MCP 托管以及可选的 headed Chrome / VNC 桌面。
- 容器内 bridge 通过 Unix Domain Socket 与 host 通信；workspace backend 抽象支持 Docker、containerd 与 Apple runtime，snapshot / storage 语义并不完全一致。
- 长期记忆组合 Qdrant、BM25 与 LLM extraction；Telegram、Discord、飞书、微信、Web UI、Email 和 webhook 形成多渠道入口。
- Connect It 子项目保存 SaaS 凭据并暴露统一 MCP connector；Supermarket / Apps 安装 skills、workspace dependencies 与 connectors。
- 代码图谱文档明确资源配额、JWT / OAuth、tool approval、workspace network 与 gRPC 生命周期是独立子系统。

## 价值

- 将对话、长期记忆、执行环境和渠道身份放在同一个 Bot 生命周期中，适合持续在线而非一次性 CLI 任务。
- 每 Bot workspace 和资源配额比多个 Agent 共享宿主目录更容易建立租户、文件和执行边界。
- Cloud 与自托管两条路径、AGPL 源码和多个 runtime backend 便于团队评估可控性与运营成本。
- 内置外部 Coding Agent、浏览器、桌面和连接器，降低自行拼接消息总线、容器与 memory 的集成成本。

## 风险边界

- “每个 Agent 一台电脑”在开源实现中主要是 workspace container，不应直接写成 microVM 或强多租户隔离；Docker、containerd 与 Apple backend 的安全属性不同。
- workspace 具有网络、浏览器、终端、文件与 connector 权限，prompt injection 可跨越聊天进入真实 SaaS 与外部渠道。
- Cloud、自托管模型 provider、IM、Email、webhook 和 MCP 都可能产生数据外发；self-hosted control plane 不等于所有内容留在本机。
- 安装脚本、Supermarket app、workspace dependency、镜像与 Agent CLI 更新形成多层供应链；每 Bot 独立并不自动验证安装内容。
- 源码文档曾记录生产会话触发 8 GiB OOM 的背景，并保留生产规模回归未完成项；资源预算仍需按本地版本实测。
- 本页未验证 RLS、容器逃逸、网络 egress、credential isolation、备份恢复、memory 删除或跨渠道身份一致性。

## 补充建议

1. 先在两测试用户、两个 Bot、无生产凭据的环境验证 workspace 文件 / 网络 / memory / channel 隔离，并做 prompt injection 对抗。
2. 固定镜像、submodule 与依赖 revision；对 Supermarket app、connector 和 workspace dependency 做签名、allowlist 与人工审批。
3. 默认关闭公网 egress 和未使用渠道，为 browser、terminal、MCP 与 SaaS connector 分别配置最小权限和短期凭据。
4. 建立资源限额、审计、备份 / 恢复、memory 删除和账号撤销演练；Cloud 与自托管方案分别画出完整数据流。

## 参考资料

- 上游 README：https://github.com/felinics/Memoh
- `v0.20.0` release：https://github.com/felinics/Memoh/releases/tag/v0.20.0
- 部署说明：https://github.com/felinics/Memoh/blob/main/DEPLOYMENT.md
- 代码结构与 workspace 边界：https://github.com/felinics/Memoh/blob/main/docs/codebase-map.md
- GitHub REST API：https://api.github.com/repos/felinics/Memoh
- LICENSE：https://github.com/felinics/Memoh/blob/main/LICENSE
