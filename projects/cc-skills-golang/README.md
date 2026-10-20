<!-- markdownlint-disable MD013 -->

# cc-skills-golang

> 更新：2026-10-21（Asia/Shanghai）。分类：Agent 框架与技能生态。上游 `samber/cc-skills-golang`；快照 `8e899e20ff0c`（main）。本文为官方资料与源码静态研究；热度、发行时间及社媒限制见[当日日报](../../daily/2026-10-21/ai-hotspots.md)。

## 定位

面向 Go 项目的 Agent Skills，覆盖风格、错误处理、测试、并发、性能、安全及常用库。作者声明从实际提交中提炼并经人工编辑；这是作者过程说明，不是本轮独立验证的质量认证。[README.md](https://github.com/samber/cc-skills-golang/blob/8e899e20ff0cd4dc524af3993e4c62d8ee8c5717/README.md)

## 用法

通用入口为 `npx skills add https://github.com/samber/cc-skills-golang --skill golang-performance`，也可按文档整套安装。先选清晰的目标与关联通用规则，再在测试项目核宿主发现的实际 skills。[README.md](https://github.com/samber/cc-skills-golang/blob/8e899e20ff0cd4dc524af3993e4c62d8ee8c5717/README.md)

README 的 Codex 小节当前指向另一个 `samber/cc-skills` 仓库，区别于本页 Go 仓库；采用前核下载目标，不把该命令当成已验证的 Go 专项安装。[README.md](https://github.com/samber/cc-skills-golang/blob/8e899e20ff0cd4dc524af3993e4c62d8ee8c5717/README.md)

## 原理

SKILL 元数据帮助触发，正文与 references / assets 提供操作规范和示例；技能间互相引用，如错误处理会影响日志规则。性能技能要求围绕测量与 profiling，安全技能提供威胁、输入和依赖检查；这些属于指导，实际工具执行仍由宿主完成。[README.md](https://github.com/samber/cc-skills-golang/blob/8e899e20ff0cd4dc524af3993e4c62d8ee8c5717/README.md) [skills/golang-performance/SKILL.md](https://github.com/samber/cc-skills-golang/blob/8e899e20ff0cd4dc524af3993e4c62d8ee8c5717/skills/golang-performance/SKILL.md) [skills/golang-security/SKILL.md](https://github.com/samber/cc-skills-golang/blob/8e899e20ff0cd4dc524af3993e4c62d8ee8c5717/skills/golang-security/SKILL.md)

## 价值

工程判断：可把团队 Go 约定变成可审阅、可版本固定的上下文，减少重复解释。适合挑真实任务做有 / 无技能对照，保留 reviewer 结果，而不是只看 Agent 自评。

## 风险边界

- README 的 overall 97% 对 57% 与各技能 error-rate gap 是作者评估；本轮未读取完整评估夹具、未复跑，不能外推为生产缺陷率下降。[README.md](https://github.com/samber/cc-skills-golang/blob/8e899e20ff0cd4dc524af3993e4c62d8ee8c5717/README.md)
- 单独装一个技能可能缺少其引用的规则；一次装全套又可能扩大上下文与指令冲突，应核实际加载、优先级和安装范围。[README.md](https://github.com/samber/cc-skills-golang/blob/8e899e20ff0cd4dc524af3993e4c62d8ee8c5717/README.md)
- MIT 覆盖仓库代码 / 文本条款，不保证第三方工具、库版本和模型数据政策。技能不是权限边界，运行命令仍需遵循项目和宿主授权。[LICENSE](https://github.com/samber/cc-skills-golang/blob/8e899e20ff0cd4dc524af3993e4c62d8ee8c5717/LICENSE) [skills/golang-security/SKILL.md](https://github.com/samber/cc-skills-golang/blob/8e899e20ff0cd4dc524af3993e4c62d8ee8c5717/skills/golang-security/SKILL.md)

## 补充建议

固定 commit，在一次性 Go 模块中做一项性能或错误处理任务，检查实际触发的文件、基准条件与人工审阅差异。要引用总体提升数字时再核 EVALUATIONS 的模型、样本与评分方法。本轮没有安装或运行技能。

## 参考资料

- [README.md](https://github.com/samber/cc-skills-golang/blob/8e899e20ff0cd4dc524af3993e4c62d8ee8c5717/README.md)
- [skills/golang-performance/SKILL.md](https://github.com/samber/cc-skills-golang/blob/8e899e20ff0cd4dc524af3993e4c62d8ee8c5717/skills/golang-performance/SKILL.md)
- [LICENSE](https://github.com/samber/cc-skills-golang/blob/8e899e20ff0cd4dc524af3993e4c62d8ee8c5717/LICENSE)
- [skills/golang-security/SKILL.md](https://github.com/samber/cc-skills-golang/blob/8e899e20ff0cd4dc524af3993e4c62d8ee8c5717/skills/golang-security/SKILL.md)
- [仓库 API](https://api.github.com/repos/samber/cc-skills-golang)
- [v2.0.0 Release](https://github.com/samber/cc-skills-golang/releases/tag/v2.0.0)
