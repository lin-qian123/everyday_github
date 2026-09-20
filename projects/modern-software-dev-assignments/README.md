<!-- markdownlint-disable MD013 MD034 -->

# modern-software-dev-assignments：Stanford CS146S 的 AI 软件开发作业库

> 上游仓库：https://github.com/mihail911/modern-software-dev-assignments · 归类：AI 学习与教育资源 · 本页基于 2026-09-21 的 README、八周 assignment、课程站点、manifest 与 REST API 静态整理；未运行作业、评分或核验课程 2026 版本。上游 README 仍写 Fall 2025，API description 写 2026/2025，存在元数据时差。

## 定位

该仓库是 Stanford CS146S “The Modern Software Developer” 的八周作业材料，从 prompting、tool calling、RAG 逐步走向 feature scaffold、MCP server、Claude Code / Warp 自动化、Semgrep、Graphite AI code review 和多 stack AI Web app。它是教学 starter / rubric，不是 Agent 工程能力的生产认证。

2026-09-21 的 GitHub 官方综合 / Python Trending 抓取显示约 `+174 stars today`；REST API 快照为 `4,540 stars / 1,009 forks / 31 open issues`，API 为 `NOASSERTION`，无 GitHub Release。仓库默认分支最后 push 为 2025-11-10，README 明确写 Fall 2025。

## 用法

上游要求 Python 3.12、Conda 与 Poetry：

```sh
conda create -n cs146s python=3.12 -y
conda activate cs146s
curl -sSL https://install.python-poetry.org | python -
poetry install --no-interaction
```

学习者应按 `week1` 到 `week8` 进入各 assignment，先读 requirements / rubric，再在 starter app 中完成 TODO、tests、writeup 和提交材料；不要把旧 dependency 或 vendor credit 说明直接带进当前环境。

## 原理

- Week 1 用代码样例比较 k-shot、self-consistency、reflexion、RAG 与 tool calling。
- Week 2 在现有应用中 scaffold feature、补 unit tests、refactor 并用 agentic mode 完成小任务。
- Week 3 要求实现 custom MCP server，训练 tool schema、transport 和可调用性思维。
- Weeks 4--5 分别用 Claude Code 与 Warp 构建 rules、commands、subagents / multi-agent workflow，并在 starter app 上交付证据。
- Weeks 6--8 转向 Semgrep 漏洞修复、Graphite AI code review 与多技术栈 AI Web app，rubric / writeup 用于约束结果说明。

## 价值

- 顺序覆盖 prompt、tool、context、automation、security、review 与 end-to-end build，比单个 demo 更接近完整开发循环。
- assignment、starter code、tests、deliverables 与 rubric 让学习成果更容易复核。
- 同时展示多个主流工具，适合比较“模型能力”和“harness / workflow 设计”的区别。
- 可作为课程设计、Agent onboarding 或内部 workshop 的参考框架。

## 风险边界

- README 与 API 的课程年份不一致，且默认分支最后 push 仍在 2025；不能把 Trending 回潮写成 2026 教材已更新。
- 根目录未见 LICENSE，GitHub API 也未识别 SPDX；在复制 starter code、rubric 或教学材料前需获得明确许可。
- 作业依赖 Claude Code、Warp、Semgrep、Graphite、Bolt 等外部服务，其价格、隐私、可用性和产品接口会变化。
- rubric 得分证明完成课程定义任务，不证明生成代码安全、原创、可维护或适合生产。
- 本页未安装依赖、运行 tests、提交作业或比较不同学生 / Agent 的表现。

## 补充建议

1. 使用固定 commit 作为 2025 baseline，并把每周外部工具、模型、价格和隐私条款做一次 2026 时效审计。
2. 在副本仓库、假 secret、合成数据与预算上限下完成作业；保留 prompt、diff、tests 和人工审阅。
3. 每周增加独立 verifier：功能 tests、安全扫描、事实 / citation 检查和回归测试，避免只按 Agent 自评打分。
4. 用于公开教学或再分发前先向上游确认许可证；明确课程完成不等于 Stanford 认证或生产资质。

## 参考资料

- 上游 README：https://github.com/mihail911/modern-software-dev-assignments
- 课程站点：https://themodernsoftware.dev
- Week 1 assignment：https://github.com/mihail911/modern-software-dev-assignments/blob/master/week1/assignment.md
- Week 3 MCP assignment：https://github.com/mihail911/modern-software-dev-assignments/blob/master/week3/assignment.md
- Week 8 assignment：https://github.com/mihail911/modern-software-dev-assignments/blob/master/week8/assignment.md
- GitHub REST API：https://api.github.com/repos/mihail911/modern-software-dev-assignments
