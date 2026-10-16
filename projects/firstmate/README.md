<!-- markdownlint-disable MD013 -->

# Firstmate（kunchenguid/firstmate）中文解读

> 上游仓库：<https://github.com/kunchenguid/firstmate> · 归类：Agent 框架与技能生态 · 证据快照：2026-10-17（Asia/Shanghai）。API：8,003 stars / 2,576 forks / 2,474 open issues；无 GitHub Release / tag；按 commit 固定此指令与脚本发行目录；MIT。本页为上游资料与相关代码的静态整理，未安装运行、复测性能或完成全面安全审计。

## 定位

Firstmate 将一般终端 coding agent 变为任务主管：用户对接 first mate，worker 在可见 session backend 和独立工作目录完成修改或调查。上游称其为 agent distro，主要由指令、技能、脚本与状态约定组成；clone 后从支持的 harness 启动，行为与宿主能力紧密相关。

## 用法

准备 macOS / Linux、Git、已认证的 GitHub CLI 和所选 session backend。把固定 commit 的 Firstmate 克隆到专用目录，先审阅其 AGENTS、hooks、脚本及外部 PR / merge 权限，再从该目录启动支持的 harness。tmux 是参考默认，Herdr 等另有配置，Zellij / cmux / Orca 标注实验。首次只分派一个测试仓库的 scout 调查，核对报告与 worker 退出，随后再验证写入任务。

## 原理

- 指令层把请求路由到 ship / scout 任务，借助 worktree、brief、状态文件和事件 watcher 跟踪 worker。
- 可选 secondmate 运行在独立 home；远程模式把整个 persistent home 放到 SSH 可达主机，远端还需自己的 runtime、仓库与凭据。
- `/afk`、`/quiet`、`/bearings`、`/stow` 等处理监督、摘要与知识维护，Calm 仅改变 transcript 展示；可选 Relay 连接公开提及等外部入口。

## 价值

它可减少人在多个终端间搬运上下文的工作，同时保留可见 worker 和交付记录。适合已有 CLI agent / Git 工作流的操作者，尤其需要分开“修代码”和“只调查”的场景；本次没有验证 unattended 完成率或并发收益。

## 风险边界

- clean worktree / 独立 home 分离任务文件，不自动隔离同用户进程、网络或 GitHub 凭据；PR、merge、远端执行须另设授权。
- hook、常驻监督、SSH 远端 job worker 与可选 Relay 扩大信任边界。远程文档明确不是任意单 worker 远程放置，也没有自动本地 failover。
- Calm 默认关闭；启用后隐藏的 operational inputs 仍在模型上下文、session 存储与 export / share 中，不能作为数据删除或权限控制。
- `codex-app` 当前仍是 blocked backend，不能因为 Codex Desktop 有 host tools 就宣称可从 Firstmate 子进程受支持地创建 / 监督桌面 chats；Codex CLI 与 App 后端须分开。

## 补充建议

先以单 worker 验任务状态、停止、清理和只读报告，再做双任务同仓库冲突演练。保持 external send / merge 明确授权，远程用专用账号与 host-key 核验，检查日志 / transcript 留存；不要把安静界面或 watcher 唤醒当成任务已成功。

## 参考资料

- 上游仓库：<https://github.com/kunchenguid/firstmate>
- GitHub REST API：<https://api.github.com/repos/kunchenguid/firstmate>
- README / 发行方式：<https://github.com/kunchenguid/firstmate/blob/main/README.md>
- 配置与后端：<https://github.com/kunchenguid/firstmate/blob/main/docs/configuration.md>
- Calm 展示与数据保留：<https://github.com/kunchenguid/firstmate/blob/main/docs/calm.md>
- Codex App 当前阻塞边界：<https://github.com/kunchenguid/firstmate/blob/main/docs/codex-app-backend.md>
- 远程 secondmate：<https://github.com/kunchenguid/firstmate/blob/main/docs/remote-secondmates.md>
- 许可：<https://github.com/kunchenguid/firstmate/blob/main/LICENSE>
- Releases：<https://github.com/kunchenguid/firstmate/releases>
