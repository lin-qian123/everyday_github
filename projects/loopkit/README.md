# loopkit

<!-- markdownlint-disable MD013 -->

## 定位

`loopkit` 是 Archive228 发布的 coding agent harness 与 skill 库。它把 `.claude/` 配置、hooks、verifier subagent、MCP 配置、memory 文件和 49 个小型 skill 打包成可直接放进项目的工作底座，目标是让 Claude Code、Cursor、Codex、Gemini CLI 等 agent 按“Plan -> Act -> Verify”的闭环工作。

截至 2026-07-11，GitHub API 显示该仓库约 472 stars，创建于 2026-06-30，许可证为 MIT。README 强调它不是新方法论或运行时，而是一套文件级 harness：没有 daemon，没有复杂 CLI，核心脚本 `run.sh` 很小。

## 用法

快速安装示例：

```bash
curl -fsSL https://raw.githubusercontent.com/Archive228/loopkit/main/install.sh | bash
echo "STATUS: not-started" > IMPLEMENTATION_PLAN.md
./run.sh
```

安装后项目中会出现 `.claude/CLAUDE.md`、`.claude/settings.json`、verifier subagent、hooks、skills、`.mcp.json`、`MEMORY.md` 和 `run.sh` 等文件。已有文件默认不覆盖，可用 `FORCE=1` 或 `BACKUP=1` 改变行为。

## 原理

loopkit 的核心不是“让模型更聪明”，而是把工作状态放在磁盘文件中，让 agent 每轮都围绕 plan、act、verify 推进。skill 采用 Markdown + YAML frontmatter，按任务触发加载；verifier subagent 用偏对抗的审查方式检查“假完成”。

它的 49 个 skill 覆盖上下文预算、spec-first、工具克制、调试、安全、测试、重构、文档、数据、git-ops 等轨道。每个 skill 都尽量短小，避免把所有规则塞进常驻上下文。

## 价值

- 适合团队把 agent 工作方式固化到项目文件，而不是靠个人 prompt 习惯。
- 对 Codex / Claude Code / Cursor 等多宿主兼容，降低供应商绑定。
- 强调 verifier 和磁盘状态，适合长任务、多人接续和复盘。
- MIT 许可证，便于拆出少数有用 skill 单独采用。

## 风险边界

- 这是强意见 harness，直接导入可能和已有 `AGENTS.md`、`.claude/`、MCP 配置冲突。
- verifier subagent 只是一层审查，不等于真实测试、CI 或安全扫描。
- README 中 star 数和 skill 数可能随时间变化，接入前应固定版本或 commit。
- 团队若已有成熟规范，应选择性移植，而不是整包覆盖。

## 补充建议

- 与 `awesome-harness-engineering` 横向比较：前者偏资料索引，loopkit 偏可直接落盘的 harness。
- 与 `self-learning-skills`、`token-diet`、`fable-soul` 一起观察，看 skills 是否会从个人经验库演化为团队工程标准。
- 引入时建议先在小项目试运行，确认 hooks、权限和 verifier 输出不会干扰现有 CI。

## 参考资料

- GitHub 仓库：<https://github.com/Archive228/loopkit>
- skills.sh 页面：<https://www.skills.sh/>
- awesome-harness-engineering：<https://github.com/ai-boost/awesome-harness-engineering>
- self-learning-skills：<https://github.com/Kulaxyz/self-learning-skills>
