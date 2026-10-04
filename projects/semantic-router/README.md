<!-- markdownlint-disable MD013 -->

# vLLM Semantic Router（vllm-project/semantic-router）

> 上游仓库：<https://github.com/vllm-project/semantic-router> · 归类：模型、训练与推理基础设施 · 本页基于 2026-10-05 的 GitHub API、README、FAQ、部署 / security hardening、SECURITY、Release 与 LICENSE 静态整理，未部署 Envoy / Kubernetes、接入 provider、训练 classifier 或复测路由质量、成本与延迟。

- 抓取快照：6,030 stars、1,008 forks、617 open issues。
- 热度信号：GitHub Go Trending 抓取时约 +16 当日 stars。
- 版本与许可：Apache-2.0；latest Release / tag 为 `v0.4.0`。

## 定位

vLLM Semantic Router 是 Mixture-of-Models 的可编程决策层：根据请求信号、用户偏好和应用策略，选择或组合模型、recipe 与执行路径。它位于客户端 / gateway 与异构模型端点之间，目标是在质量、成本、延迟、隐私和安全约束之间做显式路由，而不是替代 TLS 终止、负载均衡或 pod 调度。

## 用法

上游提供安装脚本、pip / uv、Docker、Kubernetes / Operator 与硬件特定部署入口。用户在统一配置中声明模型 / provider、signal、decision、cache / memory 与 route，再通过 Envoy ExtProc filter 或本地 listener 转发兼容请求；`route preview` 可只计算决策，`route probe` 才发送真实请求并核验 selected-model receipt 和最终交付。

## 原理

router 先从 prompt、header、session 和外部状态提取 signal，可调用 embedding / classifier、PII / jailbreak、complexity、semantic cache 与 policy 模块；decision graph 再选模型或 fusion / micro-agent recipe。Envoy 执行数据面改写，route header 提供可观察回执，session-scoped state、replay 与 store 支持连续决策；后端模型本身仍由独立推理基础设施运行。

## 价值

它把“为何选这个模型”从业务代码提升为可配置、可预览、可测量的控制面，便于在自托管、边缘和云模型之间执行数据位置、成本、能力和用户偏好规则。丰富的 benchmark contract、trace、header 和部署文档也有助于把路由正确、交付成功与答案质量分开验收。

## 风险边界

- router 位于推理关键路径，会同时接触 prompt、response、provider key、route metadata、cache / memory 与管理面；暴露 ExtProc、metrics、store 或 dashboard 端口会扩大攻击面。
- PII、jailbreak、复杂度和质量 classifier 都可能被对抗输入或分布漂移误导；“有 guardrail / classifier”不能证明不会绕过安全策略。
- 选择本地模型不自动保证数据只留在本地：route 的 provider、tools、cache、replay、logs 和 observability 分别有自己的数据位置与保留期。
- 一次 HTTP 200 不等于交付成功、路由正确或答案高质量；上游 FAQ 也要求分别检查 delivery、selected-model receipt 与 paired quality evidence。
- 安装脚本为远程 shell 管道；生产应固定 `v0.4.0` 制品、镜像 digest、模型和 gateway / Envoy 版本，而非直接执行浮动 stable channel。
- 本轮未复测 sr-bench、论文结论、路由节省、fusion / micro-agent 质量、cache 一致性或故障转移。

## 补充建议

先在合成数据与两个固定模型上部署最小闭环，把 `route preview`、`probe`、receipt、provider 账单和答案评分写入同一实验记录；对 PII / jailbreak / 长上下文和 header spoof 做对抗测试。管理面、store 和 metrics 只放私网，密钥分 route 最小授权，并明确日志、cache、replay 与 session 的保留 / 删除策略。

## 参考资料

- [GitHub 仓库](https://github.com/vllm-project/semantic-router)
- [GitHub REST API](https://api.github.com/repos/vllm-project/semantic-router)
- [README 与安装入口](https://github.com/vllm-project/semantic-router/blob/main/README.md)
- [FAQ 与验收边界](https://github.com/vllm-project/semantic-router/blob/main/website/docs/faq.md)
- [部署选项](https://github.com/vllm-project/semantic-router/blob/main/website/docs/installation/deployment-options.md)
- [Security hardening](https://github.com/vllm-project/semantic-router/blob/main/website/docs/installation/security-hardening.md)
- [SECURITY threat model](https://github.com/vllm-project/semantic-router/blob/main/SECURITY.md)
- [v0.4.0 Release](https://github.com/vllm-project/semantic-router/releases/tag/v0.4.0)
- [LICENSE](https://github.com/vllm-project/semantic-router/blob/main/LICENSE)
