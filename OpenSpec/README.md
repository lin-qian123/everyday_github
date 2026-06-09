# OpenSpec

## 项目定位
`OpenSpec` 是一个面向 AI 编码助手的 Spec-Driven Development（SDD）框架，核心目标是在动手写代码前先把需求、变更边界和任务拆解固定下来，降低“聊天里说过但代码里没落地”的不确定性。

- GitHub：https://github.com/Fission-AI/OpenSpec
- 官方站点：https://openspec.dev/
- 适用人群：高频使用 Codex、Claude Code、Cursor、OpenCode、Copilot 一类 AI 编码工具的个人开发者和团队。

## 用法

从官方 README 暴露的信息看，`OpenSpec` 的使用方式很明确：

1. 安装 CLI：
   - `npm install -g @fission-ai/openspec@latest`
2. 在现有项目里执行初始化：
   - `openspec init`
3. 让它生成 `openspec/` 目录、项目级 `AGENTS.md` 交接说明，以及对应 AI 工具的 slash commands。
4. 之后通过提案、规格、任务几个层次推进开发，并用：
   - `openspec list`
   - `openspec update`
   来查看活跃变更和刷新指令。

它不是“再加一份 README”，而是把一次需求变更拆成可审阅、可追踪的结构化工件。

## 原理

`OpenSpec` 解决的是 AI 编程里最常见的一类失败模式：需求只存在于聊天上下文，结果实现偏离预期。

它的核心设计可以概括成四层：

- 规格层：把当前事实和目标行为写进 `openspec/specs/`。
- 变更层：把待讨论或待实现的修改写进 `openspec/changes/`，让提案与事实分离。
- 协作层：让人类和 AI 在“写代码之前先对齐规格”，减少提示词漂移。
- 工具层：通过 slash commands 和项目级指令文件，把同一套流程接到 20+ AI 助手上。

官方 README 明确强调两点：一是“先对齐再编码”，二是它比偏 0->1 的重型 spec 流程更轻，尤其适合对既有项目做 1->n 迭代。

## 价值

- 对 AI 编码团队，最大的价值不是“多一层文档”，而是让需求和实现的偏差更容易被发现。
- 它对存量项目特别有用，因为很多团队真正痛的不是新建项目，而是已有系统上的连续变更。
- 兼容的 AI 工具足够多，不会把团队锁进单一 IDE 或单一模型提供商。

## 风险边界

- `OpenSpec` 不会自动提高团队的需求质量，只会把已有问题更明确地暴露出来。
- 如果团队没有最基本的评审习惯，规格文件也可能退化成“另一层形式化噪音”。
- 它更适合中等及以上复杂度的变更；对极小型脚本改动，流程成本可能高于收益。

## 补充建议

- 如果你已经在用 AI 写代码但经常返工，优先把 `OpenSpec` 用在跨文件、多角色、多阶段的需求上，而不是所有修改都强制上 SDD。
- 最值得借鉴的是“当前事实”和“提议变化”分开存放的目录设计，这比把所有讨论堆在聊天记录里更可审计。
- 它可以和现有工程文档体系并存，不需要替换 README、设计文档或 issue 流程。

## 参考资料

- 仓库主页：https://github.com/Fission-AI/OpenSpec
- 官方站点：https://openspec.dev/
- GitHub 仓库 About：https://github.com/Fission-AI/OpenSpec
- GitHub Trending：https://github.com/trending
