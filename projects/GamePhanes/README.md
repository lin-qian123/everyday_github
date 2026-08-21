<!-- markdownlint-disable MD013 -->

# GamePhanes

> 上游仓库：[GamePhanes/GamePhanes](https://github.com/GamePhanes/GamePhanes) · 归类：Agent 框架与技能生态 · 本页基于 2026-08-22 的上游 README 与 GitHub API 快照整理。

## 定位

`GamePhanes` 是面向 Godot 的开源游戏 coding-agent 环境与基准：它把“理解—规划—构建—运行—试玩—观测—修复—评测”组织成一个可验证循环。当前 v0.1 包含 Godot 环境探测、JSON 任务契约、临时工程副本、外置 playtest harness、headless 运行、NDJSON 事件日志和确定性断言，不依赖 LLM judge。

API 快照：约 85 stars、1 fork、0 个开放 issue；创建于 2026-08-21；许可证 MIT。它是早期开发者信号，README 所称 `28/28` showcase 断言来自项目方材料，尚未由本仓库独立复现。

## 用法

上游要求 Node.js 22+ 与 Godot 4.x，推荐使用可输出完整日志的 console build。先在无敏感的示例工程执行验证：

```sh
npm test
node ./bin/gamephanes.js validate ./benchmark/tasks/platformer-basic.json
node ./bin/gamephanes.js doctor --godot /path/to/godot
node ./bin/gamephanes.js run ./benchmark/tasks/platformer-basic.json \
  --godot /path/to/godot \
  --report ./reports/platformer-basic.json
```

任务文件定义候选工程、需求、外部 harness 和断言；上游的 `Starfall Protocol` 示例可用 `node ./bin/gamephanes.js run ./benchmark/tasks/starfall-protocol.json --godot /path/to/godot` 执行。先检查报告、事件日志、截图和退出状态，再考虑让 agent 接触自有游戏项目。

## 原理

- runner 将候选 Godot 项目复制到临时目录，注入由 benchmark 管理的 harness，再执行导入、运行与 playtest；这避免直接污染源工程，但不是系统级沙箱。
- 运行时将事件写成 NDJSON，规则评估器据此检查移动、交互、状态或任务完成等明确条件，并产生可复查的分数和报告。
- 任务 contract 把“做什么、如何观测、怎样判定通过”从模型提示词中拆出，使修复循环能够依赖外部断言而非模型自评。

## 价值

- 为游戏 agent 引入能重复运行的工程反馈，优于只凭截图、自然语言总结或 LLM judge 判断是否完成。
- Godot 项目、资产 manifest、任务和运行报告可版本化，有利于定位回归、复现失败与比较 agent 策略。
- 外置 harness 的设计能降低被测项目自报成功的空间，适合构建小规模、可审阅的游戏代码任务集。

## 风险边界

- 临时副本与超时限制不构成 OS 级隔离；Godot 子进程仍继承用户权限和网络访问。运行不受信任项目应放入容器或权限隔离 worker。
- 通过一组确定性断言只说明覆盖到的行为成立，不保证玩法质量、帧率、跨平台兼容性、可访问性、作弊防护或复杂场景稳定性。
- 游戏资产、参考代码、商标和试玩数据各有版权与许可约束；不要把不明来源资产或玩家数据混入 benchmark。
- 新项目的 API 元数据和 README 对真实 agent loop、CI 支持、资源消耗与失败模式的覆盖有限，生产采用前须独立验收。

## 补充建议

1. 在隔离环境先跑官方示例，保存 Node/Godot 版本、平台、任务 JSON、完整日志和报告，以核验断言是否可重放。
2. 为自有项目加入启动失败、空存档、低帧率、断网、错误输入与资源泄漏等负例；不要用单一“通关”断言替代质量门槛。
3. 将 agent 的写入范围限定为临时 checkout，只有测试、静态检查和人工审阅均通过才合并到正式游戏工程。
4. 用独立设备和不同 Godot 版本复测，报告覆盖率、误判率、执行时间与网络/文件权限，而非只汇报通过数。

## 参考资料

- [上游 README / Quick Start](https://github.com/GamePhanes/GamePhanes)
- [GitHub API 元数据](https://api.github.com/repos/GamePhanes/GamePhanes)
- [架构说明](https://github.com/GamePhanes/GamePhanes/blob/main/docs/architecture.md)
- [Godot 命令行文档](https://docs.godotengine.org/en/stable/tutorials/editor/command_line_tutorial.html)
