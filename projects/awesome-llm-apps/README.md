<!-- markdownlint-disable MD013 MD034 -->

# awesome-llm-apps

`Shubhamsaboo/awesome-llm-apps` 是一个可运行 AI agent、agent skills 与 RAG 应用模板集合。它的卖点是“clone、customize、ship”：不是只列链接，而是提供一批可以直接运行或交给 coding agent 使用的样例。

- GitHub：https://github.com/Shubhamsaboo/awesome-llm-apps
- 关联站点：https://www.theunwindai.com
- 分类：Agent 框架与技能生态
- 许可证：Apache-2.0

## 热度信号

- 2026-07-15 通过 GitHub API 抓取时约 `120.7k stars`、`17.9k forks`。
- 仓库在 2026-07-14 仍有 push，topics 包含 `agents`、`llms`、`rag`。
- README 标注覆盖 `100+` open-source AI agents、agent skills 和 RAG apps，并提供 Trendshift 日榜徽章。

## 定位

这个项目更像“可运行 agent 应用样例库”，而不是底层框架。它把多种场景拆成模板：

- starter AI agents
- advanced AI agents
- multi-agent apps
- voice AI agents
- RAG 应用
- coding agent 可安装 skills

对想快速学习“agent 应用到底怎么落到代码里”的用户，它比抽象框架文档更直接。

## 用法

README 提供两种典型入口。

安装单个 skill：

```bash
npx skills add https://github.com/Shubhamsaboo/awesome-llm-apps/tree/main/agent_skills/project-graveyard
```

克隆并运行某个示例应用：

```bash
git clone https://github.com/Shubhamsaboo/awesome-llm-apps.git
cd awesome-llm-apps/starter_ai_agents/ai_travel_agent
pip install -r requirements.txt
streamlit run travel_agent.py
```

## 原理

项目本身不是一个 runtime，而是通过目录组织沉淀模式：

- 每个 app / skill 单独成目录，包含依赖、示例代码和使用说明。
- 用常见 Python / Streamlit / agent SDK 组合降低上手门槛。
- 一部分 skill 直接面向 Claude Code、Codex、Cursor 等 coding agent。
- 模板覆盖“从输入、检索、工具调用到 UI”的完整最小链路。

## 价值

- 适合快速找样例：比从零搭 agent 更快。
- 适合教学：可以按场景拆解 RAG、工具调用、多 agent、语音 agent。
- 适合产品原型：很多模板可直接改成内部 demo。
- 适合观察 agent 应用热点：新增模板反映社区正在关注的使用场景。

## 风险边界

- awesome 仓库的 stars 不等于每个模板都生产可用。
- 示例模板可能依赖外部 API key、第三方服务或旧版本 SDK。
- 复制模板到生产前，需要补测试、鉴权、异常处理和隐私审查。
- “agent skills” 需要像代码依赖一样审查，不能盲目安装。

## 补充建议

- 使用前先选一个具体子目录，不要把整个仓库当框架。
- 对每个模板记录模型、API key、外部数据源和可复现步骤。
- 企业内复用时，建议建立允许安装的 skill 白名单。
- 可与 `awesome-copilot`、`agents`、`awesome-claude-code` 一起看，判断 skills 生态是否正在分化。

## 参考资料

- GitHub 仓库：https://github.com/Shubhamsaboo/awesome-llm-apps
- Unwind AI：https://www.theunwindai.com
- Agent skills 目录：https://github.com/Shubhamsaboo/awesome-llm-apps/tree/main/agent_skills
