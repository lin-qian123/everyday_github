# agents（wshobson/agents）

- GitHub: https://github.com/wshobson/agents
- 主页: https://sethhobson.com
- 记录日期: 2026-06-25 (Asia/Shanghai)

## 定位

`agents` 是一个跨多种 AI 编码工具的 agentic plugin marketplace。它试图用同一份 Markdown 源内容，同时为 Claude Code、Codex CLI、Cursor、OpenCode、Gemini CLI 和 GitHub Copilot 生成各自可消费的插件、技能、命令和 agent 资产。

## 用法

### 1) 作为 Claude Code 插件市场使用

官方 README 给出的最短路径是：

```bash
/plugin marketplace add wshobson/agents
/plugin install python-development
```

### 2) 作为 Codex / Cursor / OpenCode / Gemini 的分发源

README 明确给出多工具接入方式，例如：

```bash
npx codex-marketplace add wshobson/agents
```

如果是 Gemini 或 OpenCode，则走 clone + generate 路线，把源内容转换成对应 harness 可识别的目录结构。

### 3) 先看 catalog 再按需装

官方 README 里已经列出插件、agent、skills、commands 的数量，适合先按场景筛选，再决定是否安装。

## 原理

1. 仓库把 `plugins/` 目录当作单一事实源，随后通过 adapter 为不同 harness 生成各自原生格式，而不是只做最低公分母兼容。
2. `docs/harnesses.md` 直接给出 capability matrix，明确说明不同 agent 工具在 skills、subagents、commands、MCP、context file 等方面的差异。
3. 它本质上是在做“agent 生态分发层”：把可安装能力、格式转换、兼容策略和目录治理统一起来。

## 价值

- 对同时使用多种 agent 工具的团队来说，它比维护多套分散规则更省事。
- 它让“插件 / 技能 / 命令 / 子代理”从零散素材，变成可版本化、可安装、可适配的正式资产。
- 这类项目说明 agent 生态正在进入“供应链管理”阶段，而不是只比谁能多写几段 prompt。

## 风险边界

- 跨 harness 兼容并不等于跨 harness 等价；同一能力在不同代理中的落地效果仍可能明显不同。
- 仓库内容规模很大，插件数、agent 数、skills 数都很高，团队如果缺少白名单和治理规则，容易出现上下文噪声与行为漂移。
- 当上游 agent 工具更新上下文格式或插件协议时，这类仓库需要持续跟进适配。

## 补充建议

1. 优先从一个垂直插件开始试，例如 Python、前端或基础设施，不要一口气装一整套市场。
2. 真正有价值的验证点不只是“能不能装上”，而是同一插件在 Codex、Claude Code、Cursor 上是否还能保持预期工作流。
3. 如果团队内部也维护自定义技能包，可以把它视为分发和适配范式，而不一定要直接照搬全部内容。

## 参考资料

- https://github.com/wshobson/agents
- https://github.com/wshobson/agents/blob/main/docs/harnesses.md
- https://github.com/trending/python
