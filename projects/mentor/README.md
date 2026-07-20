<!-- markdownlint-disable MD013 -->

# mentor

## 定位

`mentor` 是一个面向 Claude Code、Codex 和其他支持 `SKILL.md` 的 coding agent 的会话洞察 skill。它读取本地 agent 使用历史，生成一份自包含 HTML 报告，分析用户实际如何与 agent 协作、哪里浪费时间、哪些习惯和规则可以改进。

## 用法

```bash
npx skills add smixs/mentor
```

安装后可通过 `/mentor`、`/mentor claude`、`/mentor codex` 或 `/mentor both` 运行，默认分析最近 30 天，也可以用 `--days N` 指定时间窗口。报告写入本地 HTML 文件，可直接在浏览器打开。

## 原理

skill 读取 `~/.claude` 下的 Claude Code transcript 和 `~/.codex` 下的 Codex rollout，统计消息、会话、工具调用、编辑、文件、token、每日活动、工具比例和语言分布，并聚类用户工作主题。报告重点不是漂亮图表，而是把重复摩擦点转成可执行修复建议、规则补丁或更合适的工作流。

## 价值

- 把 agent 使用本身纳入复盘，补上“人如何给 agent 设定任务”的反馈循环。
- 对频繁使用 Codex / Claude Code 的个人开发者有高实用性。
- 可帮助团队识别规则缺失、重复中断、验证不足和上下文管理问题。

## 风险边界

- 工具会读取本地会话历史，里面可能包含代码、路径、凭据片段或私人信息。
- 报告建议依赖启发式聚类，不应无审查地写入团队规则。
- 需要 `uv` 等本地运行条件，跨平台兼容性需实测。
- 如果历史数据本身不完整，统计结果可能偏差较大。

## 补充建议

- 适合按周运行，把报告中反复出现的问题沉淀到项目 `AGENTS.md` 或个人 skill 中。
- 对敏感仓库，生成报告前应确认输出路径和 HTML 内容不会同步到公共云盘。
- 可与 `mindwalk`、`agentsview`、`deja-vu` 这类 agent 复盘/记忆工具比较使用。

## 参考资料

- GitHub：<https://github.com/smixs/mentor>
- skills.sh：<https://skills.sh>
- Codex 本地历史目录说明：<https://github.com/smixs/mentor#readme>
