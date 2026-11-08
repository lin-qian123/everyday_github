<!-- markdownlint-disable MD013 -->

# Agentero（poco-ai/Agentero）中文解读

> 上游：[poco-ai/Agentero](https://github.com/poco-ai/Agentero) · 分类：RAG、检索与知识处理 · 核验：2026-11-09，仓库 ID 1291896819，主线 SHA `1c6152d3020fff23e31f0e5580a3d519fb7731c2`。本页为文档与抽样源码静态核读，未安装运行、登录或调用模型 / 云资源。

## 定位

面向人与 agent 协作的科研桌面工作台，把 PDF 阅读、结构化正文、笔记、检索与写作集中在 Vault。通过 ACP 接入自己安装的 agent，也可经 MCP / CLI 操作文献库。稳定发行 v0.15.2；当前主线 package.json 为 0.15.3，二者不能直接视为同一制品。

## 用法

从官方发行下载匹配平台的安装包；macOS 也可 `brew tap poco-ai/agentero` 后 `brew install --cask agentero`。官方文档列 macOS 12.0+、Linux Ubuntu 22.04+ / webkit2gtk 4.1。先创建单独测试 Vault，导入少量公开论文，检查正文、公式和引用再接入 agent。

首次阅读不要求先安装 Zotero 或 agent。AI 功能采用 BYOA：CLI 自己安装 / 登录 / 持有模型 Key，Agentero 在 Vault 根启动 ACP 命令。默认权限为受限，自动精读默认关闭；第一次可选择每次询问并检查写入 Diff。

## 原理

Tauri 2 + React 19 前端连接 Rust Host；PDF、Markdown、JSON 等文件与 Catalog SQLite 一起构成工作区。Vault 下有 `papers/`、`notes/`、`.agents/`、`AGENTS.md` 及 `.agentero/catalog.sqlite`，不是“完全没有数据库”。

结构化正文供 agent 使用，阅读器保留 PDF 视觉上下文；v0.15.2 加入实验记录表格的稳定行 ID / 修订校验、Markdown 源码视图、翻译缓存与写入冲突修复。远程 Vault / SSH、S3、MCP 属于另行配置的数据和权限通路。

## 价值

减少论文、笔记和对话上下文的搬运；标准文件有利于人工复核和外部编辑。实验表格与修订号有望让人和 agent 共用可检查的记录，但不自动构成科研数据合规、实验复现或结论正确性的保证。

## 风险边界

- 本地存储与本地 ACP 不保证推理全离线；agent 自己的云模型、在线翻译、推荐 embedding、可选 OCR / 同步都会形成独立出口。
- v0.15.2 发行及当前 settings 实现默认腾讯交互翻译、正文解析 local；内置 provider 文档仍写注入 Key 时默认内置翻译 / embedding，口径有滞后，需以实际版本和保存设置核对。官方包可包含内置网关凭据，免填 Key 不代表离线或二进制密钥不可提取。
- 遥测需同时满足 release 构建、编译期 PostHog Key、用户开关；开关默认 true，关闭下次启动生效。本地活动始终落盘，关闭遥测不等于停止本机记录；主动反馈是单独通路。入门文档仍称本地记录可关，与遥测文档和隐私 UI 不一致。
- README 的“上下文准确无误”“不使用私有数据库”不能作为验收结论；需核双栏、表格、公式 / 页码、翻译与 PDF 原文，Catalog SQLite 也须备份。
- Skills 是外部指令，工作区信任 / 受限权限与真实进程隔离分别验证；自动安装 / 卸载 agent 可能改用户级包与目录。代码 MIT，第三方组件与模型服务条款另核。

## 补充建议

先用 Vault 副本核导入、别名 / 跨库复制、标注、修改冲突及恢复，再迁移完整 Zotero 库。备份整个 Vault 连同 catalog.sqlite，另外审本机 usage / 会话 / 缓存。逐个列出模型、翻译、OCR、MCP、SSH、S3 和遥测的数据出口，再决定开启哪些能力；所有科研结论回到原论文与原始数据。

## 参考资料

- [上游](https://github.com/poco-ai/Agentero)、[仓库 API](https://api.github.com/repos/poco-ai/Agentero)、[v0.15.2](https://github.com/poco-ai/Agentero/releases/tag/v0.15.2)。
- [README](https://github.com/poco-ai/Agentero/blob/1c6152d3020fff23e31f0e5580a3d519fb7731c2/README.md)、[当前主线版本](https://github.com/poco-ai/Agentero/blob/1c6152d3020fff23e31f0e5580a3d519fb7731c2/package.json)、[入门与 Catalog](https://github.com/poco-ai/Agentero/blob/1c6152d3020fff23e31f0e5580a3d519fb7731c2/docs/usage/getting-started.md)、[架构](https://github.com/poco-ai/Agentero/blob/1c6152d3020fff23e31f0e5580a3d519fb7731c2/docs/architecture.md)、[ACP / 权限](https://github.com/poco-ai/Agentero/blob/1c6152d3020fff23e31f0e5580a3d519fb7731c2/docs/usage/agents.md)。
- [内置 provider 及网关边界](https://github.com/poco-ai/Agentero/blob/1c6152d3020fff23e31f0e5580a3d519fb7731c2/docs/backend/builtin-provider.md)、[当前 settings 默认](https://github.com/poco-ai/Agentero/blob/1c6152d3020fff23e31f0e5580a3d519fb7731c2/src-tauri/src/features/system/settings/mod.rs)、[遥测说明](https://github.com/poco-ai/Agentero/blob/1c6152d3020fff23e31f0e5580a3d519fb7731c2/docs/backend/telemetry.md)、[遥测门控](https://github.com/poco-ai/Agentero/blob/1c6152d3020fff23e31f0e5580a3d519fb7731c2/src-tauri/src/core/telemetry/mod.rs)、[隐私 UI](https://github.com/poco-ai/Agentero/blob/1c6152d3020fff23e31f0e5580a3d519fb7731c2/src/components/settings/panes/general/privacy-settings-block.tsx)。
