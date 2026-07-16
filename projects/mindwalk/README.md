<!-- markdownlint-disable MD013 -->

# mindwalk

## 定位

`cosmtrek/mindwalk` 是一个本地优先的 coding-agent session 可视化工具，用 3D/地图视图回放 Claude Code 与 Codex session log 在代码库中的搜索、阅读、编辑和验证轨迹。

## 用法

README 提供一键安装脚本。默认运行 `mindwalk` 会扫描 `~/.claude/projects` 和 `~/.codex/sessions`，启动本地 Web UI；也可以用 `mindwalk open <session.jsonl>` 打开单个会话，或用 `mindwalk analyze` 调用本机 agent CLI 对会话进行评估。

## 原理

项目把仓库渲染成树状或 terrain map，再把 session log 标准化为时间线：搜索、读取、执行、编辑、压缩和用户回合等事件都会映射成可播放轨迹。查看本身不上传数据；只有显式运行评估时，才会通过用户自己的 Claude 或 Codex CLI 发送会话摘要。

## 价值

- 解决“agent 到底看了哪些文件、在哪些地方绕路、编辑是否过界”的可观测性问题。
- 对 code review、事故复盘和 agent 工作流调参有实际价值。
- 本地日志读取降低了引入 SaaS 监控的门槛。
- 把 agent 行为从 JSONL 变成图形轨迹，有利于快速发现无关探索、重复编辑和验证缺口。

## 风险边界

- 可视化能帮助复盘，但不能替代测试、人工审查和安全边界。
- session log 可能包含路径、任务描述和敏感片段，分享截图或评估摘要前要脱敏。
- 评估功能会调用外部模型账户，应确认发送范围。
- 对不同 agent 日志格式的兼容性可能随宿主工具更新而变化。

## 补充建议

- 把它用于失败会话复盘，重点看“最后一次验证后又编辑了哪些文件”。
- 团队内部可建立 session 复盘模板：范围、触达文件、错误率、验证点、人工结论。
- 关注后续是否支持更多 harness、隐私过滤和 CI artifact 输出。

## 参考资料

- GitHub: <https://github.com/cosmtrek/mindwalk>
