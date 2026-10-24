<!-- markdownlint-disable MD013 -->

# cindy：统一多 Harness 的桌面与手机 Agent 客户端

- 主上游：[makecindy/cindy](https://github.com/makecindy/cindy)；repository ID `1309102418`。
- 采样日期：2026-10-25（Asia/Shanghai）；分类：Coding Agents 与终端助手。
- API 累计快照：4,059 stars / 583 forks / 1,887 open issues（含 PR 口径）；与榜单日增分开。
- 默认分支 `main`，本页静态依据固定在 `07fb9ba1e7639515f3c525416c68a8ff18bde306`。发行列表首项 `v0.1.115`，发布于 2026-10-23T02:46:16Z（正式）。
- 核验层级：直接读取上游文档、许可、元数据和下列部分实现；未安装运行、调用模型或复现性能。

## 定位

Cindy 将 Claude Code、Codex 等 Harness、模型、记忆、Skill、MCP 与自动化纳入同一客户端，面向本机文件与已登录应用工作。本仓库只开源 Electron 桌面端、Expo / React Native 手机端和共享 packages，服务端位于独立仓库；不能将客户端开放等同于完整云服务可自托管。README 标明插件市场等能力仍在打造。

## 用法

普通使用走官方发行渠道；开发需 Node 22.x、pnpm 10.x、Git LFS。上游源码入口为：

```bash
git clone https://github.com/makecindy/cindy.git
cd cindy
git lfs pull
pnpm install
pnpm restart:desktop:remote --region=cn
```

国际账号使用 `--region=global`。`pnpm install` 会按平台下载 Claude Code / Codex / ripgrep 等二进制，不是纯离线依赖解析。登录页可跳过 Cindy 登录，使用本机 agent 功能，但依赖服务端的能力不可用。以上是上游操作示例，本轮未安装或登录。

## 原理

客户端共享 packages 处理鉴权、device-link、Agent 编排与模型供应商；桌面端把不同 Harness 的任务现场、工具与记忆组织到统一界面，并可从 IM、定时任务派活。两份 endpoint 配置区分地区，Remote 开发默认使用官方云账号和服务。跨 Harness 的连续性是上游设计目标，本轮没有验证恢复、冲突与远程撤权。

## 价值

对已有 Claude Code / Codex 使用者，统一会话、文件与工具入口可减少切换成本；手机和自动化适合监督持续任务。是否能复用已有套餐、哪些能力收费，应以实际账户和服务规则为准，源码免费不代表模型调用免费。

## 风险边界

真实文件、浏览器及应用登录态意味着高权限操作能力，需用专用工作目录和可恢复样本验证。默认连接官方服务与 CDN，“本机运行”不能推出零外发。README 说明官方包含 TapDB 元数据统计；当前桌面实现进一步设置构建、隐私同意和使用统计开关三重条件，开发构建默认不初始化，不能仅凭 README 推断所有构建都立即上报。聊天和文件不采集是上游披露，本轮未抓包验证。Apache-2.0 主要覆盖本仓源码，外部模型、服务、商标与第三方组件另核。

## 补充建议

先跳过云登录，用可丢弃仓库测普通任务、切换 Harness 和重启恢复；随后逐项核地区端点、统计开关、云心跳、远程设备解绑与模型费用。把工具审批、IM 触发者权限和自动化执行身份分别记录；固定客户端与下载二进制版本，避免只记录源码 SHA。

## 参考资料

- [README.zh-CN.md](https://github.com/makecindy/cindy/blob/07fb9ba1e7639515f3c525416c68a8ff18bde306/README.zh-CN.md)。
- [SECURITY.md](https://github.com/makecindy/cindy/blob/07fb9ba1e7639515f3c525416c68a8ff18bde306/SECURITY.md)。
- [config/endpoint.json](https://github.com/makecindy/cindy/blob/07fb9ba1e7639515f3c525416c68a8ff18bde306/config/endpoint.json)。
- [config/endpoint.global.json](https://github.com/makecindy/cindy/blob/07fb9ba1e7639515f3c525416c68a8ff18bde306/config/endpoint.global.json)。
- [apps/desktop/src/renderer/analytics/tapdbClient.ts](https://github.com/makecindy/cindy/blob/07fb9ba1e7639515f3c525416c68a8ff18bde306/apps/desktop/src/renderer/analytics/tapdbClient.ts)。
- [package.json](https://github.com/makecindy/cindy/blob/07fb9ba1e7639515f3c525416c68a8ff18bde306/package.json)。
- [LICENSE](https://github.com/makecindy/cindy/blob/07fb9ba1e7639515f3c525416c68a8ff18bde306/LICENSE)。
- [仓库 API](https://api.github.com/repos/makecindy/cindy)、[发行 API](https://api.github.com/repos/makecindy/cindy/releases?per_page=3)；动态元数据只代表本轮采样。
- 事实来源为以上固定文件；价值、风险评估和验证建议为本库工程判断，未作为上游实测结果。
