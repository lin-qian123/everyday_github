# HERO-Anti-OverDefense

## 定位

HERO 是可粘贴到 `AGENTS.md`、`CLAUDE.md` 等文件的轻量约束块，给 coding agent 的过度防御命名为 Hashing、Edge cases、Rubrics、Overbuild 四类；它是经验性工作约定，不是安全模型或通用质量标准。

## 用法

从 `RULES.md` 选择完整或短版本，人工审阅后合并到宿主始终加载的指令文件。核心检查是：每项验证前说明它会发现的具体失败、结果会怎样改变行动；没有答案即不做无目的检查。

## 原理

用项目支持的真实输入/接口可达性区分真实缺陷与抽象极端情形；用是否替代更昂贵操作且改变后续行动评估额外哈希/guard；案例目录只供人类校准。规则 6 明确不覆盖已要求的安全、迁移、验证和审查。

## 价值

为长时程 agent 的 scope creep 提供具体语言和讨论边界，避免将无尽的可选不确定性降低升级为主任务。

## 风险边界

上游把模型动机解释列为观察假设。若机械执行“少检查”可能压制真实安全问题或可达 bug；粘贴规则不能替代测试、权限控制和人工审阅。

## 补充建议

在非关键仓库小范围试用，记录跳过和保留的检查，以缺陷逃逸、周期与覆盖变化评估；对安全、删除、迁移与发布任务显式写例外。

## 参考资料

- [GitHub 仓库](https://github.com/wanshuiyin/HERO-Anti-OverDefense)
- [规则与限制](https://github.com/wanshuiyin/HERO-Anti-OverDefense/blob/main/RULES.md)
- [案例目录](https://github.com/wanshuiyin/HERO-Anti-OverDefense/tree/main/cases)
