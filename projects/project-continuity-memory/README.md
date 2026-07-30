# Project Continuity Memory

## 定位

`Project Continuity Memory` 是本地优先、仓库内的 agent 交接协议。它以 `PROJECT_MEMORY.md` 保存稳定知识、以 `HANDOFF.md` 记录当前目标、已核验证据、阻塞与精确下一步，并配有 Agent Skill 和轻量验证器。

截至 2026-07-31，GitHub API 快照显示该仓库创建于 2026-07-30，约 2 stars、0 forks，Apache-2.0 许可证；仍属极早期信号，不能据此推断长期维护或跨框架兼容性。

## 用法

先阅读仓库的 skill 与模板，在一个持续迭代的项目中创建两份文件；每次恢复工作前以源码、测试和外部状态为准核验，再更新 handoff，而不是把聊天记录原样拷入。

```bash
git clone https://github.com/YSjandj-design/project-continuity-memory.git
cd project-continuity-memory
# 按仓库文档安装 skill，并将模板复制到目标项目
```

建议先让 validator 在 CI 中只报告格式问题，确认团队字段契约稳定后再设为合并门槛。

## 原理

项目把耐久知识与易变状态分离：前者承载仍然有效的边界、决定和背景；后者承载当前任务事实、证据、阻塞和下一步。它主张“当前项目事实优先于旧记忆”，因此 memory 是恢复入口而非事实源。

## 价值

- 用小而可审阅的 Markdown 缩短跨窗口、跨人或上下文压缩后的冷启动。
- 让下一步、验证证据和不确定性进入 Git 历史，补足纯聊天记忆和任务看板的空白。

## 风险边界

- 两份文件会过期，也可能泄露路径、客户信息或密钥线索；绝不能替代源码、测试、ADR 或权限控制。
- “已验证”字段只代表记录者当时的证据，恢复时仍要重查时间敏感的外部状态。
- 过度格式化可能成为维护负担；一次性任务和已有等价交接机制的仓库未必需要引入它。

## 补充建议

把可复核命令、文件路径、时间和结果写进 handoff，避免泛泛的“已完成”。设置最小字段、定期删去失效状态，并在提交前扫描敏感信息；将 memory 与项目的 README、TODO 和测试输出链接起来。

## 参考资料

- GitHub：<https://github.com/YSjandj-design/project-continuity-memory>
- GitHub API 快照：<https://api.github.com/repos/YSjandj-design/project-continuity-memory>
- Agent Skills 规范：<https://agentskills.io>
