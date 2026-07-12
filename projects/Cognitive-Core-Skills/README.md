# Cognitive-Core-Skills

<!-- markdownlint-disable MD013 -->

## 定位

`Cognitive-Core-Skills` 是一个面向 LLM、SLM、AI agents 和 world models 的认知能力 taxonomy 项目。它把感知、记忆、推理、规划、行动选择、验证、学习、治理等能力整理成 schema、skill cards、benchmark fixture 和 CI 校验。

截至 2026-07-13，GitHub API 显示该仓库约 275 stars、77 forks，创建于 2026-07-05，许可证为 MIT。它更像 agent 能力建模与评估资料库，而不是直接运行的 agent 产品。

## 用法

README 建议从以下路径入手：

```text
docs/cognitive-core-skills/
data/
Skills/index.md
```

项目当前标注 taxonomy version `1.0.0`，包含 159 个 skill cards、13 个 domains，并提供 JSON / YAML / Markdown 等可复用形态。

## 原理

项目把 agent 所需能力拆成机器可读和人可读两层：文档解释概念与评估口径，`data/` 提供结构化 taxonomy，`Skills/` 生成技能卡，CI 用于验证 taxonomy 和 benchmark fixture 的一致性。

## 价值

- 给 agent 产品、评测、skill marketplace 和 governance 提供统一语言。
- 适合做能力盘点、benchmark 设计、课程结构和 agent skill catalog 的底稿。
- 明确把 governance、verification、memory、planning 放进核心能力，而不只看推理能力。
- 可与 `awesome-harness-engineering`、`nvidia-skills`、`SkillSpector` 形成“能力定义 - 技能分发 - 安全审计”的链条。

## 风险边界

- taxonomy 不等于实测能力，仍需真实任务和可复现评估支撑。
- 分类体系可能过宽，落地时需要按团队任务裁剪。
- 159 张 skill cards 的质量和粒度需要人工审查，不能直接当标准。
- 如果被产品营销滥用，容易把概念标签误当能力证明。

## 补充建议

- 适合用于搭建 agent 能力矩阵或内部评测 rubric。
- 若要接入实际工具，应优先使用结构化 `data/`，避免手工复制 Markdown。
- 继续观察是否出现第三方 benchmark 或其他 skill 项目引用该 taxonomy。

## 参考资料

- GitHub 仓库：<https://github.com/eli-labz/Cognitive-Core-Skills>
- Skill cards 索引：<https://github.com/eli-labz/Cognitive-Core-Skills/blob/main/Skills/index.md>
- Taxonomy 文档：<https://github.com/eli-labz/Cognitive-Core-Skills/tree/main/docs/cognitive-core-skills>
