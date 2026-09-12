<!-- markdownlint-disable MD013 -->

# Worktrunk（max-sixty/worktrunk）中文解读

> 证据快照：2026-09-13（Asia/Shanghai）。GitHub REST API 显示 7,211 stars、256 forks、39 open issues，最新 release 为 `v0.77.0`。API 许可证字段为 `NOASSERTION`，根 `LICENSE` 明确允许用户在 MIT 或 Apache-2.0 中任选其一。本文未安装 CLI、创建 worktree、执行 hook 或合并分支。

## 定位

Worktrunk 是面向并行 AI coding agents 的 Git worktree CLI。它把创建/切换、列举状态、合并和清理抽象成 `wt switch`、`wt list`、`wt merge`、`wt remove`，并用路径模板、hooks、每分支变量和缓存共享降低管理多个工作目录的操作成本。

它解决的是 Git 工作区编排，不是 agent runtime 或安全沙箱。不同 worktree 能减少文件写冲突，但仍共享同一个 Git object database、用户身份、系统权限、凭据与外部服务。

## 用法

macOS/Linux 可用 Homebrew 安装并启用 shell 集成：

```bash
brew install worktrunk
wt config shell install
wt switch --create feature-auth
wt list
```

也可用 Cargo 安装。并行 agent 示例通过 `wt switch -x <agent> -c <branch> -- '<prompt>'` 创建 worktree 后启动命令；正式项目中应先在测试仓库检查路径模板、hook、base branch 与 remove/merge 行为。

## 原理

- 分支名映射到可配置 worktree 路径，shell integration 让 `wt switch` 能改变当前目录。
- `wt list` 汇总脏文件、ahead/behind、remote、commit、CI 和可选 AI summary，形成多 worktree 状态面板。
- hook 可在 create、start、pre/post-merge 等阶段执行依赖安装、服务启动、校验或清理命令。
- `wt merge` 可组合提交、rebase/fast-forward、合并和后台清理；`wt step` 暴露更细的可组合操作。
- APFS、btrfs、XFS 上可复制 ignored build cache，减少多个 worktree 重复安装/构建。

## 价值

- 用显式目录隔开并行修改，降低多个 agent 同写一个 working tree 的直接冲突。
- 状态汇总和统一清理让操作者更容易识别未提交、未推送与已合并分支。
- hooks 与分支变量可把依赖、端口和验收步骤模板化，适合批量 agent 会话。
- CLI 保持在 Git 原语之上，出错时仍可用 `git worktree`、branch 和 reflog 检查真实状态。

## 风险边界

- worktree 不是 OS sandbox：恶意脚本仍可读取用户目录、环境变量、SSH key、云凭据和其他 worktree。
- `wt merge`、自动提交、LLM commit message 与清理会修改 Git 状态；错误 base、hook 或未审 diff 可把问题快速带入主分支。
- 复制 ignored cache 能传播损坏或被污染的依赖/构建产物；不同分支未必兼容同一 cache。
- hooks 和 aliases 是命令执行供应链；从仓库或团队配置继承后必须像 CI 脚本一样审计。
- API 未识别 SPDX 不等于无许可；实际根文件是 MIT OR Apache-2.0，但依赖与发行包仍应分别检查。

## 补充建议

1. 先在可丢弃仓库验证 create/list/remove，默认关闭自动 merge、LLM commit 和第三方 hooks。
2. 每个 agent 使用独立端口、测试数据库和最小凭据；不要让 worktree 路径隔离替代系统权限隔离。
3. 合并前执行 `git status`、diff、测试与人工 review，并确认主分支、remote 和未推送提交。
4. 对 cache、hook、shell integration 与配置文件固定版本，记录失败恢复和残留 worktree 的清理流程。

## 参考资料

- GitHub：<https://github.com/max-sixty/worktrunk>
- GitHub REST API：<https://api.github.com/repos/max-sixty/worktrunk>
- Releases：<https://github.com/max-sixty/worktrunk/releases>
- 官方文档：<https://worktrunk.dev>
- Git worktree 文档：<https://git-scm.com/docs/git-worktree>
- 上游发布 X 帖：<https://x.com/max_sixty/status/2006077845391724739>
- LICENSE：<https://github.com/max-sixty/worktrunk/blob/main/LICENSE>
