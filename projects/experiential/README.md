<!-- markdownlint-disable MD013 -->

# experiential（experientiallabs/experiential）

> 记录日期：2026-09-07（Asia/Shanghai）。本页依据上游 README、SETUP、release、LICENSE 与 GitHub REST API 做静态整理；本轮未安装网关、未连接 provider key、未上传 trace，也未复现路由质量、成本或延迟。

## 定位

`experiential` 是面向 agent workflows 的开源 LLM gateway 与 router，通过 OpenAI-compatible / Anthropic Messages 接口统一 hosted、BYOK 和本地模型，并用身份、用途与预算约束调用。上游还提供从 production traces 构建项目路由器或优化自有模型的路径。

2026-09-07 的 GitHub 官方 Python Trending 抓取显示约 `+568 stars today`；REST API 快照为 `1,921 stars / 103 forks / 32 open issues`，最新 release 为 `v0.7.44`，许可证为 Apache-2.0。

## 用法

本地快速入口会启动 loopback gateway，并在首次运行保存所选 provider 连接、公开 alias、identity 和命令预算：

```bash
pip install experiential
exp
```

获得一次性 key 后可调用本地 `/v1/chat/completions`。评估时应使用测试 provider、低额度 key 和合成 trace；不要直接上传含代码、用户消息、路径或 secrets 的生产轨迹。

## 原理

- **协议网关**：把多个 provider 暴露为统一 OpenAI-compatible 与 Anthropic Messages 接口。
- **身份和预算**：为用户/agent、用途、模型与支出设置控制面，入口默认展示 `$50.00` command budget。
- **项目路由器**：读取 OpenTelemetry traces，模拟和优化质量、速度与成本权衡，再作为一个公开 alias 使用。
- **本地与托管双路径**：本地 data plane 在 loopback 提供服务；托管平台可接收 BYOK key、usage 与 traces。
- **模型优化**：上游给出从路由器 traffic 到使用 Tinker 微调自有开源模型的流程。
- **产品 telemetry**：README 说明匿名 PostHog 聚合 telemetry 默认开启，并提供 status/disable/enable 命令。

## 价值

- 统一端点可减少 agent 客户端针对每个 provider 重写适配器。
- 身份、模型和预算策略为多 agent 成本治理提供集中检查表面。
- 用真实 trace 建路由器，有机会把模型选择从静态别名变成任务相关决策。
- Apache-2.0 代码与本地 data plane 便于静态审计和原型集成。

## 风险边界

- 网关会集中 provider keys、prompts、traces、身份和费用权限；一处误配或被攻破会扩大跨 provider 的 blast radius。
- “优化质量、速度和成本”是上游能力描述；效果依赖 trace 代表性、评分器、模型版本、价格、缓存和失败处理。
- production traces 可能含源码、个人数据、工具输出和 secrets；上传托管平台前必须做字段级最小化、脱敏和保留期审查。
- PostHog telemetry 虽声明不含原始内容，仍默认开启；本轮未抓包验证实际字段、错误路径或第三方 SDK 行为。
- 公开 alias 可能隐藏底层模型变化；合规、数据驻留、许可和用户告知不能只依据 alias 名称。
- 预算上限不自动解决并发竞态、重试、长上下文、跨腿调用或 provider 账单延迟，应独立做账单对账和 hard stop。

## 补充建议

- 用专用低额度 provider key、allowlist 模型和 loopback-only 网络先做 smoke test；不要复用生产管理员 key。
- 默认关闭产品 telemetry，抓包确认无额外外发后再按组织政策决定是否开启。
- 对 trace 定义 schema 和脱敏测试，剔除 prompt、工具 payload、路径、代码、个人信息与 credentials。
- 以固定任务集比较直连、静态路由和自适应路由，同时统计成功率、完整费用、P50/P95 延迟、retry 与 fallback。
- 为 alias 保存底层 provider/model/revision、路由决策和每条 workflow leg 的账单记录，支持审计与回滚。

## 参考资料

- [GitHub 仓库](https://github.com/experientiallabs/experiential)
- [GitHub REST API](https://api.github.com/repos/experientiallabs/experiential)
- [v0.7.44 Release](https://github.com/experientiallabs/experiential/releases/tag/v0.7.44)
- [SETUP 指南](https://github.com/experientiallabs/experiential/blob/main/SETUP.md)
- [README Telemetry 说明](https://github.com/experientiallabs/experiential#telemetry)
- [Apache-2.0 License](https://github.com/experientiallabs/experiential/blob/main/LICENSE)
