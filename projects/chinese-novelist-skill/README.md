<!-- markdownlint-disable MD013 MD034 -->

# chinese-novelist-skill：分阶段生成中文长篇小说的 Agent Skill

> 上游仓库：https://github.com/PenglongHuang/chinese-novelist-skill · 归类：办公、商业与行业应用 · 本页基于 2026-09-20 的 README、`SKILL.md`、流程参考、脚本、LICENSE 与 REST API 静态整理；未生成小说、运行并行 Agent 或评估文本质量。

## 定位

`chinese-novelist-skill` 把 10–50 章中文小说创作拆成偏好加载、三层问答、大纲 / 人物 / 计划确认、串行或多 Agent 写作、字数与连贯性检查、失败重写。它是长文本生产流程模板，不是版权、事实、原创性或出版质量保证。

2026-09-20 的 GitHub 官方 Python Trending 抓取显示约 `+44 stars today`；REST API 快照为 `3,109 stars / 453 forks / 15 open issues`，MIT。README 标称 `v2.0` 并链接 Release，但 REST API 无 GitHub Release，公开 tag 列表只见 `v1.0`，版本标识存在漂移。

## 用法

上游给出的快捷安装方式为：

```sh
npx skills add PenglongHuang/chinese-novelist-skill
```

也可把目录复制到 Claude Code skills 路径。触发后先回答题材、主角、冲突、世界观、视角、主题和章节数，再确认大纲与人物档案；随后选择串行、子 Agent 并行或 Agent Teams。输出写入 `chinese-novelist/<timestamp>-<标题>/`，并保存计划 JSON、人物、大纲和章节文件。

## 原理

- Phase 0 读取 `user-preferences.json` 与未完成项目，支持跨会话偏好和断点续写。
- Phase 1 用递进问答生成创作约束与标题候选；Phase 2 生成七列章节规划、人物档案和机器可读计划。
- Phase 2.5 选择主 Agent 串行、分批子 Agent 并行或 Agent Teams，并用计划 JSON 协调状态。
- Phase 3 逐章读取大纲，按“写前分析—撰写—润色—字数检查—摘要更新”循环生成。
- Phase 4 检查章节存在、字数和连贯性，不达标时最多重写三轮。

## 价值

- 将长篇创作从单次长 prompt 变成带大纲、人物、状态和文件结构的可恢复流程。
- 规划确认在大规模生成前保留一次明确人工闸门，降低题材或角色方向完全偏离的成本。
- 章节摘要、计划 JSON 与断点续写为长会话和多 Agent 协作提供持久状态。
- 参考资料细分人物、对话、悬念、结构和扩写，便于读者审阅具体创作规则。

## 风险边界

- 字数、文件齐全和自评连贯不等于文学质量、原创性、版权安全或“去 AI 痕迹”成功。
- 并行 Agent 可能造成角色语气、伏笔、时间线和世界规则漂移；计划 JSON 只能协调状态，不能自动证明全局一致。
- 偏好文件和草稿可能包含个人经历、真实人物或未公开创作，应纳入本地权限、备份和删除治理。
- 自动重写最多三轮是控制流程，不是独立 judge；同一模型生成和验收会共享偏差。
- README `v2.0`、release 链接与实际 tag / Release API 不一致，安装前应 pin commit，而非依赖模糊版本名。
- 本页未运行 Skill、未检查模型成本、长篇一致性、敏感内容、事实引用、抄袭相似度或出版平台规则。

## 补充建议

1. 先用 3–5 章短样本验证人物声线、伏笔回收、时间线和文件恢复，再扩大到长篇。
2. 把人物表、世界规则和时间线做成独立可测试约束；并行输出合并前做跨章人工审阅。
3. 真实人物、史实、专业知识和引用必须外部核验；最终稿再做原创性、版权和敏感内容检查。
4. 固定仓库 commit、宿主 Agent、模型与生成参数，并定期备份但不要把私密偏好和草稿提交到公共仓库。

## 参考资料

- 上游 README：https://github.com/PenglongHuang/chinese-novelist-skill
- Skill 入口：https://github.com/PenglongHuang/chinese-novelist-skill/blob/master/SKILL.md
- 流程参考：https://github.com/PenglongHuang/chinese-novelist-skill/tree/master/references/flows
- GitHub REST API：https://api.github.com/repos/PenglongHuang/chinese-novelist-skill
- LICENSE：https://github.com/PenglongHuang/chinese-novelist-skill/blob/master/LICENSE
