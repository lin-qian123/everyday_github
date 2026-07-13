<!-- markdownlint-disable MD013 MD034 -->

# CowAgent

- GitHub: https://github.com/zhayujie/CowAgent
- 分类：Agent 框架与技能生态
- 主要语言：Python
- 抓取日期：2026-07-14

## 定位

`CowAgent` 是一个开源“超级 AI 助手”和 Agent Harness，实现任务规划、工具调用、技能系统、个人知识库、长期记忆、多模型接入和多渠道消息入口。GitHub API 样本显示该项目约 `46.0k stars`，topics 覆盖 `ai-agent`、`harness`、`mcp`、`skills`、`multi-agent`。

它延续了 `chatgpt-on-wechat` 一类多渠道助手路线，但把重点升级到 agent harness：不只是回复消息，而是计划任务、调用工具、安装/创建技能、沉淀记忆并在日常使用中自我演化。

## 用法

README 给出的快速路径包括：

```bash
bash <(curl -fsSL https://cdn.link-ai.tech/code/cow/run.sh)
```

也支持 Docker 部署、Web 控制台、在线体验和 Skill Hub。典型场景包括：

- 在 Web、微信、飞书、钉钉、企业微信、QQ、Telegram、Slack 等渠道接入同一个 agent。
- 配置 Claude、GPT、Gemini、DeepSeek、Qwen、GLM、Kimi、MiniMax、豆包等模型。
- 使用文件、终端、浏览器、计划任务、记忆检索、Web 搜索、MCP 等工具。
- 通过 Skill Hub 或 GitHub 安装技能，或让 agent 从自然语言中创建技能。

## 原理

CowAgent 把消息流拆成多层：

- Channels：接入不同 IM、Web 或平台消息。
- Agent Core：进行规划、推理、工具选择和执行循环。
- Memory：上下文、日常记忆、核心记忆分层，并结合关键词和向量检索。
- Knowledge：把长期知识整理为 Markdown wiki 和知识图谱。
- Skills / Tools：把可复用流程和具体能力暴露给 agent。
- Models：将不同 LLM provider 抽象为可切换后端。

## 价值

- 对中文用户：多渠道和中文文档降低了个人 agent 的部署门槛。
- 对工程实践：把 harness、memory、skills、MCP、channels 放进同一系统，适合观察“个人 AI 助手”会如何产品化。
- 对团队自动化：可以把消息入口、计划任务和工具执行结合起来，形成轻量运维/运营助手。

## 风险边界

- 多渠道接入会扩大隐私暴露面，尤其是 IM 历史、文件、联系人和组织消息。
- 一键安装脚本需要先审查来源与权限，避免在生产机器上直接执行未知脚本。
- 自演化记忆可能沉淀错误偏好或敏感信息，需要人工审查和清理机制。
- 接入 MCP、终端和浏览器后，必须限制工具权限与工作目录。

## 补充建议

- 初始部署只接入一个低风险渠道和一个测试模型。
- 先关闭高风险写操作，等工具调用日志稳定后再逐步开放。
- 把 Memory 和 Knowledge 的存储目录纳入备份、脱敏和删除策略。
- 与 `nanobot`、`openclaw`、`hermes-agent` 对照观察个人 agent kernel 的差异：渠道、记忆、技能和控制面各有侧重。

## 参考资料

- GitHub 仓库：https://github.com/zhayujie/CowAgent
- 官方站点：https://cowagent.ai/
- 文档：https://docs.cowagent.ai/
- Skill Hub：https://skills.cowagent.ai/
