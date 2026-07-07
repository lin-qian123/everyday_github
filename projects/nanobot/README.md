<!-- markdownlint-disable MD013 -->

# nanobot

## 定位

`nanobot` 是 HKUDS 开源的轻量个人 AI agent，目标是在保持核心小而可读的同时，提供 WebUI、聊天渠道、工具、记忆、MCP、模型路由、自动化和部署能力。

它更像一个“可拥有的个人 agent kernel / workbench”，不是只服务单一 IDE 的 coding agent。

## 用法

项目以 Python 包 `nanobot-ai` 为主要入口，支持命令行快速安装、浏览器 WebUI、Telegram、Discord、WeChat、Slack、Email、Mattermost 等聊天渠道，以及 provider、fallback model、Langfuse、MCP、web tools 和安全配置。

README 提供面向非技术用户的启动路径，也提供面向开发者的配置、架构和扩展文档。近期 release 重点包括 WebUI transcript、Python SDK runtime controls、automation management、搜索 / STT provider、gateway/session/provider 稳定性等。

## 原理

`nanobot` 把个人 agent 拆成多个可组合层：

- agent loop 与 session 管理。
- WebUI 和多聊天渠道适配。
- 模型 provider 与 fallback routing。
- 工具、MCP、CLI apps 和技能扩展。
- 记忆、自动压缩、自动化任务和长期目标。
- observability、权限和部署配置。

它的工程取向是让用户能在本地或自托管环境中拥有自己的 agent，而不是把所有上下文交给单个云端聊天产品。

## 价值

- **个人 AI 基础设施**：适合把日常聊天、工具调用、自动化和本地知识工作统一到一个 agent。
- **多渠道入口**：同一个 agent 可以连接 WebUI、IM、邮件和命令行。
- **可扩展工具层**：支持 MCP、web tools、CLI apps 和 provider 路由。
- **持续维护信号强**：README release notes 显示 2026 年以来高频更新，覆盖稳定性、渠道、记忆和自动化。

## 风险边界

- 多渠道 agent 会处理大量个人数据，需要认真配置访问控制、日志、密钥和存储周期。
- MCP、shell、邮件、IM 和 web tools 混在一起时，prompt injection 与越权操作风险会显著升高。
- 自托管并不自动等于安全；还需要网络暴露面、权限、备份和更新策略。
- 项目功能广，初次部署可能比单一聊天前端或单一 coding agent 更复杂。

## 补充建议

- 先从本地 WebUI 和单一 provider 试用，再逐步开启聊天渠道、MCP 和自动化。
- 对敏感账号和工作区启用最小权限，避免让 agent 同时拥有邮件、shell、浏览器和仓库写权限。
- 与 `open-knowledge`、`claude-mem`、`Personal_AI_Infrastructure` 对照，观察个人 AI 基础设施会更多走向“agent kernel”还是“知识库/记忆层”。

## 参考资料

- GitHub 仓库：<https://github.com/HKUDS/nanobot>
- 官方文档：<https://nanobot.wiki/docs/latest/getting-started/nanobot-overview>
- PyPI：<https://pypi.org/project/nanobot-ai/>
