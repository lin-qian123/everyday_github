<!-- markdownlint-disable MD013 -->

# nightshift

## 定位

Nightshift 是 Claude Code、Codex 和 Cursor 的长任务插件，用磁盘上的任务清单、hook、恢复进程和逐项收据维持执行连续性。它不提供模型，也不替代宿主的权限系统；适合把一批可验证工作交给现有编码 Agent，并在结束后审阅结果。

- 上游：[orwa-mahmoud/nightshift](https://github.com/orwa-mahmoud/nightshift)，仓库 ID `1300273081`。
- 2026-11-21（Asia/Shanghai）07 时段：官方 Shell daily **+35**；API stars / forks / open issues（含 PR）为 **566 / 24 / 5**。[API](https://api.github.com/repos/orwa-mahmoud/nightshift)
- 最新核到非预发行版 [v0.37.2](https://github.com/orwa-mahmoud/nightshift/releases/tag/v0.37.2)，UTC 11-19 19:16，北京时间 11-20 03:16；Codex manifest 同为 `0.37.2`。本页 main 固定快照 `8b596c9a3f80baf53ee339b9408a103b549b9e1c`，不等同 release tag。
- 分类：`Coding Agents 与终端助手`。本仓库首次建档，不表示今天首发；本轮仅核文档、配置与文件清单，未安装插件或运行 shift。

## 用法

上游 Codex 安装示例（本轮未执行）：

```text
codex plugin marketplace add orwa-mahmoud/nightshift
codex plugin add nightshift@nightshift
```

随后在宿主检查并信任 hooks；进入一个持久项目，依次使用 `/nightshift:setup`、`/nightshift:plan` 和 `/nightshift:start`。`/nightshift:status` 看进展，`/nightshift:stop` 暂停，`/nightshift:doctor` 只诊断。Claude Code 和 Cursor 的安装入口见[固定安装文档](https://github.com/orwa-mahmoud/nightshift/blob/8b596c9a3f80baf53ee339b9408a103b549b9e1c/docs/install.md)。这些命令是上游接口记录，使用时还需核对已安装宿主版本。

macOS / Linux 需要 Bash 3.2+ 与 POSIX 工具；原生 Windows 使用 PowerShell 5.1+。POSIX 的部分 JSON 处理依赖可用的 `jq` 或 Python 解析路径，不能把基础规则仍生效扩写成所有策略、渲染能力一致。ChatGPT 目录的 skills-only 版本没有生命周期 hooks，因此没有完整版本的 clock-out gate、恢复和 usage accounting。

建议先在可恢复的小项目中安排两项任务，明确每项 `Verify:` 和 `Evidence:`。文档验收可指定渲染与链接检查；UI 验收可指定屏幕宽度和截图；不要只写“做完”。

## 原理

1. **持久合同。** punch list 及其 `## Items` 复选框定义当班任务，收据、决策和日志保存在 `.nightshift/`。Start 通过预检、armed marker、会话绑定和进程 lease 激活任务；单独写一份清单不会自动启动 hooks。
2. **停止门控。** 绑定的 Agent 在还有任务时尝试停止，会收到当前合同；规则可拦截指定命令、工具、提交身份和敏感内容。其他会话不会自动继承同样的会话门控，因此不能视为整机访问控制。
3. **恢复。** 独立 watchman 依据宿主记录恢复中断会话，必要时退到新会话并读取磁盘进度。它涉及真正的宿主进程启动，不只是追加提示词。
4. **分层验收。** `Verify:` 定义要通过的检查，`Evidence:` 定义供人打开的产物。文件存在检查只能证明文件存在，不能证明截图正确或性能真的改善。

上述机制来自[运行说明](https://github.com/orwa-mahmoud/nightshift/blob/8b596c9a3f80baf53ee339b9408a103b549b9e1c/docs/how-it-works.md)与[证据文档](https://github.com/orwa-mahmoud/nightshift/blob/8b596c9a3f80baf53ee339b9408a103b549b9e1c/docs/evidence.md)；本轮未逐条验证 hook 实现或恢复竞争条件。

## 价值

- 把“聊天中说做过”变成任务、检查、提交 / 产物和待审决策之间的可追踪关系，便于跨会话接续。
- 对有限 backlog、文档漂移、测试维护等工作，可以减少人工反复提醒；对开放目标可配置截止时间与单项预算。
- 上游披露跨宿主接续与自用案例，但案例不构成控制实验，也不能推出普遍提效比例或无人值守成功率。[固定 README](https://github.com/orwa-mahmoud/nightshift/blob/8b596c9a3f80baf53ee339b9408a103b549b9e1c/README.md)

## 风险边界

- **默认值需实际检查。** [规则模板](https://github.com/orwa-mahmoud/nightshift/blob/8b596c9a3f80baf53ee339b9408a103b549b9e1c/plugins/nightshift/skills/nightshift/references/nightshift-rules-template.json)中 `isolation=none`、`toolingPolicy=auto-add`、`verificationProfile=fast`；五类 elevation 均为 allow，命令 / 路径 / 密钥模式保护字段为空。fast 仍有逐项检查和收据，但不运行整班 Gates；这些默认值不能解释成自动限制系统操作或严格验收。
- **证据默认不强制。** 模板的 `receipts.evidence.check=off`、`review=off`；即使启用 block，也只对命名文件是否存在作机械检查。需要把内容、交互与数值验收写进任务并实际审阅。
- **有限任务也可能久等。** 模板 `stallMax=0`，有限任务在没有截止时间、单项预算或重试上限时可能持续被门控；恢复与续跑仍消耗宿主模型额度。
- **加固不是 sandbox。** 上游明确：shift 能做宿主允许的事，guards 只加固配置的边界。worktree 是可选隔离工作副本，不是 OS / 网络沙箱；默认就在目标 checkout 工作。
- **数据出口分层。** 上游声明插件自身无 telemetry、无需额外 API key；宿主 Agent 的模型、网络和数据政策仍适用。可选 `notifyCommand` 是不受限制的本地 shell，可访问网络。[安全政策](https://github.com/orwa-mahmoud/nightshift/blob/8b596c9a3f80baf53ee339b9408a103b549b9e1c/SECURITY.md)
- **许可与版本。** 根代码为 MIT；模型服务、宿主订阅和导入工具另有条款。v0.37.2 修复 Start 保存策略和无法解码 hook payload 的拒绝原因，不能把 release 修复说明当作已覆盖所有 bypass 的验证。

## 补充建议

先设置符合本项目的禁止命令、受保护目录、身份和敏感模式，再选验证 profile、工具添加策略、预算与隔离方式。用可丢弃仓库演练“未完成就停止”“证据文件缺失”“宿主崩溃恢复”和“人工停工”，核对日志与真实提交。上线到重要项目之前，分别评估插件策略、宿主授权和 OS 权限。

本轮没有建立 schedule、授权 hooks、创建 worktree、启动 Agent、访问用户凭据或执行通知；接续重点是这些边界在目标宿主上的实际行为。

## 参考资料

- [固定 README](https://github.com/orwa-mahmoud/nightshift/blob/8b596c9a3f80baf53ee339b9408a103b549b9e1c/README.md)、[安装](https://github.com/orwa-mahmoud/nightshift/blob/8b596c9a3f80baf53ee339b9408a103b549b9e1c/docs/install.md)、[运行机制](https://github.com/orwa-mahmoud/nightshift/blob/8b596c9a3f80baf53ee339b9408a103b549b9e1c/docs/how-it-works.md)。
- [规则模板](https://github.com/orwa-mahmoud/nightshift/blob/8b596c9a3f80baf53ee339b9408a103b549b9e1c/plugins/nightshift/skills/nightshift/references/nightshift-rules-template.json)、[配置与默认值](https://github.com/orwa-mahmoud/nightshift/blob/8b596c9a3f80baf53ee339b9408a103b549b9e1c/docs/knobs.md)、[证据](https://github.com/orwa-mahmoud/nightshift/blob/8b596c9a3f80baf53ee339b9408a103b549b9e1c/docs/evidence.md)。
- [Codex manifest](https://github.com/orwa-mahmoud/nightshift/blob/8b596c9a3f80baf53ee339b9408a103b549b9e1c/plugins/nightshift/.codex-plugin/plugin.json)、[安全政策](https://github.com/orwa-mahmoud/nightshift/blob/8b596c9a3f80baf53ee339b9408a103b549b9e1c/SECURITY.md)、[MIT](https://github.com/orwa-mahmoud/nightshift/blob/8b596c9a3f80baf53ee339b9408a103b549b9e1c/LICENSE)。
