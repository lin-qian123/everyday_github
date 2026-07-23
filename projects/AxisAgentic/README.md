# AxisAgentic

## 定位

`AxisAgentic` 是长时程 AI agent 的可扩展 runtime 与评测框架，提供状态忠实的多轮执行、工具编排、上下文管理、trace、评测和训练数据导出。仓库创建于 2026-07-23，截至 2026-07-24 约 8 stars。

## 用法

项目要求 Python 3.12+ 与 OpenAI-compatible endpoint。克隆后按 `setup_env.sh` 初始化环境，复制 web-search recipe 的 YAML 配置，填写数据集与 provider 参数，先运行 `python -m recipe.web_search.runners.run_eval_config --config <file> --dry-run`，确认解析后的运行计划再启动评测。

## 原理

runtime 将可追加 trace 作为每轮上下文的事实来源，并将模型客户端、工具、数据集、评测器、奖励与 recipe policy 解耦。它内置预算、压缩、回滚、重试、验证和 trace 导出，使一次 rollout 可复放、比较或转为 SFT 数据。

## 价值

- 为长时程 agent 提供比单次 prompt 更可复现的执行/评测骨架。
- 将任务 recipe 与通用 runtime 分离，利于比较不同工具和策略。
- 配置与轨迹产物能支撑研究和工程验收。

## 风险边界

- 当前旗舰 recipe 是 web search，不能据此推断 coding agent 的同等表现。
- README 的 benchmark 对比承认不同 harness、工具与评测日期，不是统一受控排名。
- 要求外部模型端点和数据集；费用、数据出境与工具权限应由使用者控制。

## 补充建议

先以 `--dry-run` 固化配置、路径和预算，再用小型私有评测验证 trace 可重放性。对公开 benchmark 结果应保留原始配置与 evaluator 版本。

## 参考资料

- GitHub：<https://github.com/XYZ-AI-Lab/AxisAgentic>
- 技术报告：<https://xyz-lab.ai/blogs/ai4ai-at-scale/>
