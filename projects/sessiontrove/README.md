<!-- markdownlint-disable MD013 -->

# sessiontrove

> 上游仓库：[maedmatt/sessiontrove](https://github.com/maedmatt/sessiontrove) · 归类：记忆层与个人 AI 基础设施 · 本页基于 2026-08-25 的上游 README、仓库目录与 GitHub API 快照整理。

## 定位

`sessiontrove` 是一个本地 coding-agent 会话归档工具：它把 Claude Code、Codex、Oh My Pi、OpenClaw 和 Pi 的本地会话/历史文件按机器名复制到私有目录，尽量保留原始格式；源文件后来消失时，归档副本不会被它主动删除。上游明确说明它不上传、不解析，也不标准化对话，当前目标是保存用户自己的训练或复盘源材料。

API 快照：4 stars、1 fork、1 个开放 issue；创建于 2026-08-24；MIT。它只构成早期公开开发者信号，不代表所有 agent 版本均兼容，也不证明归档完整性、安全性、训练适用性或 GitHub Trending 热度。

## 用法

要求 Python 3.11+。先把目标归档目录放在加密卷或受访问控制的位置，确认目的地不是 Git 工作树或同步共享盘，再运行：

```sh
git clone https://github.com/maedmatt/sessiontrove.git
cd sessiontrove
uv run sessiontrove /absolute/path/to/agent-sessions --machine workstation-a

# 或安装为命令行工具
uv tool install .
sessiontrove /absolute/path/to/agent-sessions --machine workstation-a
```

上游建议对同一台机器持续使用相同 `--machine` 名称。开发验证可运行 `uv run ruff check .`、`uv run ruff format --check .` 与 `uv run pytest`。首次真实归档前，应以虚构会话或可丢弃 profile 核对发现范围、增量更新、权限（目录 `0700`、文件 `0600`）和恢复路径。

## 原理

- 工具读取各 agent 的本地状态根目录：例如 Codex 的 `~/.codex/sessions`、`archived_sessions` 与 `history.jsonl`，Claude Code 的项目 transcript 与历史文件；不可用的 agent 会被跳过。
- 它按机器名创建稳定顶级目录，并拷贝原始会话格式及部分关联 blob；临时和锁文件被排除，变化文件更新副本。
- 设计上是归档复制而非索引或语义处理，因此不会自动做脱敏、去重、嵌入、摘要、加密或数据质量检查。
- 上游同时提示 Claude Code 的保留期与 Codex 的 history 配置会影响源数据可否及时备份；归档能保住已读到的数据，不能找回已被上游清理的内容。

## 价值

- 多个 coding agent 的会话散落在不同路径时，可提供一份按机器组织的私有原始档案，利于调试、复盘与迁移前备份。
- 保持原格式和不删除旧副本的策略，适合建立可追溯的数据留存层，并把解析/训练等高风险步骤推迟到另行审查后。
- 对长期项目，归档能帮助把 prompt、工具输出和工作轨迹与代码版本、测试结果建立后续关联，而非只保留最终提交。

## 风险边界

- 会话可能含提示词、代码、终端输出、本地路径、访问令牌、个人数据和第三方材料；`0700`/`0600` 不是加密、密钥轮换、删除治理或跨主机访问控制的替代品。
- “从不删除归档文件”会放大过期敏感信息的留存风险；法规、公司政策或用户删除请求可能要求独立的保留期、加密销毁和审计机制。
- 归档完整性受 agent 版本、配置、平台路径、权限、源文件保留期与关联媒体解析限制；未发现或跳过某 agent 不等于其数据安全或已经备份。
- 归档对话不等于拥有训练、共享或再利用其中内容的权利；混入第三方代码、客户资料或模型输出前必须先完成权利、同意和脱敏审查。

## 补充建议

1. 先对每种 agent 做一次可控样本的“源文件数 / 归档文件数 / 哈希 / 恢复读取”清单，记录未覆盖路径和版本。
2. 在归档后立即做密钥扫描、PII 检测与人工抽样；将原始档案、脱敏副本和任何训练集物理隔离，并采用最小访问权限。
3. 为归档目录设置加密、离线或受控备份、保留期限和可验证的删除流程；不要用普通云同步目录替代这些控制。
4. 训练或共享前按来源建立权利台账，并将会话按用户、项目、敏感等级和许可状态分区；先用合成数据验证后续流水线。

## 参考资料

- [上游 README / 支持范围、命令与保留说明](https://github.com/maedmatt/sessiontrove)
- [GitHub API 元数据](https://api.github.com/repos/maedmatt/sessiontrove)
- [MIT License](https://github.com/maedmatt/sessiontrove/blob/main/LICENSE)
- [Claude Code settings reference](https://code.claude.com/docs/en/settings-reference#cleanupperioddays)
- [Codex configuration reference](https://developers.openai.com/codex/config-reference)
