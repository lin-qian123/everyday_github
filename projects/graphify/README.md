# graphify（safishamsi/graphify）

- GitHub: https://github.com/safishamsi/graphify
- 记录日期: 2026-04-22 (Asia/Shanghai)

## 这是什么

`graphify` 是一个把代码、文档、论文、图片、音视频统一抽取为“可查询知识图谱”的 AI 编码助手技能，目标是加速大型代码库/多模态资料的结构化理解。

按 GitHub 页面快照（2026-04-22 抓取）约为 `32k stars`、`3.6k forks`，并且近期 issue/PR 活跃度很高。

## 为什么值得关注

1. 不是只做 RAG，而是强调“结构关系图 + 可解释证据标注”。
2. 同时支持代码与非代码资料，适合真实工程里的混合信息源。
3. 对“上下文窗口不够”的问题给了工程化方案（预抽取、缓存、图查询）。

## 怎么用（最短路径）

### 1) 安装

```bash
uv tool install graphifyy && graphify install
# 或
pipx install graphifyy && graphify install
```

### 2) 对当前目录生成图谱

```bash
/graphify .
```

输出目录通常包含：
- `graphify-out/graph.html`（交互图）
- `graphify-out/GRAPH_REPORT.md`（摘要与发现）
- `graphify-out/graph.json`（可编程查询）

### 3) 忽略无关文件

创建 `.graphifyignore`（语法同 `.gitignore`）控制扫描范围。

## 核心原理

1. 三阶段流水线
- 阶段一：基于 tree-sitter 的 AST 确定性抽取（结构、调用、注释线索）。
- 阶段二：本地转写音视频（可选 whisper/faster-whisper）。
- 阶段三：并行 Agent 抽取语义关系，融合为统一图结构。

2. 图拓扑聚类
利用图关系密度做社区发现（如 Leiden），让“模块边界、隐含耦合、关键节点”更直观。

3. 证据分层
关系可标记为 EXTRACTED / INFERRED / AMBIGUOUS，便于区分“直接证据”和“推断结论”。

4. 增量缓存
基于文件哈希缓存，重复运行时只处理变更内容，适合持续迭代项目。

## 适用场景

1. 新成员快速理解大型仓库。
2. 架构评审时识别耦合热点和隐式依赖。
3. 代码 + 设计文档 +会议材料联合检索。
4. 研究型项目中“论文-实现-实验记录”对齐。

## 价值与风险

价值：
- 把碎片化上下文压缩成可追溯知识网络。
- 让“为什么这样设计”更可查询而非只靠口口相传。

风险：
- INFERRED 关系若未经人工复核，可能误导决策。
- 多模态数据接入后，权限边界和敏感信息治理更复杂。

## 我认为有价值的补充材料

1. 为团队定义“图谱验收基线”（关键节点召回率、误连边率）。
2. 在 CI 中定期生成图谱快照，对比架构漂移。
3. 与 ADR（Architecture Decision Record）联动，形成“决策 -> 实现 -> 证据”闭环。

## 参考来源

- https://github.com/safishamsi/graphify
- https://github.com/safishamsi/graphify/blob/main/README.md
- https://ossinsight.io/trending
