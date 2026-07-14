<!-- markdownlint-disable MD013 MD034 -->

# awesome-copilot

`github/awesome-copilot` 是 GitHub 官方组织下的 Copilot 自定义资源集合，覆盖 custom agents、instructions、skills、hooks、workflows、plugins、MCP tools 和 cookbook。它反映 Copilot 正从“补全工具”变成可配置 agent 平台。

- GitHub：https://github.com/github/awesome-copilot
- 网站：https://awesome-copilot.github.com
- llms.txt：https://awesome-copilot.github.com/llms.txt
- 分类：Agent 框架与技能生态
- 许可证：MIT

## 热度信号

- 2026-07-15 通过 GitHub API 抓取时约 `36.6k stars`、`4.6k forks`。
- 仓库在 2026-07-14 仍有 push，topics 包含 `agent-skills`、`custom-agents`、`github-copilot`。
- README 明确列出 Agents、Instructions、Skills、Plugins、Hooks、Agentic Workflows、Cookbook 等资源类型。

## 定位

Awesome Copilot 是 Copilot 生态的“配置和技能目录”。它不直接替代 Copilot CLI 或 IDE 插件，而是把社区和官方维护的 agent persona、项目规则、技能包、插件、hooks、workflow 和示例集中管理。

对团队的意义是：Copilot 的能力边界越来越多由 repo 内规则、marketplace 插件、skills 和 MCP servers 决定，而不是只由模型决定。

## 用法

README 提供插件安装入口：

```bash
copilot plugin install <plugin-name>@awesome-copilot
```

如果 marketplace 未注册，可以先执行：

```bash
copilot plugin marketplace add github/awesome-copilot
copilot plugin install <plugin-name>@awesome-copilot
```

网站提供全文搜索和过滤，`llms.txt` 则方便 agent 直接读取结构化目录。

## 原理

仓库把 Copilot 可定制能力拆成几类：

- agents：专用 Copilot agents，通常可结合 MCP servers。
- instructions：按文件模式自动应用的编码标准和项目规则。
- skills：带说明和资产的自包含能力目录。
- plugins：面向特定工作流的 agents / skills bundle。
- hooks：Copilot agent session 中触发的自动动作。
- workflows：用 Markdown 描述的 GitHub Actions agentic automation。
- cookbook：API 与实践配方。

## 价值

- 对 Copilot 用户，提供可发现、可复用的配置入口。
- 对团队治理，instructions 和 plugins 可以沉淀约定而不是口头传递。
- 对 agent 生态，说明 skills / MCP / hooks 正成为主流平台能力。
- 对研究者，可观察 Copilot 与 Claude Code、Codex、Cursor 的技能生态差异。

## 风险边界

- README 明确提示第三方 customizations 需要安装前审查。
- skills、hooks 和 plugins 可能引入外部命令、数据读取或写操作。
- 目录热度不代表每个资源都适合生产环境。
- Copilot CLI / VS Code / GitHub Web 的能力支持可能存在版本差异。

## 补充建议

- 企业内部应建立 allowlist，不要让所有开发者随意安装第三方 agent/plugin。
- 对 instructions 与 hooks 做代码审查，尤其关注凭据、网络请求和写文件动作。
- 用 `llms.txt` 做机器读取目录时，也要保留人工确认环节。
- 与 `awesome-claude-code`、`agents`、`nvidia-skills` 对比，观察跨 harness skills 是否会统一。

## 参考资料

- GitHub 仓库：https://github.com/github/awesome-copilot
- 网站：https://awesome-copilot.github.com
- Agents：https://awesome-copilot.github.com/agents
- Skills：https://awesome-copilot.github.com/skills
- Tools：https://awesome-copilot.github.com/tools
