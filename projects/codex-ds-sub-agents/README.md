# codex-ds-sub-agents

## 定位

`codex-ds-sub-agents` 是第三方 macOS 集成方案，让 Codex Desktop 以 DeepSeek 模型作为子 agent，并以工作区文件传递待办、领取记录与回执。截至 2026-08-02 的 GitHub API 快照：项目创建于 2026-08-01，约 6 stars、2 forks；API 未返回 SPDX 许可证字段。

## 用法

先在隔离测试环境运行 `python3 scripts/doctor.py`，确认 Codex 版本、Python、Keychain 条目与配置语法；再按 README 用 `python3 scripts/install.py` 安装。安装会写入 `~/.codex/agents/`、`~/.codex/models/`、`~/.codex/skills/`，并可能向 `~/.codex/config.toml` 追加 provider，因此必须先备份并审阅 diff。API Key 应由本机 Keychain 交互输入，不能粘贴到对话、任务文件或仓库。

## 原理

父 agent 将独立任务写入 `.deepseek-delegations/pending/`，worker 以原子 rename 领取到 `claimed/`，完成后回传 `task_id`、`claim_id` 与 receipt。该设计绕开该项目所述的自定义 provider 子 agent 任务正文传递问题，但不改变模型能力、计费或平台兼容性。

## 价值

- 把并行子任务的分配、领取和回执落为可检查的本地文件状态。
- 为 Codex 与外部模型的可替换 worker 组合提供实验入口。

## 风险边界

- 非 OpenAI/DeepSeek 官方插件；README 仅声称在特定 Codex 版本和 macOS 环境验证。
- 会修改用户级 Codex 配置且把任务内容发给第三方模型；需评估密钥、代码与数据外传。
- 原子领取不自动判断 worker 是否已停止，`recover` 前仍要人工确认，避免重复执行。

## 补充建议

先用无敏感、只读任务和独立配置目录验证一次；记录 provider 请求、费用和失败回执。生产代码、客户数据或高权限命令不应因并行便利而越过人工批准。

## 参考资料

- GitHub：<https://github.com/wongchisum/codex-ds-sub-agents>
- 架构说明：<https://github.com/wongchisum/codex-ds-sub-agents/blob/main/ARCHITECTURE.md>
- GitHub API 快照：<https://api.github.com/repos/wongchisum/codex-ds-sub-agents>
