<!-- markdownlint-disable MD013 -->

# FreeLLMAPI

> 上游仓库：[tashfeenahmed/freellmapi](https://github.com/tashfeenahmed/freellmapi) · 归类：模型、训练与推理基础设施 · 本页基于 2026-08-31 的 GitHub Trending、REST API 与上游 README/architecture 文档快照整理。

## 定位

FreeLLMAPI 是本地优先、单用户的免费 LLM 统一路由器：把多个 provider 的模型和兼容协议收敛到一个本地 `/v1` 端点，并提供自动回退、限额跟踪、模型目录、桌面应用、MCP 和多种 coding-agent 配置生成器。官方 Trending 抓取时显示约 +505 当日 stars；REST API 快照为 22,738 stars、3,148 forks、85 个开放 issue，最近推送于 2026-08-30，API 与 README 均标示 MIT。上游明确将其定位为个人实验，不是生产 inference SLA。

## 用法

Docker 快速路径由上游提供，使用前应先阅读脚本和 [安装文档](https://github.com/tashfeenahmed/freellmapi/blob/main/docs/install.md)：

```sh
curl -fsSL https://freellmapi.co/install.sh | bash
```

也可以从源码运行 `npm install && npm run dev`，打开本地 dashboard，添加自己拥有的 provider keys，选择 fallback chain，再将 `http://localhost:3001/v1` 配置给 OpenAI SDK、Aider、Claude Code、Codex CLI 或其他兼容客户端。首次验证应使用低额度测试 key、`--dry-run` 配置生成器和非敏感 prompt；不要把本地端口直接暴露到公网。

## 原理

- 客户端请求先到 Express proxy；router 根据优先级、健康状态、模型能力、速率余量和实时测量选择 provider/model。
- key 保存在 SQLite，并以 AES-256-GCM 加密；调用前在内存解密。发生 429、5xx 或超时后，失败 key 进入 cooldown，路由器沿 fallback chain 重试。
- rate-limit ledger 维护 RPM/RPD/TPM/TPD，health service 定期探测 key；sticky session 和 compact handoff note 用于减少多轮对话切换造成的上下文漂移。
- provider adapters 统一 OpenAI、Anthropic、Gemini/Ollama 等协议表面；dashboard 负责 key、profile、日志、分析和路由策略，MCP 端点允许 agent 查询可用模型与健康状态。

## 价值

- 用一个本地端点连接多个免费或自有 provider，便于原型阶段比较延迟、能力、限额和失败回退。
- 统一 OpenAI/Anthropic/Gemini/Ollama 表面，减少为不同 coding agent 手工维护配置的成本。
- 健康检查、per-key 限额、attempt trail、p50/p95/TTFT 和 provider breakdown 为容量与故障排查提供可观察入口。
- 桌面 app、Docker、ARM SBC 和源码路径覆盖个人电脑、homelab 和小型实验环境，但不改变免费 provider 的服务条款与容量上限。

## 风险边界

- 免费额度、排队、模型可用性、延迟和 provider 条款会变化；路由成功不等于模型能力稳定，也不等于有 SLA。
- 代理会让 prompt、工具调用、附件、日志和统计同时经过本机与上游 provider；加密 key 不会让内容自动获得端到端隐私。
- 上游明确禁止把项目当生产后端；默认的单用户模型不是多租户隔离。不要共享 unified bearer token、暴露 dashboard 或将 provider key 导出给 agent。
- “smart routing”依据有限观测和历史错误，可能把任务送到更快但更弱/更不适合的模型；工具调用、structured output 和 fallback 仍需按目标 provider 回归。
- 一键安装脚本、自动更新目录、桌面权限、加密备份和 MCP 会扩大供应链、网络和本地文件风险；安装前应锁定版本并阅读脚本。

## 补充建议

1. 在隔离环境中固定 provider、模型 revision、路由策略、并发、提示集和额度，记录成功率、TTFT、总延迟、token、质量和失败链路。
2. 先只接入个人测试 key 与公开数据，关闭远程访问、自动目录更新和不需要的协议表面，再逐项审查 provider ToS。
3. 将 fallback 当作可观测的降级策略，而不是质量保证；对 coding、视觉、工具调用和 JSON schema 分开建立基线。
4. 生产或含敏感数据的工作负载使用有合同/SLA 的 provider 或自托管模型，并保留密钥轮换、日志删除、备份恢复和回滚方案。

## 参考资料

- [上游 README、Features 与限制](https://github.com/tashfeenahmed/freellmapi)
- [架构与路由细节](https://github.com/tashfeenahmed/freellmapi/blob/main/docs/architecture.md)
- [客户端与 coding-agent 配置](https://github.com/tashfeenahmed/freellmapi/blob/main/docs/clients.md)
- [安装与部署](https://github.com/tashfeenahmed/freellmapi/blob/main/docs/install.md)
- [REST API 元数据](https://api.github.com/repos/tashfeenahmed/freellmapi)
- [GitHub Trending](https://github.com/trending)
