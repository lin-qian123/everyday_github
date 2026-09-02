<!-- markdownlint-disable MD013 MD034 -->

# Atlas：把 coding-agent 会话、上下文与提交关联起来的桌面工作台

## 项目概览

- 上游仓库：https://github.com/pacifio/atlas
- GitHub API 快照（2026-09-03）：2,845 stars、186 forks、21 个开放 issue
- 当前 release：`alpha-0.3.0`
- 主要技术：Rust / Tauri、ACP、Git checkpoints、本地向量检索、SQLite / JSONL
- 许可证：MIT

## 定位

Atlas 把 Claude Code、Codex、自带 agent 和 ACP registry 中的 CLI agents 放到同一个桌面工作区。它记录会话、工具调用、上下文与提交之间的关系，并让不同 agent 读取共享的项目记忆。

它更接近“面向 agents 的 source-control 工作台”，不是模型路由器或 OS sandbox。官方把当前版本标为 alpha，长尾 ACP agents 的兼容性仍在持续 QA。

## 用法

普通用户可从 release 下载桌面应用；源码构建需要 Rust、Bun 和平台相关 WebKit / GTK 依赖。外部 Claude Code 或 Codex 以 subprocess 通过 ACP 接入，项目知识放在 `.atlas/knowledge/`，现有 `AGENTS.md`、`CLAUDE.md` 和历史会话可进入本地索引。

首次试用宜放在可丢弃仓库，关闭团队同步，先观察导入哪些历史、生成哪些 `.atlas/` 数据、何时创建 checkpoint，以及 agent 实际继承了哪些上下文。

## 原理

Atlas 在消息送达 agent 前组装 `@` 引用、共享记忆、会话交接包和项目指令。Claude Code / Codex 作为外部 ACP 进程运行，自带 agent 则基于其 Rust 框架 Cersei 在进程内运行。

会话主要保存在本地 `.atlas/sessions.db`，commit 与产生它的 session 关联为 checkpoint；本地 embedding 与 HNSW 检索用于召回相关上下文。官方声称持久化前会做 secret scrubbing，但这仍需用真实敏感模式和误报/漏报样本验证。

## 价值

- 将“哪个 agent 为什么改了什么”与 Git 提交关联，便于审查和交接。
- 让多个 agent 共用决策、失败与架构记录，减少反复重建上下文。
- 笔记、canvas、session 采用 Markdown / JSON / JSONL 等可导出格式，降低应用锁定。
- 本地模式无需账号；团队同步是显式选择项。

## 风险边界

- Git checkpoint 和 transcript 不能证明代码正确、测试充分或推理可靠。
- 共享记忆会放大错误事实、过期决定和被污染指令；跨 agent 召回需要 provenance 与删除机制。
- “本地默认”不等于完全离线：外部模型/agent 自身仍可能联网，匿名 telemetry 默认开启。
- secret scrubbing 是上游声明，不应视为已完成的凭据安全证明；数据库、日志、备份与 crash dump 都要检查。
- 多 agent 同窗不等于文件或进程隔离；并发写入、branch/worktree 与外部工具权限仍须独立控制。
- 本页依据上游 README、release 与 API 静态核验，未安装，也未验证跨 agent 兼容性和长期记忆准确率。

## 补充建议

1. 固定 `alpha-0.3.0`，在无敏感数据的仓库分别测试 Claude Code、Codex 和内置 agent。
2. 用已知决策、撤销决定、同名文件和错误事实构造记忆回归集，记录召回率与错误传播。
3. 检查 `.atlas/`、系统日志、备份和同步出口，验证删除、导出、重建与 secret scrub。
4. 把 checkpoint 当作审查索引，不把会话解释当作测试、代码审查或安全证明。
5. 开启团队同步前先定义组织权限、保留期、离职回收和敏感仓库禁用策略。

## 参考资料

- 仓库与 README：https://github.com/pacifio/atlas
- Releases：https://github.com/pacifio/atlas/releases
- 官方站点：https://www.tryatlas.cc/
- 文档：https://docs.tryatlas.cc/
- 架构说明：https://github.com/pacifio/atlas/blob/main/ARCHITECTURE.md
- Telemetry 说明：https://github.com/pacifio/atlas/blob/main/TELEMETRY.md
