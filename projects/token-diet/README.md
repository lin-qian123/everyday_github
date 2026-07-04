# token-diet

- GitHub：<https://github.com/Kulaxyz/token-diet>
- 抓取时间：2026-07-05（Asia/Shanghai）
- 今日信号：GitHub API 显示该仓库创建于 2026-07-03，抓取时约
  `447 stars / 0 forks`，README 声称可为 Claude Code、Codex、Cursor、
  Windsurf、Cline 等 coding agent 降低 token 成本。

## 定位

`token-diet` 是一个面向 coding agent 的“常驻型 token 效率 skill”。
它不是模型压缩工具，而是把简洁输出、少读文件、少做无用工具调用、
聚焦关键测试、减少解释性废话等行为规则写成 agent 可加载的操作约束。

项目 README 声称在真实 Sonnet 5 运行中可获得约 31% 平均账单下降，
但这些数字来自项目方说明，仍需要第三方复测。

## 用法

README 给出的安装方式是：

```bash
INSTALL_URL=https://raw.githubusercontent.com/Kulaxyz/token-diet/main/install.sh
curl -fsSL "$INSTALL_URL" | bash
```

也可以传入参数选择强度或目标 agent：

```bash
INSTALL_URL=https://raw.githubusercontent.com/Kulaxyz/token-diet/main/install.sh
curl -fsSL "$INSTALL_URL" | bash -s -- --ultra
```

支持 `on`、`lite`、`ultra`、`off` 等级，并可针对 Claude Code、Codex、
Cursor、Windsurf、Cline 或当前项目安装。

## 原理

它把 token 节省拆到 agent 行为层：

- 回复先给结论，去掉寒暄和尾声。
- 文档、计划、handoff 和注释只保留必要信息。
- 读文件前先搜索，避免整文件读取和重复读取。
- 工具调用尽量批处理，拿到足够证据后及时停止。
- 测试覆盖关键路径和高风险边界，避免为了数量堆测试。
- 对正确性、关键测试、代码和错误信息保留完整度，不把节省 token 变成偷工减料。

## 价值

- 对高频 coding agent 用户：可降低长会话输出和工具使用成本。
- 对团队：提供一个讨论“agent 该如何少浪费上下文”的规则样本。
- 对 agent 生态：说明可靠性之外，成本工程也在逐步 skill 化、规则化。

## 风险边界

- 项目当前未显示明确许可证，生产或团队分发前需要确认使用权。
- 节省比例来自项目 README，不能直接视为通用结论。
- 过度压缩沟通可能损害可审计性，尤其是安全、支付、数据迁移等高风险任务。
- install script 会修改本地 agent 配置，运行前应审查脚本内容并备份配置。

## 补充建议

- 与 `fable-soul`、`self-learning-skills`、`loop-engineering` 对照观察：
  它们分别关注判断力、经验沉淀、loop 设计和成本控制。
- 团队使用时建议分级启用：普通问答可更激进，代码修改和事故排查保留足够上下文。
- 后续关注是否出现公开 benchmark、配置差异说明和许可证补充。

## 参考资料

- GitHub 仓库：<https://github.com/Kulaxyz/token-diet>
- README：<https://github.com/Kulaxyz/token-diet#readme>
