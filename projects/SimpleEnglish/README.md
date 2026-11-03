<!-- markdownlint-disable MD013 -->

# SimpleEnglish：用受控语言规则约束 AI 英文写作

- 上游：[AminBlg/SimpleEnglish](https://github.com/AminBlg/SimpleEnglish)；分类：Agent 框架与技能生态。
- 更新：2026-11-04（Asia/Shanghai）；固定 main SHA：`a6fcb4fde098b33617cc1578d151ebf58774b883`。
- 热度：Python daily +50；API 4,200 stars / 179 forks / 14 open issues（含 PR）。最新 v2.1.1，UTC 2026-09-30；MIT。
- 证据范围：官方榜单、API、发行与固定技能 / hook 说明；未安装插件、重跑评估或开展读者测试。

## 定位

受 ASD-STE100 Simplified Technical English 启发的英文写作技能。Plain 为默认，Strict 再加词汇纪律；区分文档与聊天回复两套规则，适合 README、运行手册、报错和技术说明。它是非官方项目，不提供 STE 认证。

## 用法

上游技能安装入口：

```sh
npx skills add AminBlg/SimpleEnglish
```

此方式只装技能，不会安装 session hook 或 output style。审查并固定本页 SHA 后，再按目标宿主安装完整目录，用一段已有英文文档比较改写结果。

Claude Code 插件另提供 SessionStart、output style 和 advisory 检查；Codex 插件只运行 SessionStart。Hook 需 Node.js；Claude Code 的文件 / 回复检查另调用 Python。不要从“技能无依赖”推断插件全部功能无运行依赖。

## 原理

- 文档规则约束祈使句、主动语态、条件先于命令、指令 20 词 / 描述 25 词上限、术语首次解释与同词同义。
- 技能要求保留代码、标识符、命令、路径、引文错误文本和事实；回复规则另外限制标题、列表和强调格式。
- SessionStart 将压缩规则注入上下文；Claude Code 的 PostToolUse / Stop 检查只提示问题，不阻止完成。
- 机械 linter 计数句长和部分格式规则；词汇工具需用户自己的标准 PDF，仓库不分发标准词典。

## 价值

把“写清楚”拆成可检查的表达约束，便于团队统一英文操作文档。对于条件、动作、主机和前置步骤明确的任务，能提供具体修订方向；事实正确和读者理解需要另行验证。

## 风险边界

- README 的 95% 更少回复可见缺陷来自 2026-09-02 的 2.0.1、8 个问题各两次，共 16 条回复；计数对象是破折号、加粗、标题和列表，不是读者错误率。
- 2.1.0 已删除五句回复上限，2.1.1 再改措辞；发行说明明确没有新版 benchmark，不能将旧结果标为当前版本实测。
- 文档 78% 更少 linter 违规来自 8 个任务、每条件一次；模型家族评审偏差和单次波动已由作者披露，不能外推为普遍理解提升。
- Plain / Strict、语法约束与正式标准合规不同；词典有独立复制限制，MIT 不覆盖第三方标准。
- 把 may / should 等一律改写可能改变证据强度或规范性要求；虽然技能要求保留事实，科研和合同等文本仍应逐句检查语义与不确定性。

## 补充建议

1. 用真实读者测试任务完成率、误解和时间，同时检查事实、数值、警示、命令与限定词是否保留。
2. 区分技能按需触发与插件全会话注入，避免写作风格挤占代码、中文科研或结构化交付要求。
3. 固定模型 / 版本重跑自己的文档集，分别记录格式遵守、术语一致和读者理解。

## 参考资料

- [README 与评估边界](https://github.com/AminBlg/SimpleEnglish/blob/a6fcb4fde098b33617cc1578d151ebf58774b883/README.md)、[技能规则](https://github.com/AminBlg/SimpleEnglish/blob/a6fcb4fde098b33617cc1578d151ebf58774b883/skills/simple-english/SKILL.md)。
- [Hook 说明](https://github.com/AminBlg/SimpleEnglish/blob/a6fcb4fde098b33617cc1578d151ebf58774b883/src/hooks/README.md)、[LICENSE](https://github.com/AminBlg/SimpleEnglish/blob/a6fcb4fde098b33617cc1578d151ebf58774b883/LICENSE)。
- [API](https://api.github.com/repos/AminBlg/SimpleEnglish)、[v2.1.1](https://github.com/AminBlg/SimpleEnglish/releases/tag/v2.1.1)、[v2.1.0 口径变更](https://github.com/AminBlg/SimpleEnglish/releases/tag/v2.1.0)。
