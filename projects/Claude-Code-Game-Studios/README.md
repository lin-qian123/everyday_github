<!-- markdownlint-disable MD013 -->

# Claude Code Game Studios（Donchitos/Claude-Code-Game-Studios）

> 上游仓库：<https://github.com/Donchitos/Claude-Code-Game-Studios> · 归类：Agent 框架与技能生态 · 本页基于 2026-10-02 的 GitHub API、README、hooks / rules / templates、security policy、Release 与 LICENSE 静态整理，未克隆模板、启动游戏引擎或运行 Claude Code。

- 抓取快照：25,624 stars、3,650 forks、58 open issues。
- 热度信号：GitHub Shell Trending 抓取时约 +47 当日 stars。
- 版本与许可：MIT；latest Release / tag 为 `v1.1.2`。

## 定位

Claude Code Game Studios 是把游戏开发流程编码成 Claude Code 项目模板的“虚拟工作室”：49 个角色 Agent、74 个 workflow Skill、12 个事件 hook、13 组路径规则和 39 个文档模板覆盖设计、程序、美术、音频、叙事、QA、制作与发行，并分别提供 Godot、Unity 与 Unreal 专门角色。

## 用法

将仓库 clone / 作为 template 创建新游戏，进入目录运行 Claude Code，再用 `/start` 选择项目阶段、引擎和 rigor；也可直接调用 `/brainstorm`、`/setup-engine`、`/create-stories`、`/dev-story`、`/story-done` 等 Skill。`project.yaml` 是团队配置源，个人覆盖写进 gitignored 的 `project.local.yaml`。

## 原理

角色按 director、department lead、specialist 分层，垂直委派、横向咨询、冲突上提与跨部门变更传播形成组织图。path-scoped rules 给 gameplay、engine、network、UI 等目录加载不同规范；session、commit、push、asset 与 compaction hooks 提供提示或验证；`modes.rigor` 将 workflow、文档密度、QA、story 粒度、review 与 team size 联动为 minimal / standard / full。

## 价值

它把容易遗忘的游戏设计、架构决定、视觉检查、可访问性和发行门槛放进可审阅文件，而不是只依赖长对话。对个人或小团队，minimal 模式提供从 brief 到可运行切片的轻路径；已有项目也能通过 `/adopt` 与反向文档逐步接入。

## 风险边界

- 49 个角色只是提示、规则与委派结构，不等于真实跨专业团队；同一基础模型的多个角色会共享盲点，也可能扩大 token / API 成本。
- shell hooks 在本机、用户权限下执行；README 的人工批准约定与权限提示不是 OS sandbox，第三方更新仍应按可执行供应链审查。
- 上游对四个游戏、文档数量与 blind review 的比较是项目方测量，样例游戏本身未随仓库提供，本轮无法复验设计质量或时间数字。
- standard / full 模式可生成大量文档；traceability 不自动带来更好玩法，反而可能延迟真实 prototype 与 playtest。
- screenshot 与自动测试不能覆盖手感、叙事、完整可访问性、性能波动、平台认证和在线安全。
- 引擎、插件、模型、生成美术 / 音频 / 代码和商用素材各自有许可与来源要求，仓库 MIT 只覆盖模板代码和文档。

## 补充建议

在可丢弃项目副本固定 `v1.1.2`，先用 minimal 模式制作一个垂直切片；审阅 `.claude/settings.json` 与所有 hooks，再只开放所需目录、命令和网络。为每个故事保留真实引擎运行、截图 / 视频、性能与 playtest 证据，同时统计文档时间与返工率；只有观察到明确收益时才提高 rigor 或启用更多角色。

## 参考资料

- [GitHub 仓库](https://github.com/Donchitos/Claude-Code-Game-Studios)
- [GitHub REST API](https://api.github.com/repos/Donchitos/Claude-Code-Game-Studios)
- [README 与 workflow 说明](https://github.com/Donchitos/Claude-Code-Game-Studios/blob/main/README.md)
- [Agents](https://github.com/Donchitos/Claude-Code-Game-Studios/tree/main/.claude/agents)
- [Skills](https://github.com/Donchitos/Claude-Code-Game-Studios/tree/main/.claude/skills)
- [Hooks](https://github.com/Donchitos/Claude-Code-Game-Studios/tree/main/.claude/hooks)
- [SECURITY](https://github.com/Donchitos/Claude-Code-Game-Studios/blob/main/SECURITY.md)
- [v1.1.2 Release](https://github.com/Donchitos/Claude-Code-Game-Studios/releases/tag/v1.1.2)
- [LICENSE](https://github.com/Donchitos/Claude-Code-Game-Studios/blob/main/LICENSE)
