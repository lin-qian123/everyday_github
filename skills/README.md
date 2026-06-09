# Skills（vercel-labs/skills）

- GitHub: https://github.com/vercel-labs/skills
- 记录日期: 2026-04-30 (Asia/Shanghai)

## 这是什么

`skills` 是一个面向 Agent 技能生态的 CLI 工具，用来在不同 AI 编码代理之间安装、检索、更新、移除 `SKILL.md` 技能包。它强调“同一套技能，多代理复用”（如 Codex、Claude Code、Cursor、OpenCode）。

## 热度信号

1. GitHub 仓库约 `16.5k stars`（2026-04-30 抓取快照）。
2. GitTrend/Trendshift 近期趋势里，“AI skills”持续处于高热主题。

## 怎么用（最短路径）

```bash
# 列出某仓库可安装的技能
npx skills add vercel-labs/agent-skills --list

# 安装指定技能
npx skills add vercel-labs/agent-skills --skill frontend-design

# 查看本机已安装技能
npx skills list
```

## 核心原理

1. 统一分发层：把 GitHub/Git URL/本地路径抽象成一致技能来源。
2. 代理适配层：按 `--agent` 参数将技能落到不同代理的技能目录。
3. 安装策略：支持软链接（便于更新）与复制（兼容受限环境）两种方式。

## 适用场景

1. 团队要把工程规范批量下发到多种 AI 编码工具。
2. 需要快速试验并回滚不同技能集合。
3. 希望将技能管理纳入 CI/CD 与项目初始化流程。

## 价值与风险

价值：
- 显著降低技能分发与版本漂移成本。
- 让“流程最佳实践”更容易标准化落地。

风险：
- 技能来源质量差异大，可能引入低质量或冲突规则。
- 跨代理行为不完全一致，仍需验证执行结果。

## 我认为有价值的补充材料

1. 给技能仓库增加可信来源白名单与签名校验。
2. 在团队内维护“基线技能包 + 项目增量技能包”两层结构。
3. 对关键技能建立回归任务，防止更新后行为退化。

## 参考来源

- https://github.com/vercel-labs/skills
- https://gittrend.io/
- https://trendshift.io/
