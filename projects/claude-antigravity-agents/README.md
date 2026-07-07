<!-- markdownlint-disable MD013 -->

# claude-antigravity-agents

## 定位

`claude-antigravity-agents` 是一个 Claude Code skill，用来把 Claude Code 变成主协调者，并把大型审查、研究、重构或第二意见任务委派给 Google Antigravity CLI 的后台子 agent。

它代表的是“跨模型、跨 agent 委派”路线：Claude Code 不再独自承担所有上下文和 token 消耗，而是生成自包含任务 brief，启动 `agy` 子任务，再回收结果并做验证。

## 用法

基本使用方式是先安装 Google Antigravity CLI，并完成一次 Google 登录，然后把仓库中的 `antigravity-agents` skill 目录复制到 Claude Code 的 skills 目录。

之后用户可以在 Claude Code 中提出类似“让 Antigravity 审查当前 diff”“让 Gemini 给这个缓存设计第二意见”“后台扫一遍依赖风险”的请求。skill 会指导 Claude Code 判断任务类型、生成 brief、启动 `agy -p "<task>"`，并在结果返回后做 diff、typecheck、build 等验证。

## 原理

项目本体很轻，核心是一份 `SKILL.md` 操作规程。它把任务分成两类：

- 只读任务：代码审查、架构分析、安全审计、研究 sweep 等，放在只读 sandbox 中并行执行。
- 写入任务：大型重构或独立编码任务，要求放进隔离 worktree 或单独仓库，避免与 Claude Code 当前编辑的文件冲突。

关键约束是“不让 Antigravity job 写入 Claude Code 正在编辑的同一批文件”，并要求 Claude 在采纳任何输出前读取结果、检查 diff、运行项目验证命令。

## 价值

- **节省上下文与 token**：把长审查、全仓扫描和研究任务从 Claude 主会话拆出去。
- **引入第二模型视角**：让 Gemini / Antigravity 对设计或实现给出独立判断。
- **并行吞吐**：主 agent 可以继续写代码，子 agent 在后台做可分离工作。
- **强化验证纪律**：项目明确要求返回结果必须经过 diff、typecheck、build，而不是直接信任子 agent。

## 风险边界

- 该项目依赖 Google Antigravity CLI 的可用性、登录状态和权限模型；不同地区、账号和模型配额会影响体验。
- 子 agent 仍可能产生错误结论或危险改动，不能绕过人工审查和测试。
- 写入型任务必须隔离 worktree；否则多 agent 并发编辑会制造冲突和难以追溯的状态。
- 项目 star 数较低且很新，适合作为模式样本，不宜直接视为成熟平台。

## 补充建议

- 优先把它用于只读审查、依赖风险扫描、架构第二意见等低冲突任务。
- 与 `codex-plugin-cc` 对照看：前者是 Claude Code 委派给 Antigravity，后者是在 Claude Code 中调用 Codex，二者都说明跨 agent 调用正在成为日常工作流。
- 在团队场景中，应把子 agent 产物限定为补充证据，最终合并仍由主仓库 CI 和 code owner 决定。

## 参考资料

- GitHub 仓库：<https://github.com/markfulton/claude-antigravity-agents>
- Google Antigravity CLI 文档：<https://antigravity.google/docs/cli/getting-started>
- Claude Code：<https://claude.com/claude-code>
