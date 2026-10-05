<!-- markdownlint-disable MD013 -->

# Agent Memory Repo（AgentMemoryRepo/agentmemoryrepo）

> 上游仓库：<https://github.com/AgentMemoryRepo/agentmemoryrepo> · 归类：记忆层与个人 AI 基础设施 · 本页基于 2026-10-06 的 GitHub API、README、文件结构规范、示例 skill 与 LICENSE 静态整理，未为真实用户创建记忆仓库、配置 remote 或验证多 Agent 合并。

- 抓取快照：162 stars、7 forks、1 open issue；仓库创建于 2026-10-04 22:10 UTC。
- 热度信号：GitHub Search 按新建仓库 stars 排序的早期开发者信号；不是 GitHub Trending 或社媒互动量。
- 版本与许可：MIT；无 GitHub Release / tag，也没有运行时 manifest；这是开放文件规范与示例 skill，不是记忆数据库产品。

## 定位

Agent Memory Repo 是由 Cognition 发起的开放规范：把跨会话 Agent 记忆放进独立 Git 仓库，以短 `MEMORY.md` 为入口，用 Markdown / SQL / 脚本承载主题内容，并依靠历史、权限与 merge 支持个人、团队和多 Agent 共享。

## 用法

规范要求每次会话先 clone / 更新记忆仓库，读取 `MEMORY.md` 并按任务 grep 或跟随 `[[path]]`，获得新信息后修改条目并单独 commit。上游示例 skill 默认只创建本地独立 repo，不自动添加 remote；只有用户明确给出自己拥有的私有仓库时才允许同步。

## 原理

记忆条目是单行 bullet，可在尾部写 `[source: ...; added: ...]`；主题文件通过相对 memory root 的双括号链接互相引用。多个用户或团队的 repo 保持分离并同时加载，Git 负责版本历史和显式冲突；“dreaming” 被描述为周期性 Agent，用于归纳、去重和核查矛盾，但规范仓库本身没有提供 scheduler 或运行实现。

## 价值

它复用 Agent 已熟悉的文件、grep、diff、commit 和权限工具，把记忆变化变成可审阅历史；短入口 + 按需链接也能避免每次加载全部材料。独立 repo 比把个人记忆混进业务代码仓库更容易设置所有权与迁移策略。

## 风险边界

- 规范不是运行时、加密、访问控制或自动加载实现；Git 历史只提供可追踪性，不保证事实正确、来源可信或当前有效。
- README 的 memory loop 提到 Agent 可“无人工介入”更新，但示例 skill 同时要求 clean worktree、无 secrets、独立 repo 和谨慎 push；采用时应以更严格的人工 / policy gate 为准。
- 删除当前文件不会从 Git 历史抹去敏感数据；密码、token、隐私信息和受监管数据不应进入普通记忆 repo。
- `source` 链接可能暴露私有会话 URL、客户标识或内部系统；多人组合 repo 时还会出现归属、同意、撤回和跨用户泄露问题。
- Merge 能显示文本冲突，却不能自动识别语义矛盾、过期事实、错误 SQL 或恶意记忆指令；“dreaming” 也可能进一步压缩错信息。
- 仓库创建不足两天且无版本 tag；格式、metadata 与跨链接语义仍可能快速变化。

## 补充建议

先用纯合成偏好在本地无 remote 仓库试验，明确“记忆是数据而非指令”，为写入、删除、用户归属和敏感分类制定 policy；每条关键事实保留可访问来源与复核日期。需要同步时只用受控私有 remote、分用户 repo 和 secret scanning，并建立冲突 / 撤回 / 历史清理流程。

## 参考资料

- [GitHub 仓库](https://github.com/AgentMemoryRepo/agentmemoryrepo)
- [GitHub REST API](https://api.github.com/repos/AgentMemoryRepo/agentmemoryrepo)
- [README 与 memory loop](https://github.com/AgentMemoryRepo/agentmemoryrepo/blob/main/README.md)
- [文件结构规范](https://github.com/AgentMemoryRepo/agentmemoryrepo/blob/main/SPEC.md)
- [示例 Agent skill](https://github.com/AgentMemoryRepo/agentmemoryrepo/blob/main/skills/agent-memory-repo/SKILL.md)
- [Cognition 发布页](https://cognition.ai/agent-memory-repo)
- [MIT LICENSE](https://github.com/AgentMemoryRepo/agentmemoryrepo/blob/main/LICENSE)
