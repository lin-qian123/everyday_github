<!-- markdownlint-disable MD013 -->

# GitHub Agentic Workflows（github/gh-aw）

> 上游仓库：<https://github.com/github/gh-aw> · 归类：Agent 框架与技能生态 · 本页基于 2026-10-03 的 GitHub API、README、architecture / engine 文档、security policy、advisory、Release、tag 与 LICENSE 静态整理，未安装 CLI extension、编译 workflow 或在 GitHub Actions 中运行 Agent。

- 抓取快照：5,335 stars、572 forks、471 open issues。
- 热度信号：GitHub Go Trending 抓取时约 +12 当日 stars。
- 版本与许可：MIT；latest GitHub Release 为 `v0.89.21`，最新 tag 已到 `v0.90.2`，两者存在发布口径时差。

## 定位

GitHub Agentic Workflows（`gh-aw`）把 Markdown + YAML frontmatter 编译成标准 GitHub Actions workflow，让 Copilot、Claude Code、Codex、Gemini、Pi 等 engine 处理 issue triage、PR review、CI 故障调查、文档维护和依赖分析。它用于补充需要解释和推理的任务，不替代确定性的 build、test、lint 与 deploy。

## 用法

先运行 `gh extension install github/gh-aw`，在 Markdown frontmatter 中声明 trigger、permission、tool、engine 与 safe output，再用 `gh aw compile` 校验并生成 `.lock.yml`。生成的 Actions workflow 才是实际执行制品；engine 还需要对应 GitHub / provider 认证与模型额度。

## 原理

源码层把自然语言任务与运行配置分离：编译器生成固定 Actions graph，Agent job 默认只读并在 sandbox 中运行；需要写 GitHub 的操作通常先缓存在 `safe-outputs`，由独立 job 验证后以更窄权限应用。不同 engine 负责推理，GitHub Actions 提供 trigger、runner、secret、artifact 和 audit surface。

## 价值

团队可以 code-review Agent prompt、permissions 与 generated lock file，把非确定性自动化纳入既有 Actions 可见性；safe-output 分离也比直接给模型 write token 更容易审计。多 engine 支持降低单一 CLI 绑定，并允许把解释型步骤和确定性 CI 保持清晰边界。

## 风险边界

- “read-only / sandboxed by default”只描述受支持默认路径；作者可扩大 permissions、tools、network 和 runner，配置后仍可能获得 repo、secret 或外部系统写权限。
- issue、PR、代码、日志和依赖元数据都是不可信输入，可通过 prompt injection 影响 Agent；safe output 验证只覆盖配置的输出类型，不证明语义正确。
- compiler 生成 `.lock.yml` 后仍需审阅 diff；浮动 action、container、engine、model 与网络依赖会改变实际执行面。
- 上游曾披露 `>=0.83.3,<0.85.4` 的 `GHSA-8h78-hpm7-29gg` 并退役相关版本，说明版本固定与升级审计不能省略。
- Release `v0.89.21` 落后于 tag `v0.90.2`；只看 `/releases/latest` 或只追 tag 都可能误判当前推荐构建。
- Agent 的结论、review 与 issue 操作不具备事实保证；关键 merge、发布、删除、权限和 secret 变更仍需独立确定性 gate 与人工负责。

## 补充建议

从 fork / 测试仓库、只读 `GITHUB_TOKEN`、无 secret runner 与手动 dispatch 开始，固定 `v0.89.21` 或经审计的具体 tag / commit。提交 source Markdown 与 `.lock.yml`，在 CI 检查编译结果无漂移；为可写 safe output 设置类型、数量、路径、目标分支和人工 approval，并准备 prompt-injection fixture、恶意 issue / diff 与超预算失败测试。

## 参考资料

- [GitHub 仓库](https://github.com/github/gh-aw)
- [GitHub REST API](https://api.github.com/repos/github/gh-aw)
- [README 与安全默认](https://github.com/github/gh-aw/blob/main/README.md)
- [工作原理与 architecture](https://github.github.com/gh-aw/introduction/architecture/)
- [Engine reference](https://github.github.com/gh-aw/reference/engines/)
- [GHSA-8h78-hpm7-29gg](https://github.com/github/gh-aw/security/advisories/GHSA-8h78-hpm7-29gg)
- [v0.89.21 Release](https://github.com/github/gh-aw/releases/tag/v0.89.21)
- [v0.90.2 Tag](https://github.com/github/gh-aw/tree/v0.90.2)
- [LICENSE](https://github.com/github/gh-aw/blob/main/LICENSE)
