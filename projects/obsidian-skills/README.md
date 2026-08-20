<!-- markdownlint-disable MD013 -->

# Obsidian Skills

> 上游仓库：[kepano/obsidian-skills](https://github.com/kepano/obsidian-skills) · 归类：Agent 框架与技能生态 · 本页基于 2026-08-21 的上游 README 与 GitHub API 快照整理。

## 定位

`obsidian-skills` 是一组遵循 [Agent Skills](https://agentskills.io/specification) 规范的技能包，让兼容该规范的 agent 在 Obsidian vault 中读写 Obsidian Markdown、Bases、JSON Canvas，并调用 Obsidian CLI 或以 Defuddle 抽取网页正文。它是“让 agent 理解并操作本地知识库格式”的适配层，不是知识库同步服务、权限系统或事实核验器。

API 快照：约 46.9k stars、3.4k forks、64 个开放 issue；创建于 2026-01-02；API 许可证字段为 MIT。GitHub Trending 当日页面展示约 +292 stars，属于短期公开关注度，不能据此推断质量、安全性或生产成熟度。

## 用法

优先只在测试 vault 安装，再审查技能文件与宿主授权范围。

```sh
# Marketplace（适用于支持该插件命令的宿主）
/plugin marketplace add kepano/obsidian-skills
/plugin install obsidian@obsidian-skills

# 或使用 npx skills
npx skills add https://github.com/kepano/obsidian-skills
```

上游也列出了手动安装路径：Claude Code 可将内容置于目标 vault 的 `.claude`；Codex 通常复制 `skills/` 到 `~/.codex/skills`；OpenCode 则克隆完整仓库到其 skills 目录。安装后先以非敏感 Markdown、空白 Canvas 和只读 CLI 操作验证，再允许 agent 修改真实笔记。

## 原理

每个技能以 `SKILL.md` 描述宿主可调用的约束与操作模式：

- `obsidian-markdown`：处理 wikilink、嵌入、callout、properties 等 Obsidian 方言；
- `obsidian-bases`：编辑 `.base` 视图、过滤器、公式与汇总；
- `json-canvas`：以节点、边和分组编辑开放的 `.canvas` 格式；
- `obsidian-cli`：通过官方 CLI 与 vault、插件或主题交互；
- `defuddle`：去除网页杂质并提取 Markdown，以减少进入上下文的无关内容。

因此它把“模型生成文本”收敛到一套具体格式和操作契约；最终的文件访问、命令执行与网络访问仍由 agent 宿主和操作系统决定。

## 价值

- 把常用 vault 格式的结构性规则显式给 agent，降低把内部链接、属性或 Canvas JSON 写坏的概率。
- 采用跨宿主技能规范，方便在 Claude Code、Codex、OpenCode 等环境中复用同一领域知识。
- 可将网页提取、笔记结构化和本地 CLI 操作组织为可审查的知识维护流水线。

## 风险边界

- vault 可能含工作记录、个人资料、密钥或未公开研究；技能不提供租户隔离、加密或访问控制。
- agent 可误删、误链接、批量改写或将笔记内容发送给模型/provider；版本控制、备份与最小目录授权不可省略。
- Defuddle 的抽取结果不是原文证据，也不保证版权、登录态、动态内容或事实完整性。
- Marketplace、`npx` 和 Git clone 都引入供应链风险；固定 revision、审查 `SKILL.md`/脚本及依赖，避免直接对生产 vault 开放 shell/网络权限。

## 补充建议

1. 先复制一个最小 vault，在 CI 或 pre-commit 中检查 Markdown、JSON Canvas 和链接完整性。
2. 将可写范围限制为单独的 `agent-drafts/`，由人工审阅后再合并到正式笔记。
3. 对网页摘录保留原始 URL、抓取时间与关键引文，避免把模型摘要当作可追溯资料。
4. 记录安装版本和 hash；升级技能后用固定样例回归链接、属性、Canvas 与 CLI 行为。

## 参考资料

- [上游 README](https://github.com/kepano/obsidian-skills)
- [GitHub API 元数据](https://api.github.com/repos/kepano/obsidian-skills)
- [Agent Skills specification](https://agentskills.io/specification)
- [Obsidian CLI 文档](https://help.obsidian.md/cli)
