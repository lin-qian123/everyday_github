<!-- markdownlint-disable MD013 MD034 -->

# code-review-graph：给 Coding Agent 使用的本地代码知识图谱

> 上游仓库：https://github.com/tirth8205/code-review-graph · 归类：RAG、检索与知识处理 · 本页基于 2026-09-19 的 README、复现文档、`pyproject.toml`、release、LICENSE 与 REST API 静态整理；未在本机建立图谱或复跑 benchmark。

## 定位

`code-review-graph` 用 Tree-sitter 把仓库解析为函数、类、导入、调用、继承和测试关系图，再通过 CLI、MCP 与 GitHub Action 向 Coding Agent 返回与问题或改动相关的最小上下文。它解决的不是“再做一个聊天助手”，而是让现有 Claude Code、Codex、Cursor、OpenCode 等工具少读无关文件，并显式查看改动的 blast radius。

2026-09-19 的 GitHub 官方 Python Trending 抓取显示约 `+50 stars today`；REST API 快照为 `31,592 stars / 2,872 forks / 132 open issues`，MIT，默认分支为 `staging`。同日最新 release 为 `v2.3.9`。

## 用法

项目要求 Python `>=3.10`：

```sh
pip install code-review-graph
code-review-graph install
code-review-graph build
```

`install` 会检测本机 Agent 客户端，写入 MCP 配置，并在受支持的平台安装 hook、skill 或规则文件；也可用 `--platform codex` 等参数只配置一个客户端。CI 侧可使用 `tirth8205/code-review-graph@v2.3.9`，在 PR 上生成风险函数、执行流和测试缺口评论。

## 原理

- Tree-sitter 与针对框架的 resolver 把源码写入 SQLite 图，节点表示文件、类和函数，边表示调用、导入、继承与测试覆盖。
- SHA-256、Git diff、watch mode 与 hooks 只重解析变化文件及受影响依赖；上游在约 3,000 文件仓库上报告两文件编辑的 hook 路径约 2.5 秒。
- 查询阶段先做关键字 / 向量检索，再沿调用和依赖边扩展，把 compact context 通过 MCP 返回给模型。
- GitHub Action 在 runner 内构图；上游说明源码不发往外部服务，但 Action 仍需要 checkout、缓存和 PR 写权限。
- 上游六仓库快照报告每问题相对“读取完整语料”的 token 中位缩减约 63 倍；README 同时明确该基线是上界，impact recall 使用同一图生成 ground truth，存在循环性。

## 价值

- 将“模型自己 grep”升级为可复用、可增量更新的结构化索引，适合大仓库审阅和影响分析。
- MCP、CLI 与 CI 共用一份本地图，可以让交互审阅和合并门禁围绕相同关系数据展开。
- 多语言解析、notebook 支持、可复现脚本和明确的 benchmark limitations，比只给营销数字更便于技术选型。
- 图结果可解释为具体节点与边，便于人工追问为什么某文件被纳入上下文。

## 风险边界

- `install` 会修改 Agent 配置、hooks、skills 与规则文件；应先用可丢弃配置、`--dry-run` 或单平台安装检查写入范围。
- 静态图会漏掉反射、动态导入、运行时注册、字符串调用与框架魔法；README 也承认 JavaScript / Go flow detection 和搜索排序仍需改进。
- 上游 63 倍数字使用完整语料作为基线，真实 Agent 通常会先 grep；尚未发布 canonical agent-baseline 捕获，不能写成实际成本必然下降 63 倍。
- graph-derived ground truth 使 recall `1.0` 只是构造上界；co-change 模式在上游快照中尚未给出可用结果。
- 本地图不等于数据无泄露：后续被选中的源码片段仍会发往所配置的模型 provider。
- 本页未复跑 `v2.3.9`、未验证 40 秒 cold build、2.5 秒增量、F1、跨语言准确率或 CI 权限最小化。

## 补充建议

1. 用固定 commit、真实 review 问题和人工标注影响文件，对比纯 grep、语言服务器与图查询，而不是只比较完整语料 token。
2. 先在副本仓库运行 `install` / `uninstall --dry-run`，记录每个客户端配置、hook 与 rules 文件的差异。
3. 对动态调用、monorepo、生成代码、notebook 和框架 DI 单独建漏检集，同时统计 false positive 和人工审阅时间。
4. CI 只授予 `contents: read` 与必要的 PR comment 权限，锁定 Action tag / commit，并独立验证 cache 与第三方依赖供应链。

## 参考资料

- 上游 README：https://github.com/tirth8205/code-review-graph
- `v2.3.9` release：https://github.com/tirth8205/code-review-graph/releases/tag/v2.3.9
- Benchmark 复现说明：https://github.com/tirth8205/code-review-graph/blob/staging/docs/REPRODUCING.md
- GitHub Action 文档：https://github.com/tirth8205/code-review-graph/blob/staging/docs/GITHUB_ACTION.md
- GitHub REST API：https://api.github.com/repos/tirth8205/code-review-graph
- LICENSE：https://github.com/tirth8205/code-review-graph/blob/staging/LICENSE
