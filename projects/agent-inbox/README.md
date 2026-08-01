# agent-inbox

## 定位

`agent-inbox` 是一个个人链接收集队列：从手机、浏览器或脚本把 URL/选中文本投递到 REST API，再由 Claude、ChatGPT、MCP client 或 shell 脚本按队列读取并给出意见和下一步。截至 2026-08-02 的 GitHub API 快照：项目创建于 2026-08-01，约 4 stars、0 forks，MIT。

## 用法

可通过 Cloudflare Workers 部署按钮，或克隆后 `npm install`、`npx wrangler deploy`。首次打开部署地址要立即创建 inbox 并安全保存 passcode/secret；也可通过 userscript、浏览器扩展、iOS Shortcut 或网页粘贴投递。将 API 接给 agent 前，应先只允许已知域名和测试队列。

## 原理

服务运行在 Cloudflare Workers + D1，队列通过普通 REST API 暴露，因此不同 agent 或客户端都能消费。它解决的是“捕获与排队”，不验证链接内容，也不保证 agent 对链接的总结、观点或行动建议正确。

## 价值

- 把碎片化阅读入口与后续 agent 处理解耦，适合个人研究与待办收集。
- API 与客户端无关，可用既有 MCP/脚本接入，而不锁定单一模型供应商。

## 风险边界

- 链接、选中文本和 agent 处理结果都可能含个人信息、访问令牌或未公开内容。
- README 提醒未完成初始化前，知道部署地址的他人可能抢先认领 inbox；密钥和访问控制必须优先处理。
- 不可信网页会带来提示注入、恶意下载和错误结论风险，不能让 agent 自动执行页面建议。

## 补充建议

使用随机长 token、最小权限和短日志保留期；入队时保存来源与时间，消费端实行域名 allowlist、纯文本提取、人工批准和密钥脱敏。

## 参考资料

- GitHub：<https://github.com/OGZamasu/agent-inbox>
- 部署说明：<https://github.com/OGZamasu/agent-inbox/blob/main/SETUP.md>
- GitHub API 快照：<https://api.github.com/repos/OGZamasu/agent-inbox>
