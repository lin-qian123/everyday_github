<!-- markdownlint-disable MD013 -->

# clawk

## 定位

`clawkwork/clawk` 是一个面向 coding agent 的本地 disposable Linux VM sandbox。它主张不要把 Claude Code、Codex 或 shell 直接放在宿主机上运行，而是给 agent 一个隔离虚拟机、受控网络和可销毁环境。

## 用法

典型方式是在项目目录执行 `clawk`，让 agent 在 VM 中工作，代码以挂载方式进入 guest。项目支持 `clawk attach` 恢复会话，必要时可销毁 VM 后重新创建。

## 原理

clawk 的边界来自 VM，而不是 prompt 规则。README 描述其网络采用 allow-list，宿主密钥不进入 VM，但可通过 ssh-agent forwarding 支持必要的 Git 操作。它把 package install、测试运行、服务启动和潜在破坏性命令放到 disposable guest 内执行。

## 价值

- 击中 coding agent 的核心安全痛点：真实自动化需要执行命令，但宿主机权限太大。
- 比单纯命令审批更适合长任务，因为 agent 可以在 VM 内自由试错。
- 对多仓库、多 worktree 和长期 agent session 有工程价值。
- 与 Docker/devcontainer 不同，它强调完整虚拟机边界和 disposable lifecycle。

## 风险边界

- 项目仍处 pre-1.0，README 明确提示 breaking changes 和 rough edge。
- allow-list 只限制未知网络；若允许 GitHub 等外部服务，agent 仍可能把可读内容发布出去。
- ssh-agent forwarding 便利但也需要最小化授权和审计。
- VM 不是完整供应链防护，恶意依赖、日志泄露和 prompt injection 仍需单独治理。

## 补充建议

- 用于有写权限 agent 前，先做一组恶意命令、外连、secret 读取和 git push 演练。
- 对不同项目维护最小网络 allow-list，不要把 sandbox 变成默认全网环境。
- 与 `mindwalk`、`coder_eval` 这类可观测/评测工具组合使用，形成执行、复盘、验收闭环。

## 参考资料

- GitHub: <https://github.com/clawkwork/clawk>
