<!-- markdownlint-disable MD013 -->

# OpenMausBot

## 定位

OpenMausBot 把 Claude、Codex、Grok 等本地 CLI 接成一个可管理的机器人团队，并提供聊天、任务、审批、电脑操作、外部应用和语音入口。它是独立项目，与 xAI 没有隶属或背书关系。

电脑能力有不同边界：可用自己的主机、Local VM 或 Boat 云电脑；不能把所有机器人都理解为运行在独立虚拟机内。

2026-10-30 快照：综合 / TypeScript daily +1,190 stars；API 累计 7,423 stars / 1,108 forks / 550 open issues（含 PR）。核读 main `dd7045000c0f`；发行 API 首项 [v0.1.133](https://github.com/milind-soni/OpenMausBot/releases/tag/v0.1.133)，2026-10-29 UTC。以下为文档与有限源码核读，未安装运行。

## 用法

先选择固定发行包，或审阅源码后在专用环境启动。主线要求 Node 24+、pnpm，并至少安装登录一种 Agent CLI；下面是上游源码流程，本轮未执行：

```bash
git clone https://github.com/milind-soni/OpenMausBot
cd OpenMausBot
pnpm install
pnpm dev:server
# 另一终端启动前端
pnpm dev
```

默认 harness 为 127.0.0.1:8799，前端为 127.0.0.1:5199。Composio、Boat、托管语音是分别配置的可选服务；先用无外部连接的合成任务验收。也有 npm CLI、桌面包和 stdio MCP，按实际部署路径选一种。

## 原理

React 前端通过 HTTP 发命令，并归并一条 SSE 事件流；服务端持有 provider driver、Agent 进程、permission broker 和逐会话 NDJSON。MCP 暴露任务 / 团队控制、有限转录检索和等待操作；文档明确不暴露审批授予、凭据和电脑生命周期。等待接口还区分会话 settled 与 job completed / failed / needs-input。

## 价值

适合把多 provider 的开发与资料整理任务放在一个可观察工作台中。紧凑转录和 job 状态有助于脚本接续，但“有机器人回复”仍需与交付文件和任务验收分开。

## 风险边界

- 核心 Apache-2.0，enterprise/ 使用单独的 source-available 条款，生产启用、再分发和第三方托管有额外限制；依赖组件还保留原许可。
- CLI onboarding 文档明确 API key 保存在私有 config.json 中，为明文；Unix 的 0600 权限不等于加密。
- 主机控制、应用连接、邮件 / 社媒动作和云电脑各有真实权限、数据出口与费用。MCP 的有限工具集不自动缩减被驱动 Agent 本身的权限。
- Ubuntu 仍为 beta；Wayland 的本机机器人控制被禁用，Xorg 需要明确启用；桌面能力不能跨平台一概而论。
- analytics 文档细于 README 的“匿名”摘要：特定已登录 Cloud Pro 弹窗点击可把本机事件关联到 Cloud 邮箱。可在 Settings → General → Usage analytics 关闭；不同服务页面的设置范围需逐一核对。
- 触发器工具可创建日程和 webhook；停掉聊天窗口不一定等于清理已配置自动任务。

## 补充建议

固定发行和 provider 版本，用可丢弃仓库验证失败任务、转交任务、审批等待、中断与重启恢复。先用 mock connector 和最低权限主机，再分别检查云电脑销毁、费用、日志留存、key 文件和每个页面的 analytics 设置。

## 参考资料

- [上游仓库](https://github.com/milind-soni/OpenMausBot)、[仓库 API](https://api.github.com/repos/milind-soni/OpenMausBot)。
- [README.md](https://github.com/milind-soni/OpenMausBot/blob/dd7045000c0fd4d408c627962ff1ced964f29be4/README.md)。
- [docs/analytics.md](https://github.com/milind-soni/OpenMausBot/blob/dd7045000c0fd4d408c627962ff1ced964f29be4/docs/analytics.md)。
- [docs/mcp-server.md](https://github.com/milind-soni/OpenMausBot/blob/dd7045000c0fd4d408c627962ff1ced964f29be4/docs/mcp-server.md)。
- [LICENSING.md](https://github.com/milind-soni/OpenMausBot/blob/dd7045000c0fd4d408c627962ff1ced964f29be4/LICENSING.md)。
- [enterprise/LICENSE](https://github.com/milind-soni/OpenMausBot/blob/dd7045000c0fd4d408c627962ff1ced964f29be4/enterprise/LICENSE)。
- [LICENSE](https://github.com/milind-soni/OpenMausBot/blob/dd7045000c0fd4d408c627962ff1ced964f29be4/LICENSE)。
