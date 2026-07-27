# cursor-bridge

## 定位

`cursor-bridge` 是单 Rust 二进制工具，声称让 Claude Code 使用 Cursor 订阅能力并尽量做到零配置。

截至 2026-07-27，GitHub API 显示其创建于 2026-07-26，约 22 stars；属早期开发者信号。

## 用法

按项目说明安装二进制并连接本地 Cursor/Claude Code 配置；在非敏感工作区先验证行为。

## 原理

它在 coding agent CLI 与订阅型 IDE 服务之间充当桥接层，复用现有会话或认证路径。

## 价值

- 反映开发者希望把不同 agent UI、订阅和 CLI 工作流组合使用。
- 单二进制发布降低试用门槛。

## 风险边界

- 应审查认证令牌、会话转发、服务条款与本地配置写入。
- 桥接层可能随上游客户端更新失效。

## 补充建议

先在临时账号和受控项目验证日志、网络目标和卸载/回滚路径。

## 参考资料

- GitHub：<https://github.com/hkc5/cursor-bridge>
