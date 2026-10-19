<!-- markdownlint-disable MD013 -->

# Marble Skill Taxonomy（os-taxonomy）

> 更新：2026-10-20（Asia/Shanghai）。分类：AI 学习与教育资源。上游 `withmarbleapp/os-taxonomy`；快照 `ff9853306ba0`（main）。本文基于官方榜单、认证 API 与上游文件静态研究；热度、版本时间与跨平台证据见[当日日报](../../daily/2026-10-20/ai-hotspots.md)。

## 定位

Marble 公开的基础教育微主题知识图谱数据集：将儿童学习主题、前置关系、课程标准映射和教学建议表示为 JSON。适合研究 AI 辅助课程规划、知识依赖检索与学习活动设计；不是学生能力测评模型，也不是被教育实验验证的自适应系统。[README.md](https://github.com/withmarbleapp/os-taxonomy/blob/ff9853306ba0c36a3e0045f43054f6039f62b0e5/README.md)

## 用法

直接读取 `data/topics.json` 和 `data/dependencies.json`，按稳定 topic ID 建索引。边的方向为 `topicId` 依赖 `prerequisiteId`，反向查找才是可解锁后续主题；教学建议以 `topicId` 连接 `teaching-research.json`。建议先取小型子图，保留缺覆盖状态。[README.md](https://github.com/withmarbleapp/os-taxonomy/blob/ff9853306ba0c36a3e0045f43054f6039f62b0e5/README.md)

上游提供 `node scripts/validate.mjs` 与 `node --test scripts/teaching-research.test.mjs` 检查结构、覆盖、来源连接及校验和。本轮读取 manifest / 文档，没有下载全部数据或执行这些检查。

## 原理

采样 v1 manifest 声明 1,591 个主题、3,225 条前置边、176 个 cluster、7 套课程 / 3,261 条标准；教学 research 覆盖 Science 547 与 Mathematics 504，共 1,051 个主题，其余 540 个主题无该层资料。manifest 包含各文件 SHA-256 与 research 绑定的 topic hash，可用于检测跨版本错配。[data/manifest.json](https://github.com/withmarbleapp/os-taxonomy/blob/ff9853306ba0c36a3e0045f43054f6039f62b0e5/data/manifest.json)

教学 research 由 Agent 编写，再经过面向可移植性的改写、另一 critic 检查与抽样。资料中的 confidence / source verification flag 是作者生产记录，不是独立质量评分；结构连接正确也不证明教学因果有效。[README.md](https://github.com/withmarbleapp/os-taxonomy/blob/ff9853306ba0c36a3e0045f43054f6039f62b0e5/README.md)[PROVENANCE.md](https://github.com/withmarbleapp/os-taxonomy/blob/ff9853306ba0c36a3e0045f43054f6039f62b0e5/PROVENANCE.md)

## 价值

相比平面课程目录，显式前置关系及其理由有利于解释推荐路径，缺覆盖清单有利于防止 AI 将缺失内容“补成事实”。可用来搭建有来源的教学检索原型，再由学科教师核任务与年龄适配。

## 风险边界

- 图谱不代表每个儿童都遵循相同学习顺序；年龄范围、掌握标准与生成活动不能直接用作能力诊断。README 明示部分活动无直接 source claim，保留的旧教学 / assessment 文本可能比更新 guidance 更绝对。[README.md](https://github.com/withmarbleapp/os-taxonomy/blob/ff9853306ba0c36a3e0045f43054f6039f62b0e5/README.md)
- publication 沿用原来源标志而未重新抓取原始文献，课程对齐不是教学干预效果证据。不得把 Agent critic / 抽样写成真人教学实验或全量事实核验。[PROVENANCE.md](https://github.com/withmarbleapp/os-taxonomy/blob/ff9853306ba0c36a3e0045f43054f6039f62b0e5/PROVENANCE.md)
- 多层许可必须拆开：数据库结构 / 关系 ODbL-1.0，Marble 自写正文 CC BY-SA 4.0，第三方课程标准仍按其上游条款。GitHub API 单个 SPDX 不覆盖全部文件。[LICENSE](https://github.com/withmarbleapp/os-taxonomy/blob/ff9853306ba0c36a3e0045f43054f6039f62b0e5/LICENSE)[LICENSE-CONTENT](https://github.com/withmarbleapp/os-taxonomy/blob/ff9853306ba0c36a3e0045f43054f6039f62b0e5/LICENSE-CONTENT)[PROVENANCE.md](https://github.com/withmarbleapp/os-taxonomy/blob/ff9853306ba0c36a3e0045f43054f6039f62b0e5/PROVENANCE.md)
- 部分受限标准仅发布 codes；导出对长文字匹配的机械移除不构成全面权利清理。二次分发应保留逐源声明，不能因数据库可商用而认定全部课程正文可任意重发。公开数据未包含儿童个人记录；接入真实学生系统时需另行设计隐私边界。[PROVENANCE.md](https://github.com/withmarbleapp/os-taxonomy/blob/ff9853306ba0c36a3e0045f43054f6039f62b0e5/PROVENANCE.md)[README.md](https://github.com/withmarbleapp/os-taxonomy/blob/ff9853306ba0c36a3e0045f43054f6039f62b0e5/README.md)

## 补充建议

先对小子图做 ID 引用、方向、环路和年龄异常检查，逐条核 hard / soft 关系及教学引用。保存 manifest、数据 hash、未覆盖主题与教师修改记录；若要验证推荐价值，需要另行设计有基线与明确学习指标的研究。本轮没有进行教学有效性或法律合规结论评估。

## 参考资料

- [README.md](https://github.com/withmarbleapp/os-taxonomy/blob/ff9853306ba0c36a3e0045f43054f6039f62b0e5/README.md)
- [LICENSE](https://github.com/withmarbleapp/os-taxonomy/blob/ff9853306ba0c36a3e0045f43054f6039f62b0e5/LICENSE)
- [LICENSE-CONTENT](https://github.com/withmarbleapp/os-taxonomy/blob/ff9853306ba0c36a3e0045f43054f6039f62b0e5/LICENSE-CONTENT)
- [PROVENANCE.md](https://github.com/withmarbleapp/os-taxonomy/blob/ff9853306ba0c36a3e0045f43054f6039f62b0e5/PROVENANCE.md)
- [data/manifest.json](https://github.com/withmarbleapp/os-taxonomy/blob/ff9853306ba0c36a3e0045f43054f6039f62b0e5/data/manifest.json)
- [仓库 API](https://api.github.com/repos/withmarbleapp/os-taxonomy)
