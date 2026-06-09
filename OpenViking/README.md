# OpenViking

- GitHub: https://github.com/volcengine/OpenViking
- 官网/文档: https://www.openviking.ai
- 记录时间: 2026-03-15（Asia/Shanghai）

## 这是什么
OpenViking 是面向 AI Agent 的“上下文数据库（Context Database）”。它把 Agent 运行所需的 `memory / resources / skills` 用“类文件系统”统一管理，而不是分散在多个向量库、提示词文件和临时缓存里。

从今天 GitHub Trending（Today）快照看，`volcengine/OpenViking` 位于榜首附近，显示约 `1,557 stars today`，总星约 `10.5k`，属于当天增速很高的 Agent 基础设施项目。

## 为什么会被热议
1. Agent 工程正在从“单次对话”转向“长期任务”，上下文管理成为瓶颈。
2. 传统 RAG 常见问题是扁平检索、可观测性差、长期记忆难迭代。
3. OpenViking 把“目录结构 + 分层上下文 + 递归检索轨迹”组合成一套可调试的上下文系统，工程感更强。

## 怎么用（最小可跑通）

### 1) 环境要求
- Python >= 3.10
- Go >= 1.22
- GCC 9+ 或 Clang 11+

### 2) 安装
```bash
pip install openviking --upgrade --force-reinstall
```

可选 CLI（Rust）：
```bash
curl -fsSL https://raw.githubusercontent.com/volcengine/OpenViking/main/crates/ov_cli/install.sh | bash
```

### 3) 启动与导入资源
```bash
openviking-server

ov status
ov add-resource https://github.com/volcengine/OpenViking
ov ls viking://resources/
ov tree viking://resources/volcengine -L 2
ov find "what is openviking"
```

### 4) 想直接体验 Agent 聊天
```bash
pip install "openviking[bot]"
openviking-server --with-bot
ov chat
```

## 原理拆解（核心设计）

### 1) 文件系统范式统一上下文
OpenViking 使用类似 `viking://` 的虚拟层级路径，把资源、用户记忆、Agent 技能放进同一命名空间。优点是可管理、可审计、可追踪。

### 2) L0/L1/L2 分层上下文
写入后自动形成三层：
- L0: `.abstract`，短摘要，快速召回
- L1: `.overview`，结构化概览，支持规划阶段决策
- L2: 原始细节，按需深读

这样可降低 token 开销，减少“把所有上下文一次塞进提示词”的噪音问题。

### 3) 目录递归检索（Directory Recursive Retrieval）
其策略不是只做一次向量检索，而是：
1. 先做意图分析
2. 定位高分目录
3. 在目录内二次检索
4. 向子目录递归下钻
5. 聚合最终候选

这类“先锁定目录，再细化内容”的检索路径，对复杂任务通常比纯扁平语义搜索更稳。

### 4) 检索轨迹可观测
检索过程可映射到目录/文件路径，便于排查“为何命中/为何漏检”。这是很多黑盒 RAG 系统缺失的调试能力。

### 5) 会话结束后的记忆自迭代
系统支持把会话执行结果和反馈沉淀到用户/Agent 记忆目录，形成持续学习闭环。

## 适合什么场景
- 需要长期记忆的 Coding Agent
- 需要跨文档/跨项目资料管理的 Research Agent
- 需要追踪检索路径、调优命中率的企业 Agent 平台

## 风险与注意点
1. 需要额外治理目录结构和生命周期策略，否则会“有序膨胀”。
2. 分层摘要质量依赖底层模型，摘要偏差会传导到检索。
3. 生产环境建议独立服务部署，并设计权限隔离与配额。

## 参考来源
- GitHub Trending: https://github.com/trending
- OpenViking 仓库 README: https://github.com/volcengine/OpenViking
- OpenViking 文档: https://www.openviking.ai
