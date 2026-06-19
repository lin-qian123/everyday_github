# GLM-5（zai-org/GLM-5）

- GitHub: https://github.com/zai-org/GLM-5
- 博客: https://z.ai/blog/glm-5.2
- 技术报告: https://arxiv.org/abs/2602.15763
- 记录日期: 2026-06-19 (Asia/Shanghai)

## 定位

`GLM-5` 是智谱 / Z.ai 面向长时程 agentic engineering 的开源大模型系列仓库，当前公开覆盖 `GLM-5`、`GLM-5.1`、`GLM-5.2`。它不是只强调“会写几段代码”的 coder 模型，而是直接把目标放在复杂系统工程、长会话工具调用和大上下文任务执行。

## 热度信号

1. GitHub API 在 2026-06-19 抓取时显示约 `4.1k stars`、`432 forks`，且仓库 `updated_at` 为 `2026-06-19T01:02:03Z`。
2. GitHub 通用 Trending 页面在 2026-06-19 抓取时出现 `zai-org/GLM-5`，说明它已进入当天开发者公共热点窗口。
3. 官方 README 直接把项目标题写成 `From Vibe Coding to Agentic Engineering`，并连续给出 `GLM-5.2`、`GLM-5.1`、`GLM-5` 的编码与长时程 benchmark 结果，定位非常鲜明。

## 用法

### 1) 直接下载模型

官方 README 提供 Hugging Face 与 ModelScope 链接，覆盖 `GLM-5` / `5.1` / `5.2` 以及 `FP8` 版本。

### 2) 本地推理部署

官方注明 `GLM-5.2` 可通过以下框架部署：

- `SGLang`
- `vLLM`
- `Transformers`
- `KTransformers`
- `Ascend NPU` 相关推理框架

### 3) 控制推理强度

README 提供 `reasoning_effort` 参数，用于在 `max` 与 `high` 两档之间调节思考预算；也可通过 `enable_thinking=false` 关闭思考链路。

## 原理

1. 该系列继续沿着“超长上下文 + 稀疏注意力 + agentic task 对齐”的路线推进，而不是单纯做聊天优化。
2. `GLM-5.2` 在 README 中强调 `1M-token context`，并引入 `IndexShare` 这类为长上下文降 FLOPs 的架构改动。
3. 仓库把“模型能力”与“工程可部署性”同时摆到台面，直接给出多框架推理接入路径，说明它想争夺的是实际工作流入口，而不是只做论文样例。
4. README 反复强调在 `Terminal-Bench`、`SWE-bench Pro`、`Vending Bench 2` 这类偏真实任务或长时程任务上的结果，说明其核心卖点是长链路执行稳定性。

## 价值

- 对想比较开源 frontier coding / agent 模型的人，这个仓库是 2026 年中必须纳入样本的一支。
- 它把“开源模型是否能承担长时程 agent 工程任务”这个问题重新拉回前台，而不是只比一次性 benchmark 分数。
- 对自建推理栈团队来说，`GLM-5.2` 同时支持大上下文和多推理框架，意味着它更适合做内部 agent 平台底模评估。

## 风险边界

- 仓库里的 benchmark 主要来自官方 README、技术报告和自家实验设置，适合看方向，不应直接当成你业务环境下的生产结论。
- `744B-A40B` 级别模型对推理资源、部署复杂度和成本提出很高要求，不是普通本地工作站就能轻松承载的方案。
- “更强 agentic engineering” 不等于在所有真实仓库都更稳，尤其在私有代码、工具异常、长会话中断和多步回滚上仍需单独验证。

## 补充建议

1. 如果你关心的是“终端里能不能连续干活”，优先把它与 `codex`、`claude-code`、`qwen-code` 的真实仓库任务做 A/B 对比，而不是只看公开榜单。
2. 若资源有限，可先从云端 API 或社区量化版本试用，再决定是否投入本地推理部署。
3. 在团队内部评估时，除正确率外，还应记录长会话稳定性、工具调用成功率、回滚能力和总 token / GPU 成本。

## 参考资料

- https://github.com/zai-org/GLM-5
- https://z.ai/blog/glm-5.2
- https://arxiv.org/abs/2602.15763
- https://github.com/trending
