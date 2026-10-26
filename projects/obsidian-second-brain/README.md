<!-- markdownlint-disable MD013 -->

# obsidian-second-brain：让多个 Agent 读写可追溯的 Markdown 知识库

- 主上游：[eugeniughelbur/obsidian-second-brain](https://github.com/eugeniughelbur/obsidian-second-brain)；repository ID `1190557545`。
- 采样日期：2026-10-27（Asia/Shanghai）；分类：记忆层与个人 AI 基础设施。
- API 累计快照：4,954 stars / 607 forks / 6 open issues（含 PR 口径），与榜单日增分开。
- 默认分支 `main`；本页主线静态依据固定在 `58ca891156088635b4c28615d71a7842a8ca3143`。发行 API 首项 [v0.20.0](https://github.com/eugeniughelbur/obsidian-second-brain/releases/tag/v0.20.0)，UTC 2026-10-25T17:36:24Z，正式发行标记。
- 核验层级：读取一手文档、许可、元数据与所列部分实现；未安装运行上游、调用模型或复现实验。

## 定位

obsidian-second-brain 是围绕本地 Obsidian vault / Markdown 笔记组织的技能与脚本集合，覆盖保存、摄取、检索、任务、研究和知识整理。Crew 还提供跨 Agent 共享日志。它不是替代模型的记忆引擎，也不要求把全部资料迁到某个专用云数据库。

## 用法

先复制一份测试 vault 并保留 Git 历史 / 快照，再选择宿主安装方式。Claude Code 有原生插件与经典脚本路线；Codex、OpenCode 等在当前 README 中推荐统一 Agent Skills build，旧独立构建已标为弃用。

固定源码中可构建对应输出，本轮未执行：

```bash
bash scripts/build.sh --platform agent-skills
```

审阅生成的 dist/agent-skills 及安装说明后再放入测试 vault；配置 `OBSIDIAN_VAULT_PATH`，从保存、查找和健康检查开始。不要把该仓库当 Hermes plugin 直接安装，README 指出应走其 skills build。

## 原理

命令、AI-first 笔记约定和 adapter 将相同流程编译到各宿主。frontmatter、链接、来源和新鲜度帮助 Agent 找到实体页；已有概念优先改原页，再传播决策与任务到相关笔记。默认是关键词搜索，可选本地或远端 embedding；语义索引需重复 build 更新，过期或不可用时可回退。

`note_io.py` 提供同目录临时文件＋rename 的写入，以及写前比较原内容的冲突检查。后者缩短 Agent 思考期间的丢更新窗口，但源码明确它不是原子的比较交换，检查到 rename 之间仍有竞态，也没有证明所有 Agent 写入都走该函数。

## 价值

适合已有 Markdown 知识库，希望跨会话延续人物、决定和工作状态的用户。笔记可读、可迁出，便于逐次 review diff；自动整理是否改善检索和减少遗漏，要用真实问题金标衡量，不能直接推广作者特定 vault 的召回率。

## 风险边界

- 本地 Markdown 不代表本地推理：宿主模型、研究服务、Telegram 和云端 embedding 都可能外发内容。选择本地 embedding 也没有自动关闭其他出口。
- rewrite / reconcile 能修改既有知识；模型可能误合并人物、覆盖来源或把推断写成事实。原子替换只保护部分文件完整性，不提供语义正确、全批次事务或完整回滚。
- 后台 / 定时任务依宿主不同；插件的 background agent 需主动启用，Pi / Grok 的支持范围也不同。不能把总览中的 Always On 当成所有安装默认开启。
- README 现行总计为 49 个命令，跨平台因 calendar 限制少一项，FAQ 等段落还保留旧计数；以实际所构建树和宿主能力为准。
- MIT 代码许可不决定 vault 内材料、远端来源和外部服务的使用权；来源里的恶意指令仍应作为数据处理。

## 补充建议

先用十条合成笔记测试同名实体、冲突决定、过期事实和同步并发；每轮只做可审阅的小批量，审查 diff 后合并。保留 vault 自身历史，云端向量化前配置排除目录，核对索引新鲜度。暂不接后台任务，直到恢复与错误纠正机制可重复。

## 参考资料

- [README.md](https://github.com/eugeniughelbur/obsidian-second-brain/blob/58ca891156088635b4c28615d71a7842a8ca3143/README.md)。
- [references/write-rules.md](https://github.com/eugeniughelbur/obsidian-second-brain/blob/58ca891156088635b4c28615d71a7842a8ca3143/references/write-rules.md)。
- [scripts/build.sh](https://github.com/eugeniughelbur/obsidian-second-brain/blob/58ca891156088635b4c28615d71a7842a8ca3143/scripts/build.sh)。
- [scripts/note_io.py](https://github.com/eugeniughelbur/obsidian-second-brain/blob/58ca891156088635b4c28615d71a7842a8ca3143/scripts/note_io.py)。
- [LICENSE](https://github.com/eugeniughelbur/obsidian-second-brain/blob/58ca891156088635b4c28615d71a7842a8ca3143/LICENSE)。
- [仓库 API](https://api.github.com/repos/eugeniughelbur/obsidian-second-brain)、[发行 API](https://api.github.com/repos/eugeniughelbur/obsidian-second-brain/releases?per_page=1)；动态元数据仅代表本轮采样。
- 事实依据为以上一手材料；价值、风险判断与建议为本库工程分析，未写作实测结论。
