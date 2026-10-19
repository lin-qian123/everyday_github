<!-- markdownlint-disable MD013 -->

# Claude Code Action

> 更新：2026-10-20（Asia/Shanghai）。分类：Coding Agents 与终端助手。上游 `anthropics/claude-code-action`；快照 `db77d4d3c98f`（main）。本文基于官方榜单、认证 API 与上游文件静态研究；热度、版本时间与跨平台证据见[当日日报](../../daily/2026-10-20/ai-hotspots.md)。

## 定位

Anthropic 将 Claude Code 接入 GitHub PR / issue 的 Action，可响应 @claude、分配事件或显式 prompt，回答仓库问题、审查变更及生成代码。运行位置是自己的 GitHub runner；模型请求仍送到选定 provider。它是 CI 中的 Agent 执行层，不是独立模型。[README.md](https://github.com/anthropics/claude-code-action/blob/db77d4d3c98f3f6380e7cd45ffba2342a3dbde3c/README.md)

## 用法

仓库管理员可在 Claude Code 运行 `/install-github-app`，安装 GitHub App 并配置 secrets；此快捷路径面向 Anthropic 直连用户。Bedrock、Vertex AI、Foundry 应按云 provider 文档配置身份。手工 workflow 使用 `anthropics/claude-code-action@v1`，以 `prompt` 和 `claude_args` 控制任务；生产应把已审查版本固定到完整 commit。[README.md](https://github.com/anthropics/claude-code-action/blob/db77d4d3c98f3f6380e7cd45ffba2342a3dbde3c/README.md)[docs/setup.md](https://github.com/anthropics/claude-code-action/blob/db77d4d3c98f3f6380e7cd45ffba2342a3dbde3c/docs/setup.md)

先在测试仓库做只读问答 / review，给出最小 workflow permissions、模型额度和明确成功条件，再考虑允许写分支。本轮未安装 App、添加 secrets 或运行 workflow。

## 原理

Action 根据 GitHub 事件选择执行模式，检查触发者权限、建立短期仓库 token，再在 runner 启动 Claude Code；`action.yml` 暴露模型认证、工具参数、结构化输出和日志控制。安全文档说明 PR 场景会从 base 恢复一组 Claude 配置文件，而低层 `claude-code-base-action` 不提供同等 actor 检查与配置恢复。[action.yml](https://github.com/anthropics/claude-code-action/blob/db77d4d3c98f3f6380e7cd45ffba2342a3dbde3c/action.yml)[docs/security.md](https://github.com/anthropics/claude-code-action/blob/db77d4d3c98f3f6380e7cd45ffba2342a3dbde3c/docs/security.md)

## 价值

适合把仓库问答、可复核 review、issue 分类和文档同步接到现有 CI，使输入事件、生成 diff、测试与结果链接留在同一审计链中。代码正确率、维护成本与节省时间需要用实际任务衡量。

## 风险边界

- 默认要求事件触发者具备仓库写权限，bots 默认不允许；`allowed_bots` 匹配项会跳过仓库权限检查，公开仓库使用 `*` 可引入外部 App 输入。`allowed_non_write_users` 则明确绕过主要权限门槛，不能把它当作普通协作选项。[docs/security.md](https://github.com/anthropics/claude-code-action/blob/db77d4d3c98f3f6380e7cd45ffba2342a3dbde3c/docs/security.md)[action.yml](https://github.com/anthropics/claude-code-action/blob/db77d4d3c98f3f6380e7cd45ffba2342a3dbde3c/action.yml)
- `pull_request_target` / `workflow_run` 可带 base 仓库 secrets；执行前把不可信 PR head checkout 到工作区根目录会扩大风险。配置恢复和文本清洗只覆盖特定路径 / 输入，不构成任意代码隔离或完整 prompt injection 防护。[docs/security.md](https://github.com/anthropics/claude-code-action/blob/db77d4d3c98f3f6380e7cd45ffba2342a3dbde3c/docs/security.md)
- `show_full_output` 会公开工具结果等敏感内容；Actions debug 模式也会自动启用完整输出。自托管 runner、模型 provider、GitHub token 和额外 MCP 各有独立数据 / 权限边界。[docs/security.md](https://github.com/anthropics/claude-code-action/blob/db77d4d3c98f3f6380e7cd45ffba2342a3dbde3c/docs/security.md)
- 采样 latest Release 为历史 `v1`，不是今天新发版；本文固定的是当前主分支文件，不能保证所有已安装 `@v1` 行为与其一致。仓库代码 MIT，模型服务与云资源另行计费。[LICENSE](https://github.com/anthropics/claude-code-action/blob/db77d4d3c98f3f6380e7cd45ffba2342a3dbde3c/LICENSE)

## 补充建议

建立写权限用户、外部贡献者、允许 bot 三组触发夹具，核对实际运行 / 拒绝结果；把 secret canary、最小 token scope、成本上限、最终 diff 和必需测试作为验收项。升级前比较固定 Action commit、base-action 与 runner 镜像，不只检查 workflow 是否退出成功。

## 参考资料

- [README.md](https://github.com/anthropics/claude-code-action/blob/db77d4d3c98f3f6380e7cd45ffba2342a3dbde3c/README.md)
- [LICENSE](https://github.com/anthropics/claude-code-action/blob/db77d4d3c98f3f6380e7cd45ffba2342a3dbde3c/LICENSE)
- [docs/security.md](https://github.com/anthropics/claude-code-action/blob/db77d4d3c98f3f6380e7cd45ffba2342a3dbde3c/docs/security.md)
- [action.yml](https://github.com/anthropics/claude-code-action/blob/db77d4d3c98f3f6380e7cd45ffba2342a3dbde3c/action.yml)
- [docs/setup.md](https://github.com/anthropics/claude-code-action/blob/db77d4d3c98f3f6380e7cd45ffba2342a3dbde3c/docs/setup.md)
- [仓库 API](https://api.github.com/repos/anthropics/claude-code-action)
- [v1 Release](https://github.com/anthropics/claude-code-action/releases/tag/v1)
