# open-knowledge

## 1. 项目定位

`open-knowledge` 是 Inkeep 开源的 AI-native Markdown 编辑器和 LLM Wiki 工具，面向知识库、规格文档、工程 notes、MDX 内容和 agent second brain。

它把 WYSIWYG Markdown 编辑、macOS 桌面应用、本地 Web UI、MCP、skills、agentic search、git/GitHub 同步和团队共享放在一个知识工作台里，目标是让 Claude、Codex、Cursor 等 agent 能直接围绕本地文档协作。

## 2. 基本用法

macOS 用户可以下载桌面应用。Linux、Windows 和 Intel Mac 用户可通过 CLI 启动本地 Web 编辑器，官方 README 给出的命令是：

```bash
npm install -g @inkeep/open-knowledge
cd your-project
ok init
ok start --open
```

`ok init` 会初始化项目并接入 Claude Code、Cursor、Codex 等 harness 的 MCP 和 skill 配置。用户也可以打开已有 Markdown/MDX 文件夹、Obsidian vault 或工程 wiki。

## 3. 核心原理

`open-knowledge` 的核心是把 Markdown 文件夹变成 agent 可协作的知识工作区：

- WYSIWYG 编辑让 Markdown 像文档工具一样可视化编辑。
- 文件导航、搜索、标签页和 graph wiki link viewer 提供知识库浏览能力。
- MCP、CLI 和 skills 将本地知识库暴露给 agent。
- Git/GitHub 用作底层同步和分享机制。
- 可嵌入 HTML 与富组件让工程规格、报告和可视化内容留在文档体系中。

## 4. 工程价值

很多 agent 项目都在解决“上下文如何长期沉淀”的问题。`open-knowledge` 不是只做向量记忆，而是把人类可读的 Markdown wiki 作为协作界面，让人和 agent 都能编辑、搜索、引用和同步同一套知识。

它适合团队把规格、设计决策、运行手册、研究 notes 和 agent 技能说明放在一个版本化目录中，比纯聊天记录或闭源笔记工具更适合工程审计。

## 5. 风险边界

- 采用 GPL-3.0-or-later 许可证，商业集成或分发前需要评估合规边界。
- 自动初始化 MCP / skills 可能改动项目配置，应在版本控制下审查。
- 本地知识库若同步到 GitHub，需要单独处理私密文档、密钥、客户数据和内部链接。
- WYSIWYG 编辑不应破坏已有 Markdown/MDX 工程约定，尤其是文档站、博客或规范仓库。

## 6. 补充建议

- 适合和 `Personal_AI_Infrastructure`、`open-notebook`、`supermemory`、`codebase-memory-mcp` 横向比较。
- 在工程仓库中试用时，先用独立 `docs/` 或 wiki 目录，不要直接让 agent 扫描全部敏感内容。
- 对长期项目来说，它更像“人机共享知识层”，不是单纯的 RAG 检索库。
- 本仓库将其放入 `记忆层与个人 AI 基础设施`，因为它强化的是长期知识组织和 agent second brain。

## 7. 参考资料

- GitHub 仓库：https://github.com/inkeep/open-knowledge
- 官方网站：https://openknowledge.ai
- 文档：https://openknowledge.ai/docs
- 最新发布：https://github.com/inkeep/open-knowledge/releases/latest

