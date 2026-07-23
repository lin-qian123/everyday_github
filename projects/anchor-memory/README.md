# anchor-memory

## 定位

`anchor-memory` 是以单个 SQLite 文件为事实源的本地 agent 记忆系统，覆盖消息路由、混合召回、belief、记忆维护与评测。仓库创建于 2026-07-23，截至 2026-07-24 约 4 stars。

## 用法

创建虚拟环境后执行 `pip install -e .`，可先运行 `python scripts/generate_demo_db.py --data-dir ./data --json` 生成演示库；用 `anchor-demo --config config/anchor.example.toml recall "<query>"` 测试召回，并用 `anchor-maintenance health --config ... --json` 做健康检查。

## 原理

SQLite 持久化节点、边、belief、激活分数和维护事件；召回结合 FTS5、向量相似度、RRF、图扩散与 rerank。系统将意图路由、注入门控、时序衰减、反例复查和批量维护拆开，并保留可追踪的决策标识。

## 价值

- 本地、可携带的单文件事实源降低记忆数据被多个向量库分裂的风险。
- 混合检索、belief 和维护链路为长期 agent memory 提供完整实验样本。
- 支持 dry-run 与 JSON 输出，便于脚本化审计。

## 风险边界

- 项目明确将 AI agent 视为记忆语义作者/审阅者；这不应取代人类对隐私、事实和权限的最终负责。
- belief 分数与 LLM 分类会放大错误输入或偏差，需要人工可撤销机制。
- 默认本地嵌入不等于数据绝不会外流；启用可选 provider 前仍须检查配置。

## 补充建议

先用合成数据和只读召回评测，建立删除、导出与备份流程后再导入真实会话。把“事实记录”和“推断 belief”分库存放或至少分级查看。

## 参考资料

- GitHub：<https://github.com/anhe2021212-spec/anchor-memory>
