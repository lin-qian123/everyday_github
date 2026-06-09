# TencentDB-Agent-Memory

## 定位
`TencentDB-Agent-Memory` 是面向 AI 代理的本地长短期记忆层，强调零外部 API 依赖与分层记忆组织。

- 仓库：<https://github.com/Tencent/TencentDB-Agent-Memory>
- 观察时间星标：约 2.3k stars

## 用法
- 按仓库 Quick Start 完成依赖安装与配置。
- 在代理系统中接入其 memory 插件/SDK，先验证短期压缩与长期检索链路。
- 结合自身任务类型调整记忆写入频率与摘要策略。

## 原理
- 将记忆拆分为符号化短期记忆与分层长期记忆。
- 通过结构化摘要替代原始日志堆积，降低 token 占用。
- 以场景/角色等结构组织长期信息，提升后续召回质量。

## 价值
- 对长会话、多阶段任务有较高价值，可减少上下文遗忘与重复解释。
- 本地化方案更易满足隐私和数据治理要求。

## 风险边界
- 记忆压缩策略若不当，可能丢失关键细节导致错误决策。
- 需要额外治理“记忆污染”和过期信息清理机制。

## 补充建议
- 建立可解释的记忆回溯日志，便于排查错误来源。
- 增加定期“记忆体检”任务（冲突检测、陈旧清理、重要度重排）。

## 参考资料
- GitHub: <https://github.com/Tencent/TencentDB-Agent-Memory>
- 趋势信号: <https://trendshift.io/>
