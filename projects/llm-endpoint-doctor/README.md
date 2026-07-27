# llm-endpoint-doctor

## 定位

`llm-endpoint-doctor` 是面向 OpenAI-compatible、OpenAI Responses 与 Anthropic Messages 端点的诊断 CLI：它发现 base URL/模型，并探测 SSE、工具调用循环和基础 agent 兼容性，生成可复用报告与本地配置。

截至 2026-07-28，GitHub API 显示其创建于 2026-07-27，约 6 stars；属于早期开发者信号。

## 用法

使用 Node.js 20+ 安装或通过 `npx` 执行。先在无敏感数据的测试端点用 `--quick` 做发现；完整探测可能调用模型并产生费用，应把 key 放在环境变量或未提交的本地配置中。

```bash
npx llm-endpoint-doctor probe https://api.example.com --key-env API_KEY --quick
```

## 原理

CLI 尝试常见 URL 形态和协议端点，读取模型目录，并以小型请求验证流式事件及函数/工具返回后的续接行为。它据此写出能力报告，而不是从供应商宣传直接推断兼容性。

## 价值

- 在接入 coding agent 前暴露“普通聊天能通、工具循环却失败”的常见中继问题。
- 将端点检查结果固化为 JSON，可纳入部署验收或 provider 切换回归。

## 风险边界

- 成功的函数循环不代表支持托管 MCP、web/file search、computer use、长期 JSON Schema 稳定性或所有 agent。
- 探测请求会把测试提示发给目标端点，可能计费；不要将生产密钥写进报告、聊天或版本库。
- 早期 CLI 的兼容结论应以目标客户端实际集成为准。

## 补充建议

为每个 provider 设独立低额度测试 key；把 `--require` 的能力断言接入 CI，并在升级代理、模型或协议后重新执行最小回归。

## 参考资料

- GitHub：<https://github.com/xinlizhu/llm-endpoint-doctor>
- GitHub API 快照：<https://api.github.com/repos/xinlizhu/llm-endpoint-doctor>
