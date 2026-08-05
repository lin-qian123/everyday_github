# portable-agent-skills

- 仓库：[ch1109/portable-agent-skills](https://github.com/ch1109/portable-agent-skills)
- 快照：2026-08-06 抓取；GitHub API 显示其创建于 2026-08-05，约 11 stars、0 forks，MIT。数字会随时间变化。
- 分类：Agent 框架与技能生态

## 定位

一组强调跨宿主可移植性的 Agent Skills，覆盖带来源的主题研究、仓库部署前的显式执行闸门，以及安装前的静态安全检查。

## 用法

可用 `npx skills add ch1109/portable-agent-skills --skill <name>` 安装单个 skill，或按 Hermes/Codex 的各自插件流程安装。调用时按 skill 名提供具体任务，例如 `topic-research` 做决策简报、`github-project-deployer` 先检查后部署、`skill-safety-checker` 扫描陌生技能；仓库还提供 `python3 -m unittest -v tests/test_repository.py` 校验自身布局。

## 原理

将核心说明保持为标准 `SKILL.md`，把宿主差异、长清单与脚本放入按需加载文件；工作流先探测本机能力与权限，再区分事实、来源主张、推断与未知，并在执行或“安全”结论之前要求可见证据。

## 价值

适合作为不同 agent host 之间迁移工作方式的参考：减少对固定工具名、路径和网络权限的隐式依赖，同时把高影响操作前的人工决策点写进流程。

## 风险边界

可发现、可加载不等于任何宿主上都可安全运行；静态扫描只产生候选发现，不能证明运行时无风险。部署 skill 的计划也不能替代源码审计、许可证检查、凭据隔离和生产变更审批。

## 补充建议

安装前在沙箱中逐项检查脚本、网络访问与写入范围；将扫描结果与实际环境、依赖锁定和人工复核结合。若团队复用，给每项批准决定和验证证据留下可追溯记录。

## 参考资料

- [项目 README](https://github.com/ch1109/portable-agent-skills)
- [仓库验证说明](https://github.com/ch1109/portable-agent-skills/tree/main/tests)
- [GitHub API 元数据快照](https://api.github.com/repos/ch1109/portable-agent-skills)
