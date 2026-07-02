# self-learning-skills

- GitHub：<https://github.com/Kulaxyz/self-learning-skills>
- 抓取时间：2026-07-03（Asia/Shanghai）
- 今日信号：GitHub API 显示该仓库创建于 2026-06-28，抓取时约 `893 stars / 14 forks`，主题集中在 Claude Code、Cursor、Codex 与 `AGENTS.md` 风格的可复用技能沉淀。

## 定位

`self-learning-skills` 是一个面向 AI coding agent 的“元技能”：它不直接替用户写业务代码，而是教 agent 在一次艰难调试、部署、验证或排障之后，把真正可复用的路径沉淀成下一次会自动加载的 skill、rule 或项目记忆。

它关注的问题很具体：开发者和 agent 经常反复踩同一个环境坑、部署坑、验证坑；如果这些经验只停留在当前会话，下一次仍然从零开始。该项目试图把“这次终于跑通的路径”结构化保存下来。

## 用法

推荐路径是通过 `skills` CLI 安装：

```bash
npx skills add kulaxyz/self-learning-skills
npx skills add kulaxyz/self-learning-skills -g
npx skills add kulaxyz/self-learning-skills -a claude-code
```

也可以按不同 agent 手动放置：

- Claude Code / Codex / Agent Skills 客户端：写入 `skills/<name>/SKILL.md`。
- Cursor：写入 `.cursor/rules/learned/<name>.mdc`。
- Zed / Aider / Gemini CLI 等读取 `AGENTS.md` 的工具：追加到项目级说明或记忆文件。

## 原理

项目把经验沉淀拆成三个判断：

1. 识别：当前会话是否刚刚解决了一个以后可能重复出现的问题。
2. 路由：多步流程沉淀成 skill/rule，单点事实进入轻量记忆，一次性答案跳过。
3. 晋升：只有在有通过验证、命名失败模式、至少一个被排除的死路时，才把经验提升为可自动信任的技能。

这个设计比“把所有东西都记下来”更克制，重点是减少未来会话的重复试错，而不是无限膨胀上下文。

## 价值

- 对个人：把本地环境、部署路径、测试命令和故障经验变成 agent 可复用资产。
- 对团队：适合把“项目特有的黄金路径”沉淀成共享技能，降低新 agent / 新成员接手成本。
- 对 agent 生态：把 skill 从静态人工维护，推进到“从真实执行中采样并回写”的闭环。

## 风险边界

- 经验自动沉淀容易写入过期信息，需要定期清理或在 skill 中注明验证条件。
- 项目强调不写入 secret，但在真实团队中仍需做提交前审查，避免路径、内部系统名或环境细节泄露。
- 如果没有严格的通过验证标准，agent 可能把偶然成功的路径包装成“最佳实践”。

## 补充建议

- 与 `awesome-harness-engineering`、`loop-engineering`、`agents`、`nvidia-skills` 放在一起观察：前者偏方法论和技能市场，本项目偏从会话中自动收获技能。
- 团队使用时可以先限制在非敏感项目和 CI/测试流程，再逐步扩展到部署与生产排障。
- 适合纳入本仓库后续“agent skill 生命周期”横向比较。

## 参考资料

- GitHub 仓库：<https://github.com/Kulaxyz/self-learning-skills>
- `skills` CLI：<https://github.com/vercel-labs/skills>
