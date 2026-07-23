# TokenScope

## 定位

`TokenScope` 是 Claude Code 本地会话 transcript 的 token profiler：它不预测成本，而是分析实际 JSONL usage、工具输出与读取行为，指出重复读取、错误循环、缓存未命中等上下文卫生问题。仓库创建于 2026-07-23，截至 2026-07-24 约 5 stars。

## 用法

可执行 `npx @asmitbohra/tokenscope` 查看项目概览，指定项目名查看会话拆分，或运行 `npx @asmitbohra/tokenscope codemap .` 生成签名级 `CODEMAP.md`。用项目根目录的 `.tokenscope.json` 屏蔽不适合自身流程的建议。

## 原理

工具解析 Claude Code 写入本地的 JSONL transcript，直接读取 API usage 字段作为 token 与 API-equivalent 费用的依据；再用确定性规则衡量 cache、重复读取、工具错误、压缩和 MCP 使用情况。工具结果的 token 估计与真实 usage 分开标注。

## 价值

- 用实际会话证据定位 token 浪费，而非基于一次性估算。
- 可帮助团队把大型文档、冗长 shell 输出和闲置 MCP schema 的问题具体化。
- `CODEMAP.md` 为 agent 提供低成本的仓库入口。

## 风险边界

- 只适用于 Claude Code transcript；订阅用户看到的是 API 等价价值而非实际账单。
- “低分”不等于低价值，验证、研究或长任务可能本就昂贵。
- transcript 含 prompt、代码路径与工具输出，运行前应确认本地访问和生成文件的边界。

## 补充建议

先在一个非敏感项目执行，只采纳可复验证据支持的建议。将验证密集型工作在配置中显式标注，避免为压 token 损害验收质量。

## 参考资料

- GitHub：<https://github.com/AviVAvi/TokenScope>
