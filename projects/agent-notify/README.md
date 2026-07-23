# agent-notify

## 定位

`agent-notify` 是 macOS 上面向并行 Claude Code、Codex 等终端 agent 会话的通知队列守护进程。它用一条通知对应一个待处理会话，让通知栈本身成为“哪些 agent 正在等我”的状态板。截至 2026-07-24，仓库创建于 2026-07-23，约 9 stars。

## 用法

按项目 `install.md` 构建 Swift 二进制并配置 LaunchAgent，或手动运行 `agent-notify <bundle-id> <socket>`。现成 Claude Code hook 会在停止、等待输入和用户跟进时更新通知；其他 agent 可通过 Unix socket 的 `post`、`remove`、`list` JSON 协议接入。

## 原理

单一常驻守护进程独占通知连接，并以稳定会话标识替换同一会话的旧 banner。这样避免多个临时 notifier 冒用同一终端 bundle identity 时互相清理通知的竞态。

## 价值

- 为多 agent 并行工作提供低摩擦的人工注意力路由。
- 状态与工作树、仓库关联，减少“响了但不知道是谁”的上下文切换。
- 协议简单，可接入不同终端 agent。

## 风险边界

- 仅适用于 macOS，并依赖已废弃但仍可用的 `NSUserNotification`；未来系统兼容性不确定。
- hook 会读取本地会话元数据，通知正文不应包含敏感 prompt 或日志。
- 冒用终端应用身份依赖该应用已有通知权限，需明确授权与卸载路径。

## 补充建议

先在单个低敏感会话验证通知内容和点击跳转；再启用多会话。将通知分组关闭可提高可见性，但也会增加桌面噪声。

## 参考资料

- GitHub：<https://github.com/yauyauyauhen/agent-notify>
