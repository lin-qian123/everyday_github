# MemPalace（milla-jovovich/mempalace）

> 更新日期：2026-04-10（Asia/Shanghai）  
> 项目地址：https://github.com/milla-jovovich/mempalace

## 为什么今天值得关注

- 在近期 GitHub 趋势榜里，`milla-jovovich/mempalace` 处于高热区（Trendshift 2026-04-09 日榜 Top 1）。
- 仓库页抓取时约 `35.5k stars`、`4.5k forks`，讨论密度很高（Issues/PR 同步快速增长）。
- 它击中当前 Agent 工程核心痛点：**会话记忆丢失**（长期上下文不可持续）。

## 这个项目是做什么的

`MemPalace` 是一个“本地优先”的 AI 记忆系统，目标是让你和模型的历史对话不再在会话结束后消失。

核心思路不是“先总结再存储”，而是：

- 尽量保留原始对话（verbatim）
- 用结构化空间（wing/room/closet/drawer）组织记忆
- 用语义检索在需要时召回，而不是把全部历史硬塞进上下文窗口

适配场景：长期 coding agent、研究助手、团队项目复盘、客户沟通长期跟进。

## 怎么用（最短路径）

### 1) 安装

```bash
pip install mempalace
```

### 2) 初始化你的“记忆空间”

```bash
mempalace init ~/projects/myapp
```

### 3) 接入你的 agent 工作流

- 在项目里建立“人物/项目/主题”分区（wing）
- 把对话、决策、调试过程持续沉淀进去
- 每次会话唤醒时先加载关键 facts，再按需检索细节

## 原理是什么（可落地理解）

1. 原文存储优先（Raw Verbatim）
- 与“抽取偏好标签”的记忆系统不同，它倾向保存原始交流内容。
- 价值：可追溯性强，减少“总结丢语义”。

2. 分层记忆结构（Palace Layout）
- `Wing`：按项目/人/主题分区
- `Room`：按议题细分
- `Closet/Drawer`：更细粒度组织和定位原始内容
- 作用：降低检索噪声，提高 agent 定位效率。

3. 向量检索 + 元数据过滤
- 语义检索找相似片段，元数据过滤做范围收缩（例如只看某项目/某阶段）。
- 对 agent 来说，这比“全量上下文拼接”更稳，更省 token。

4. AAAK（实验压缩层）
- README 明确把 AAAK 标为实验能力：用于高复用实体的压缩表达。
- 当前官方说明中，AAAK 在基准上相对 raw 模式仍有明显退化，因此不应当作为默认路径。

## 典型工作流建议

- 研发团队：PR 讨论、架构争论、故障复盘全部入库；周会前按主题回溯。
- 独立开发者：把“试错过程”变成可检索资产，减少重复踩坑。
- AI 产品团队：把客服/用户反馈对话做长期记忆，支持策略迭代。

## 争议与风险（必须知道）

根据仓库 README 的 2026-04-07 勘误说明，社区在发布早期提出了关键质疑：

- AAAK 的 token 节省示例曾存在表述不准，后续已更正方向。
- “30x 无损压缩”等宣传语被下调，官方承认 AAAK 是有损压缩实验层。
- 96.6% LongMemEval 高分来自 raw 模式，不是 AAAK 模式。

这类公开纠错本身是正向信号，但也说明：

- 你在生产使用前要区分“稳定能力”和“实验能力”；
- 基准成绩要看具体模式、脚本可复现性和评测边界。

## 实操建议（给今天就想上手的人）

1. 先用 raw 模式跑 1~2 个真实项目周，验证检索命中率。
2. 把记忆结构按“人/项目/阶段”定好，再逐步细化房间。
3. AAAK 只做可选实验，不要直接上生产默认。
4. 给团队设一条规则：重要决策必须沉淀到可检索记忆层。

## 参考来源

- GitHub 仓库主页：https://github.com/milla-jovovich/mempalace
- GitHub Trending：https://github.com/trending?since=daily
- Trendshift 日榜（2026-04-09）：https://trendshift.io/
