<!-- markdownlint-disable MD013 -->

# OpenBitFun（GCWing/OpenBitFun）中文解读

> 上游仓库：<https://github.com/GCWing/OpenBitFun> · 归类：Coding Agents 与终端助手 · 证据快照：2026-10-18（Asia/Shanghai）。认证 API：2,828 stars / 267 forks / 115 open issues；Release / tag `v1.0.6`；核心代码 MIT，第三方依赖 / 资产保留各自条款。本页为上游材料及所列源码的静态整理，未安装运行、复测 benchmark 或完成全面安全审计。

## 定位

OpenBitFun 用 Rust Agent Runtime 与 Tauri 桌面壳组织编码及通用任务，支持多种 harness、Mini App、CLI 与远程工作空间。四种模式分别面向快速协作、分步任务、复杂多 Agent 和定制创作；模式更多是执行策略，不能直接代表质量等级。

## 用法

从官方入口按平台选包并参照下载验证文档，或按 README 用 Node.js 22.12+、pnpm 10.15.0 和 Rust 构建。先配测试模型和一次性 workspace，从 Minimal / Standard 单任务开始。**1.0 与旧 0.2.x 数据不兼容**，README 指定 Data Tools 迁移范围为稳定版 0.2.17–0.2.19；升级前核对旧版本与备份，不能覆盖后再尝试恢复。

## 原理

Runtime 管理 session、上下文、工具、压缩和中断恢复；桌面、CLI、手机等是交互入口，SSH / Docker 可把执行放到目标环境。Mini App 把专用界面与会话绑定，MCP / Skills / Hooks 扩展工具。当前 Relay 文档描述同一 GitHub 身份的设备发现与加密消息中转。

## 价值

把任务、文件和多个交互设备连起来，有助于长任务接续和把重复操作做成专用工具。DeepSWE v1.1 两组模型通过率与时延仅是 README 作者评测；应在自己的任务上记录固定模型、成本、最终验收和恢复一致性。

## 风险边界

- **远程连接文档存在漂移**：首页折叠段说用自部署 Relay；当前 Relay README 则说默认使用官方 endpoint，以 GitHub 身份配对。私有 Relay 需要修改并构建匹配客户端，不能按首页认定开箱即用自托管。
- 同网模式在桌面启动局域网 Relay，但两种模式都通过官方身份服务验证 GitHub 登录，仍需互联网。文档称 X25519 / HKDF / AES-GCM 加密、中转不持私钥；本轮没有密码学或运行时验证。
- 端侧解密后，模型、工具、MCP、shell、远端主机仍有各自数据与权限边界；加密中转不限制 Agent 的已授权操作。
- Mini App、市场插件、Hook 和自修改源码扩大供应链。最新版才单独接收安全修复；下载页可达不等于制品签名已经验证。

## 补充建议

用两个测试设备与无隐私内容验证配对、撤销、离线表现和中断恢复；单独验 SSH / Docker 的文件与凭证范围。迁移先保留旧安装和备份，在副本上核对 sessions / 文件数量；固定 harness 与模型完成同一任务，再比较复杂模式的收益。

## 参考资料

- 上游仓库：<https://github.com/GCWing/OpenBitFun>
- GitHub REST API：<https://api.github.com/repos/GCWing/OpenBitFun>
- README / 四模式 / 迁移：<https://github.com/GCWing/OpenBitFun/blob/main/README.md>
- 当前 Relay 架构与身份依赖：<https://github.com/GCWing/OpenBitFun/blob/main/src/apps/relay-server/README.md>
- 下载验证方法：<https://github.com/GCWing/OpenBitFun/blob/main/docs/verify-downloads.md>
- 安全策略：<https://github.com/GCWing/OpenBitFun/blob/main/SECURITY.md>
- 数据迁移工具：<https://github.com/GCWing/OpenBitFun/blob/main/src/apps/data-tools/README.md>
- Release：<https://github.com/GCWing/OpenBitFun/releases/tag/v1.0.6>
- 许可：<https://github.com/GCWing/OpenBitFun/blob/main/LICENSE>
