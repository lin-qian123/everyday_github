# ironcode

- 仓库：[djfksjd/ironcode](https://github.com/djfksjd/ironcode)
- 快照：2026-08-05 抓取；GitHub API 显示其创建于 2026-08-04，约 11 stars、1 fork，MIT。数字会随时间变化。
- 分类：Agent 框架与技能生态

## 定位

面向 Claude Code 与 Codex CLI 的工程质量 gate skill，强调任何“完成”声明都必须有新鲜、可观察的测试、构建或运行证据，并覆盖安全、资源、数据访问、鲁棒性和可维护性。

## 用法

按 README 克隆到对应的 skills 目录后，通过 `/ironcode` 或明确要求严格实现/审查触发。先在一个小型 PR 上运行，确认它只读取预期文件、不会替你执行部署或外部变更，再逐步接入团队流程。

## 原理

skill 根据 PLAN、BUILD、GATE 阶段按需载入参考清单：先确认规格和根因，再审查资源释放、N+1/分页、注入/授权、边界条件与发布准备度，最后用实际命令生成可定位的证据。

## 价值

它将常被 agent 跳过的验证、成本与资源安全检查写成可重复门槛，适合作为代码生成之后的第二道审阅框架。按需加载也避免每个小修改都引入整套长清单。

## 风险边界

规则包不能替代威胁建模、领域测试和人工 code review；“通过”只代表实际执行的检查覆盖到的范围。安装第三方 skill 前应审查其内容、hook 和更新来源，不能让它自动拥有生产访问权。

## 补充建议

把项目自身的验收命令、SLO 和安全规范映射到该 skill 的 gate；要求报告列出执行命令、环境与未覆盖项。对高风险改动仍采用独立 reviewer、CI 和分阶段发布。

## 参考资料

- [项目 README](https://github.com/djfksjd/ironcode)
- [安全检查参考](https://github.com/djfksjd/ironcode/blob/main/references/security.md)
- [GitHub API 元数据快照](https://api.github.com/repos/djfksjd/ironcode)
