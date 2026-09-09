<!-- markdownlint-disable MD013 -->

# fff（dmtrKovalenko/fff）中文解读

> 证据快照：2026-09-10（Asia/Shanghai）。GitHub REST API 显示 10,657 stars、443 forks、90 open issues，MIT；最新 release 为 `v0.10.6`。本文未运行 benchmark，速度、内存和集成范围均按上游材料分级记录。

## 定位

`fff` 是为人、编辑器和 AI agents 设计的文件搜索 toolkit。它以 Rust core 提供 typo-tolerant path/content search、frecency 排序、Git 状态注释、后台 watcher 与内存内容索引，并提供 MCP、Neovim、Rust、C、Python、Bun 和 Node.js 接口。

它的目标场景不是“一次性 shell grep”，而是同一长驻进程在同一代码库中反复搜索。

## 用法

MCP server 可通过 Homebrew 安装：

```bash
brew install dmtrKovalenko/fff/fff-mcp
codex mcp add fff -- "$(brew --prefix)/bin/fff-mcp"
```

连接后可调用 `ffgrep`、`fffind` 与 `fff-multi-grep`。上游也提供一行安装脚本，但正式使用前应先打开脚本审阅；SDK 用户可按语言选择对应 package，Neovim 用户可启用 picker。

## 原理

- Rust core 维护文件树、内容索引和 fuzzy / typo-tolerant 匹配算法。
- watcher 与 warm-up 让长驻进程复用已扫描状态，并按打开频率和最近使用情况调整排序。
- Git-aware annotations 把 modified、untracked 和 staged 状态并入结果，definition-first hinting 把更像代码定义的行前置。
- 切换 `cwd` 时会重建索引；默认最多阻塞约 10 秒，保证结果来自目标树，而非静默复用旧目录。

## 价值

- 对 coding agent 的重复检索可减少多轮 `rg` / `find` 子进程启动和重复扫描。
- frecency、定义优先与 Git 状态能让结果更贴近当前编辑上下文，而不只是纯文本匹配。
- 同一个 core 暴露多语言与 MCP 接口，方便编辑器、pre-commit、IDE 和 agent harness 共享行为。

## 风险边界

- “fastest / most accurate”和第二次搜索即可回本是上游 benchmark / 经验主张，本轮没有在固定硬件、仓库和查询集上复现。
- 性能以常驻索引换取内存：README 估算约 360 bytes / 可索引文件，10 万文件约 36 MB；大型仓库可能需要数百 MB。
- 单次终端搜索时，上游也承认 `rg` 更合适；不能把重复搜索优势推广到所有 workload。
- MCP server 获得的目录可见性取决于启动路径和 host 权限；索引可能包含敏感文件名或文本片段。
- 一行安装脚本、自动 release 与客户端配置属于供应链入口，必须固定版本、审阅脚本和二进制来源。

## 补充建议

1. 用本地真实仓库建立 cold/warm 两组基准，固定查询、缓存状态、RSS、CPU、正确结果集和重复次数，与 `rg` 分开比较。
2. 明确 `base_path`、ignore、binary / oversized file 与 symlink 策略，验证不会跨出授权 workspace。
3. 对错误 `cwd`、目录切换、watcher 漏事件、Git 大仓库和并发请求做回归；把 partial result 与 complete result 分开记录。
4. 若项目只偶尔搜索，不要为追求微秒延迟引入常驻索引与额外 MCP 权限。

## 参考资料

- GitHub：<https://github.com/dmtrKovalenko/fff>
- GitHub REST API：<https://api.github.com/repos/dmtrKovalenko/fff>
- Releases：<https://github.com/dmtrKovalenko/fff/releases>
- Rust 文档：<https://docs.rs/fff-search/latest/fff_search/>
- 上游内存讨论：<https://x.com/neogoose_btw/status/2041606853155811442>
- LICENSE：<https://github.com/dmtrKovalenko/fff/blob/main/LICENSE>
