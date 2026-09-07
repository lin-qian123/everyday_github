<!-- markdownlint-disable MD013 MD034 -->

# claude-ads（AgriciDaniel/claude-ads）

> 记录日期：2026-09-08（Asia/Shanghai）。本页依据上游 README、control-plane 文档、release、LICENSE 与 GitHub REST API 做静态整理；本轮未安装 skill、未导入广告账户、未运行 audit，也未验证 scoring、平台覆盖或写入 gate。

## 定位

`claude-ads` 是面向 Claude Code 的 paid-media operations skill / 工具集，覆盖 Google、Meta、YouTube、LinkedIn、TikTok、Microsoft、Apple、Amazon、Reddit、Pinterest、Snapchat 与 X 等 12 个广告平台。它强调从授权 export 或只读 account read 生成审计、计划、创意工作流、实验、监控和版本化报告，并把账户修改放在额外 capability gate 后。

2026-09-08 的 GitHub Python Trending 抓取显示约 `+94 stars today`；REST API 快照为 `8,981 stars / 1,339 forks / 39 open issues`，最新 release 为 `v2.0.1`（2026-07-13），许可证为 MIT。

## 用法

上游提供 skill 安装与仓库方式。风险最低的起点是克隆固定 release，仅用脱敏 export 做只读分析：

```bash
git clone --branch v2.0.1 https://github.com/AgriciDaniel/claude-ads.git
cd claude-ads
```

正式接账户前，应先阅读 `control-plane/` 的 claims、capabilities、privacy、release requirements 和 publishing policy，确认目标平台 adapter 真实存在、当前且有 fixture / test。不要因一句自然语言要求就启用写账户能力。

## 原理

- **Conductor + bounded workers**：主协调器持有 scope、policy、聚合与最终 artifact，各 worker 只分析限定切片。
- **统一结果契约**：先生成版本化 JSON bundle，再从同一数据渲染 Markdown、HTML 与 PDF，减少不同报告口径漂移。
- **证据覆盖与健康分离**：控制项为 `pass/fail/unknown/not_applicable`；未知会降低 evidence coverage，但不会被偷偷算作健康失败或通过。
- **部分失败显式化**：required worker 失败时整轮标记 partial；失败平台不进入 portfolio score。
- **账户变更门**：精确 account/object ID、before/after diff、blast radius、owner approval、ceiling、idempotency、audit、rollback、verification window 和远端 precondition 缺一不可。
- **公开 control plane**：用日期来源、声明、capability 与 release 条件约束“文档里说支持”和“代码可安全执行”之间的距离。

## 价值

- 将跨平台广告审计的证据结构、缺失数据和输出格式标准化，而不是让模型自由生成一份看似完整的报告。
- 默认只读、未知项不混入健康分、失败不冒充完成，适合作为高后果自动化的治理模板。
- 同一 JSON 派生多种报告，有利于 diff、归档与后续复算。
- 把 mutation 前置条件写成可检查 contract，比仅在 prompt 中写“请小心”更具工程价值。

## 风险边界

- 12 平台覆盖是上游声明；平台 API、归因窗口、政策和可用字段变化频繁，当前 adapter 与测试覆盖必须逐项核验。
- deterministic score 只保证给定规则下可重复，不保证商业目标、因果关系、创意质量或预算分配正确。
- 广告 export、受众、转化、搜索词、创意和账户 transcript 可能含客户、个人与商业敏感数据。
- “read-only by default”不表示永远不能写。若 capability 被启用，agent 仍可能改预算、状态或投放对象，必须由外部审批和额度系统兜底。
- 上游规则不能替代 Google/Meta 等平台条款、隐私同意、政治广告、歧视、地域和行业监管审查。
- 本轮没有复现 score、partial run、rollback 或 remote precondition；不能把 README 的安全设计写成已证明的账户保护。

## 补充建议

- 先用固定导出做离线回放，手工核对 20–30 个控制项的来源、unknown 处理、分母和跨平台聚合。
- 写入测试只连接沙箱 / 测试账户并设置极低 ceiling，故意制造并发修改、超时、重复请求与 rollback 失败。
- 将平台 schema、政策和来源日期纳入 CI；任何 adapter 无 fixture / test 或来源过期时强制降级为只读 / 不支持。
- 对客户数据设最小字段、脱敏、保留期和禁止入 Git / transcript 的技术检查，而不只依赖文档约定。

## 参考资料

- GitHub 仓库：https://github.com/AgriciDaniel/claude-ads
- GitHub REST API：https://api.github.com/repos/AgriciDaniel/claude-ads
- 最新 release：https://github.com/AgriciDaniel/claude-ads/releases/tag/v2.0.1
- Account safety：https://github.com/AgriciDaniel/claude-ads#account-safety
- Scoring and evidence：https://github.com/AgriciDaniel/claude-ads#scoring-and-evidence
- LICENSE：https://github.com/AgriciDaniel/claude-ads/blob/main/LICENSE
