# 666ghj/MiroFish

- GitHub: https://github.com/666ghj/MiroFish
- 记录时间: 2026-03-21（Asia/Shanghai）

## 这是什么
`MiroFish` 是一个“群体智能 + 多智能体仿真”的预测引擎。项目核心目标不是回答单点问题，而是把现实世界的“种子材料”（新闻、政策、金融信号、报告、故事文本）转成一个可交互、可演化的数字世界，再在这个世界里做推演。

根据仓库 README，系统流程包括：
1. 图谱构建（现实种子提取 + 记忆注入 + GraphRAG）
2. 环境搭建（实体关系抽取 + 人设生成 + 仿真参数注入）
3. 开始模拟（并行模拟 + 时序记忆动态更新）
4. 报告生成（ReportAgent 与仿真环境交互输出）
5. 深度互动（和模拟世界中角色继续对话）

## 为什么今天值得跟进
GitHub Trending（抓取时间：近 7 天内快照）显示该项目在 AI 工具里处于前列，且当日增星非常高：
- `666ghj/MiroFish`：`2,294 stars today`
- 同榜单还有 `openclaw/openclaw`（9,164 stars today）、`msitarzewski/agency-agents`（4,415 stars today）等

这意味着它不是“长尾慢热”，而是近期高传播、高讨论的短期爆发项目。

## 怎么用（最小可跑）
以下命令来自项目 README（源码部署路径）：

### 1) 环境前置
- Node.js 18+
- Python >=3.11 且 <=3.12
- `uv`（Python 包管理器）

### 2) 配置环境变量
```bash
cp .env.example .env
# 填写至少以下变量
# LLM_API_KEY
# LLM_BASE_URL
# LLM_MODEL_NAME
# ZEP_API_KEY
```

### 3) 安装依赖
```bash
npm run setup:all
# 或分步：npm run setup && npm run setup:backend
```

### 4) 启动
```bash
npm run dev
# 前端: http://localhost:3000
# 后端: http://localhost:5001
```

### 5) Docker 方案
```bash
cp .env.example .env
docker compose up -d
```

## 原理拆解（工程视角）

### 1) 从“问答”转向“环境建模”
传统 LLM 工具多是“输入问题 -> 输出答案”；MiroFish 更像“输入现实材料 -> 建一个可演化世界 -> 读取世界演化结果”。

### 2) 关键技术路线
- `GraphRAG`：把实体关系和上下文组织成图结构，减少纯向量检索丢关系的问题。
- `Agent Memory`：给个体与群体引入记忆，使行为不是“单回合反应”，而是“跨时序演化”。
- `Multi-Agent Simulation`：通过多角色交互形成涌现行为，适合推演舆情、政策、市场情景。
- `ReportAgent`：在仿真后世界中取证、归纳、写报告，降低人工总结成本。

### 3) 为什么会出圈
- 叙事上直观：“数字沙盘 + 上帝视角”比纯文本分析更容易传播。
- 使用门槛相对可控：README 给了源码和 Docker 两条启动路径。
- 场景覆盖广：舆情、政策、金融、创作推演都能套同一框架。

## 适用场景
- 舆情预演：品牌公关事件可能走向。
- 策略演练：政策/运营动作的多方反应推演。
- 创作世界观推演：小说结局、角色关系分叉。
- 教学与演示：解释“多智能体涌现”比单模型推理更直观。

## 风险与边界
1. 预测不等于事实，输出受种子材料质量和先验假设强约束。
2. 多智能体仿真很容易“看起来合理”，需要外部基准验证。
3. API 成本和仿真轮数成正比，README 也提示先做小轮次试跑。
4. 若用于公共决策，必须补充人工审查与可追溯记录。

## 建议的评估方式
- 先做小规模回测：用已知结果的历史事件做盲测。
- 记录关键假设：每次注入变量都要可追踪。
- 输出分层：事实证据 / 模型推断 / 猜测建议分开写。
- 对照基线：与简单统计模型或人工专家判断做并行对比。

## 参考来源
- GitHub 仓库: https://github.com/666ghj/MiroFish
- GitHub Trending: https://github.com/trending
- 项目在线 Demo（README 提供）: https://666ghj.github.io/mirofish-live-demo
