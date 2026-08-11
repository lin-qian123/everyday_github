# agent-link

## 定位

`agent-link` 让跨机器 Codex、Claude Code 等 coding agents 通过共享私有 Git 仓库或可选 relay 交换任务和进度。它使用端到端加密 room、local daemon、MCP server 与通知 hook；不是陌生协作者的安全通信系统。

## 用法

```bash
pipx install git+https://github.com/Riccardo8888/agent-link.git
agent-link install
agent-link config --set git_remote="git@github.com:you/your-project.git"
agent-link doctor
```

一方以 `agent-link join --room auth-review` 创建 room，再分享 invite 或无 secret door code。应为 CI 配置 `branches-ignore: [claude-link]`，防止 heartbeat push 触发构建。

## 原理

agent 经 MCP stdio 调用 local daemon；daemon 处理同步、收件箱、日志与网络。私有 carrier 使用孤儿 `agent-link` 分支下的 `claude-link/`，不抓取项目代码历史。frame 采用 AES-256-GCM、发送设备签名，路由 header 被绑定到签名和 AEAD tag。

## 价值

将跨机 agent 的分工、回报和等待消息变为可控通道，同时将传输分支与代码分支分开。

## 风险边界

无 forward secrecy：长期 room key 可读过去和未来内容，移除成员不能回收已读消息。host/relay 虽不能读正文却可见元数据；`.conv/` transcript 在成员机明文保存，远端消息进入模型仍是不可信输入，不能发送凭据或客户数据。

## 补充建议

仅对互信人员、私有仓库和隔离项目试用；验证 branch filter、密钥轮换和 transcript 保护，并对接收消息实施 prompt-injection 处理与人工审核。

## 参考资料

- [GitHub 仓库](https://github.com/Riccardo8888/agent-link)
- [README：安装、传输与安全限制](https://github.com/Riccardo8888/agent-link/blob/main/README.md)
- [安全报告流程](https://github.com/Riccardo8888/agent-link/blob/main/SECURITY.md)
