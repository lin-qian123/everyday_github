# lemma-platform

## 1. 定位

`lemma-platform` 是 Lemma 的开源工作区平台，目标是让人类和 AI agents 在同一个
结构化 workspace 中协作。它不把工作停留在聊天滚动记录里，而是把 agent 产出
落到表格、任务、审批、文件、工作流和外部沟通入口中。

它的定位接近“agent-native operations workspace”：既可以本地运行，也可以接入
lemma.work 云端；既能被 Claude Code、Codex、OpenCode、Cursor 等 coding agent
通过 skill 操作，也能作为团队流程系统运行。

## 2. 基本用法

README 给出的轻量入口是先安装 CLI：

```bash
uv tool install lemma-terminal
lemma skills install
lemma auth login
lemma pod create my-team --with-starter
lemma chat "what can you do in this pod?"
```

若要让本地 coding agent 接受 pod 分配的任务，可以启动 daemon：

```bash
lemma daemon start
lemma daemon status
lemma daemon stop
```

从源码本地运行则使用安装脚本启动完整 stack，并将本地服务暴露在
`127-0-0-1.sslip.io` 相关地址。

## 3. 核心原理

Lemma 的基本单位是 `pod`。一个 pod 包含表格、文件、agents、workflows、
functions、permissions、approvals、apps 和沟通 surfaces。人类与 agent 读写同一套
状态，而不是各自保存孤立上下文。

它的关键设计点包括：

- 用表格和文件承载长期业务状态。
- 用 agents 和 workflows 表达自动化角色与流程。
- 用 permissions 和 approvals 限制 agent 可以看什么、做什么、何时暂停。
- 用 Slack、Teams、Gmail、Outlook、Telegram、WhatsApp 等 surfaces 接入团队入口。
- 用 CLI / SDK / skills 让 coding agent 能构建和操作 pod。

## 4. 工程价值

Lemma 代表了从“聊天机器人”向“协作系统”迁移的趋势。对团队来说，真正重要的不是
agent 回复了什么，而是它是否把结果写回任务表、是否等待正确审批、是否留下可追溯
状态。

对开发者来说，pod-as-files 的思路也很有价值：如果一个工作流可以导出、编辑、
导入，就更容易用 coding agent 生成、测试和版本化。

## 5. 风险边界

Lemma 涉及业务数据、表格、消息平台和审批流，权限模型必须比普通聊天工具更谨慎。
错误配置的 agent 可能读取过多记录、触发错误 workflow，或在外部沟通入口发送未经
批准的内容。

AGPLv3 core 与 Apache-2.0 SDKs 的组合也需要在商业内嵌场景中确认许可证边界。

## 6. 补充建议

- 先用单人 pod 或非生产流程试验，确认 permissions、approvals 和日志模型。
- 对接 Slack / Gmail / WhatsApp 等外部入口前，先建立测试账号和测试 channel。
- 把 pod 文件纳入版本控制，便于审查 agent 生成的 workflow 变更。
- 与 `open-tag`、`background-agents`、`ai-maestro` 比较，观察团队级 agent
  控制面是否走向结构化状态系统。

## 7. 参考资料

- GitHub 仓库：<https://github.com/lemma-work/lemma-platform>
- 官网：<https://lemma.work>
- 许可证：AGPL-3.0 core，Apache-2.0 SDKs
