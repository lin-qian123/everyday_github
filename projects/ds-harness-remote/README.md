<!-- markdownlint-disable MD013 -->

# ds-harness-remote

- 主上游：[liguobao/ds-harness-remote](https://github.com/liguobao/ds-harness-remote)
- 分类：记忆层与个人 AI 基础设施。
- 核验日期：2026-10-24（Asia/Shanghai）；默认分支 `main` 快照 `4d888ad3e359`。
- [API](https://api.github.com/repos/liguobao/ds-harness-remote) 快照：798 stars / 73 forks / 14 open issues；发行列表首项 [v0.5.18](https://github.com/liguobao/ds-harness-remote/releases/tag/v0.5.18)（UTC 2026-10-23，正式）。累计量不是今日增长，主线也不等于发行版。

## 定位

DS Harness Remote 是独立社区远程访问项目，让手机、浏览器或另一台电脑继续操作原 Host 上的 DeepSeek Harness 会话，并提供可选 Codex / ACP 工作区支持。它延伸现有开发环境的控制面，不是另起一套云开发环境；非 DeepSeek 官方产品。 [README.md](https://github.com/liguobao/ds-harness-remote/blob/4d888ad3e359416836072796d06348eba37eccc6/README.md)

## 用法

在 DeepSeek Harness Desktop 的插件管理中安装 `ds-harness-remote@0.5.18` 并重启；已有官方 launcher 也可使用：

```sh
dsh plugin --profile desktop add -w ds-harness-remote@0.5.18
```

从 Remote 侧栏登录，在另一设备以同账号选择 Host 和工作区。默认连接项目托管 Server；可按自托管文档部署最小 Server。Android 有发行包，iOS 为 TestFlight beta；VS Code 扩展仍为实验状态，README 明示跨机器端到端验证尚未完成。 [README.md](https://github.com/liguobao/ds-harness-remote/blob/4d888ad3e359416836072796d06348eba37eccc6/README.md)、[apps/server/README.md](https://github.com/liguobao/ds-harness-remote/blob/4d888ad3e359416836072796d06348eba37eccc6/apps/server/README.md)

## 原理

Host 主动向外建连，传输按 LAN → P2P → TURN → Relay 协商回退；业务流使用固定 Noise 套件加密，并结合账号 membership 与本地固定的设备公钥授权。中继仍能观察连接元数据。以上为上游协议 / 实现设计描述，本轮未复验密码学或真实跨网连接。 [docs/end-to-end-encryption.md](https://github.com/liguobao/ds-harness-remote/blob/4d888ad3e359416836072796d06348eba37eccc6/docs/end-to-end-encryption.md)、[docs/network.md](https://github.com/liguobao/ds-harness-remote/blob/4d888ad3e359416836072796d06348eba37eccc6/docs/network.md)

## 价值

适合在多设备间延续长时间编码任务，保留原有仓库、会话和工具状态。工程价值取决于网络回退、设备撤销和 Host 权限是否可控，而非是否采用 P2P 标签。

## 风险边界

- README 当前默认开启“允许控制此设备”和远程终端；终端以 Host 用户身份运行，独立于 Agent 审批。Linux 安装器还会以 root 启动服务，macOS 安装路径则为普通用户。关闭终端也不等于关闭所有可写操作，例如创建工作区仍可能创建目录。 [README.md](https://github.com/liguobao/ds-harness-remote/blob/4d888ad3e359416836072796d06348eba37eccc6/README.md)
- 同一 commit 的 E2EE 文档末段仍称不额外开放 Shell / PTY，与 README 的终端功能有范围差异；`terminal-policy.ts` 实际列出 create / write / follow 等接口并检查 Host 开关和设备归属。应以当前功能边界配置，不把旧描述当成无 shell 保证。 [docs/end-to-end-encryption.md](https://github.com/liguobao/ds-harness-remote/blob/4d888ad3e359416836072796d06348eba37eccc6/docs/end-to-end-encryption.md)、[packages/plugin/src/terminal-policy.ts](https://github.com/liguobao/ds-harness-remote/blob/4d888ad3e359416836072796d06348eba37eccc6/packages/plugin/src/terminal-policy.ts)
- E2EE 不解决已授权恶意客户端、终端系统被入侵或网络元数据暴露；长期连接 rekey 与独立密码安全审查仍在文档路线图中。 [docs/end-to-end-encryption.md](https://github.com/liguobao/ds-harness-remote/blob/4d888ad3e359416836072796d06348eba37eccc6/docs/end-to-end-encryption.md)
- 仓库 API 没识别到根许可证，但插件目录实际含 MIT；本轮只确认该文件，不能据此自动覆盖所有客户端、第三方素材或整个 monorepo。 [packages/plugin/LICENSE](https://github.com/liguobao/ds-harness-remote/blob/4d888ad3e359416836072796d06348eba37eccc6/packages/plugin/LICENSE)

## 补充建议

先在低权限测试 Host 连接两个自有设备，验证错误设备公钥、撤销后断连、终端关闭、重连附件归属、Relay 回退与文件预览边界。记录插件 / Server / 客户端各自版本。本轮未安装插件、登录托管服务、开放端口或运行远程终端。

## 参考资料

- [README.md](https://github.com/liguobao/ds-harness-remote/blob/4d888ad3e359416836072796d06348eba37eccc6/README.md)（固定 commit）。
- [docs/end-to-end-encryption.md](https://github.com/liguobao/ds-harness-remote/blob/4d888ad3e359416836072796d06348eba37eccc6/docs/end-to-end-encryption.md)（固定 commit）。
- [docs/network.md](https://github.com/liguobao/ds-harness-remote/blob/4d888ad3e359416836072796d06348eba37eccc6/docs/network.md)（固定 commit）。
- [packages/plugin/src/terminal-policy.ts](https://github.com/liguobao/ds-harness-remote/blob/4d888ad3e359416836072796d06348eba37eccc6/packages/plugin/src/terminal-policy.ts)（固定 commit）。
- [apps/server/README.md](https://github.com/liguobao/ds-harness-remote/blob/4d888ad3e359416836072796d06348eba37eccc6/apps/server/README.md)（固定 commit）。
- [packages/plugin/LICENSE](https://github.com/liguobao/ds-harness-remote/blob/4d888ad3e359416836072796d06348eba37eccc6/packages/plugin/LICENSE)（固定 commit）。
- [发行列表](https://github.com/liguobao/ds-harness-remote/releases)、[仓库 API](https://api.github.com/repos/liguobao/ds-harness-remote)（动态状态）。
