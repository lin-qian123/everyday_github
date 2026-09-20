<!-- markdownlint-disable MD013 MD034 -->

# awesome-free-llm-apis：带免费层的 LLM API 可核对清单

> 上游仓库：https://github.com/mnfst/awesome-free-llm-apis · 归类：模型、训练与推理基础设施 · 本页基于 2026-09-21 的 README、`data.json`、contributing、许可证与 REST API 静态整理；未注册任何 provider、创建 API key、调用模型或复核所有限额。

## 定位

`awesome-free-llm-apis` 是模型提供商与第三方 inference provider 的免费层目录，记录 API key 入口、base URL、模型、context、输出长度、modality 和 rate limit。它是动态采购 / 试用线索，不是统一 gateway、SLA、模型质量评测或“永久免费”保证。

2026-09-21 的 GitHub 官方 JavaScript Trending 抓取显示约 `+138 stars today`；REST API 快照为 `7,944 stars / 759 forks / 17 open issues`，CC0-1.0，无 GitHub Release；默认分支最新 push 为 2026-08-21。

## 用法

使用时先按用途和区域筛选 provider，再回到每家官方 pricing、quota、data use、terms 与 deprecation 页面复核。README 称多数 endpoint 兼容 OpenAI SDK，但明确有例外，因此不能只替换 `base_url` 就假设 authentication、model name、streaming、tool call 与 error semantics 全部一致。

建议把清单复制为内部、带核验日期的 provider matrix，至少记录：

- 免费资格、信用卡 / 实名要求、RPM / RPD / TPM、并发和 reset 周期；
- prompt / output 是否用于训练、日志保留、地域与商业用途限制；
- model ID、context、tool / vision 支持、deprecation 和 fallback 行为；
- 预算上限、key 作用域、可撤销性、可靠性与错误率。

## 原理

- README 按 model owner 与 inference host 分组，将公开 quota / model metadata 组织为表格。
- `data.json` 提供结构化数据，仓库内 `.verify` / scripts 用于维护和核对条目。
- contribution 规则要求给出 provider、endpoint、rate limit、官方文档与代表模型，并排除一次性 trial credit / 限时促销。
- 项目同时链接 `manifest.build`，但目录内容与外部产品能力、服务条款和运行可靠性应分开判断。

## 价值

- 为原型、教学、低频评测快速建立候选集合，减少逐家发现入口的时间。
- 把 rate limit、context、modality 和数据使用提示放在同一视图，便于初步比较。
- 结构化 `data.json` 可接入内部检查器，定期发现失效 model、quota 和 URL。
- contribution contract 比无来源的“免费 API 大全”更易审计，但仍依赖维护时效。

## 风险边界

- 免费层、模型名、context、限额、区域和数据政策都可能随时变化；仓库 title 中的 permanent 不能作为合同承诺。
- 免费服务可能用 prompt 改进产品、限制商业用途、要求实名、记录内容或在额度耗尽后降级；必须回到官方条款。
- OpenAI-compatible 只描述部分接口形状，不证明 tool calling、streaming、token accounting、moderation 或错误语义一致。
- 目录没有对模型质量、隐私、安全、availability 或 provider 身份作全面保证；也不应把 API key 放入前端或公开仓库。
- CC0-1.0 适用于目录内容，不自动覆盖 provider 文档、模型权重、输出和服务条款。

## 补充建议

1. 为每个候选记录 `verified_at` 与官方 source URL，自动提醒 14--30 天复核，不沿用陈旧额度。
2. 使用合成、无敏感数据的固定 probe 测 authentication、streaming、tool call、latency、error、quota 与账单边界。
3. key 使用独立 project、最低 quota、server-side secret store 和可撤销 scope；默认禁止把科研 / 客户原文送入免费层。
4. 生产系统至少准备付费 SLA / self-hosted fallback，并把模型退役、免费层取消和协议差异纳入演练。

## 参考资料

- 上游 README：https://github.com/mnfst/awesome-free-llm-apis
- 结构化数据：https://github.com/mnfst/awesome-free-llm-apis/blob/main/data.json
- 贡献规则：https://github.com/mnfst/awesome-free-llm-apis/blob/main/contributing.md
- GitHub REST API：https://api.github.com/repos/mnfst/awesome-free-llm-apis
- LICENSE：https://github.com/mnfst/awesome-free-llm-apis/blob/main/license
