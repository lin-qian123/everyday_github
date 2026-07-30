# skill-audit-router

## 定位

`skill-audit-router` 是无第三方依赖的 Python 工具，用来盘点磁盘上的 `SKILL.md`、识别真正会被宿主加载的技能、重复/遮蔽项和描述难以路由的技能，并给出重写待办与评测入口。

截至 2026-07-31，GitHub API 快照显示它创建于 2026-07-30，约 5 stars、0 forks，MIT 许可证。README 中的示例统计是作者环境示例，不能外推到任意安装。

## 用法

克隆后可先运行自带 fixture；审计真实环境前，明确扫描根目录并先以只读报告检查发现范围。

```bash
git clone https://github.com/rushindrasinha/skill-audit-router.git
cd skill-audit-router
python skill_audit.py --roots examples/fixture-skills --include-workspace
```

随后按其文档的 audit、measure、rewrite、re-measure 循环处理，并避免让工具直接改写生产技能而没有版本控制 diff。

## 原理

项目区分“文件系统中存在”与“宿主可加载”，再以名称、描述、触发词和相似度分析可发现性与混淆。核心问题是 agent 常按技能元信息路由，而非逐个阅读全部正文，因此标签质量和安装路径都会影响召回。

## 价值

- 为大量 skills 的重复、影子副本和上下文占用提供可量化排查入口。
- 可把“技能真的被选中吗”转为可重测的工程假设，而非仅按文件数判断。

## 风险边界

- 各 agent 的加载、路由和上下文策略不同；静态评分不能证明某模型在真实任务中会或不会调用技能。
- 扫描目录可能暴露内部路径、技能内容或业务词汇，报告应作为敏感工程资产处理。
- 自动重写描述可能破坏既有触发语义；必须在 representative prompts 上回归。

## 补充建议

用真实任务语料建立小型 eval 集，分别记录加载率、正确路由、误触发和 token 成本。将安装清单与技能版本锁进仓库，先处理死副本和同名遮蔽，再调节描述。

## 参考资料

- GitHub：<https://github.com/rushindrasinha/skill-audit-router>
- GitHub API 快照：<https://api.github.com/repos/rushindrasinha/skill-audit-router>
- Agent Skills：<https://agentskills.io>
