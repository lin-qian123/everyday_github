<!-- markdownlint-disable MD013 MD034 -->

# Weave Router：按请求动作选择模型的 Agent 推理网关

> 上游仓库：https://github.com/weave-os/router · 归类：模型、训练与推理基础设施 · 本页基于 2026-09-19 的 README、benchmark harness、语义 / 部署文档、LICENSE 与 REST API 静态整理；未部署路由器、调用 hosted service 或复跑付费 benchmark。

## 定位

Weave Router 是兼容 Anthropic Messages、OpenAI Chat Completions 与 Gemini API 的模型路由网关。它用本地 embedding / cluster scorer 或可选 HMM policy 针对每个 upstream action 选择模型，并面向 Claude Code、Codex、Cursor、OpenCode、Pi 和自建应用暴露一个统一 endpoint。核心卖点是成本、质量与延迟之间的动态取舍，而不是单纯的协议转发。

2026-09-19 的 GitHub 官方 Go Trending 抓取显示约 `+31 stars today`；REST API 快照为 `4,464 stars / 123 forks / 126 open issues`。GitHub API 未识别标准 SPDX，根 LICENSE 为 Elastic License 2.0；当前无 GitHub Release，README 的 npm 固定示例为 `@weave-os/router@0.1.0`。

## 用法

最快入口会连接 hosted Weave Router 并修改所选 Agent 配置：

```sh
npx @weave-os/router --codex
```

自托管模式需要 provider key、强 dashboard password、Postgres 与 router 服务：

```sh
git clone https://github.com/weave-os/router.git
cd router
echo "OPENROUTER_API_KEY=..." >> .env.local
echo "ROUTER_ADMIN_PASSWORD=..." >> .env.local
make up
```

可用 `--scope project`、`--local`、自定义 base URL 与明确 npm 版本控制写入范围和供应链漂移。

## 原理

- router 在每次 action 上生成 embedding 并用 cluster scorer 选择候选模型；可选 HMM sidecar 使用冻结 artifact 与显式 roster。
- API translation 层接受 Anthropic、OpenAI 与 Gemini 请求，并把流式响应、tool、vision 与 usage 映射到对应 provider。
- 自托管时 router、scorer、Postgres 与 provider key 留在本机；prompt 仍直接发往被选中的外部 provider，OTLP 也可能发往配置的 collector。
- provider key 加密后存储，客户端使用另一类 `rk_` router key；两种密钥的用途和泄露影响不同。
- dashboard 与 analytics 记录 route decision、usage 和 cost；流式请求的最终费用通过响应事件而非已发出的 HTTP header 返回。
- 仓库含可复现 Codex benchmark harness，锁定任务、Harbor / Codex 版本、manifest 和统计方法，并公开报告多个对照中 router 有胜、有负、有统计意义不足的情况。

## 价值

- 让应用和 Coding Agent 使用一个 endpoint，而无需在每个客户端手写 provider 路由、协议转换与成本汇总。
- action 级选择比整段会话锁死单模型更细，可把简单动作送往低成本模型，把复杂任务送往高能力模型。
- 自托管数据流、健康检查、route-only endpoint、OTLP 与 analytics export 便于做治理和可观测性。
- benchmark 文档公开 pins、费用口径、置信区间和 caveats，适合独立复跑而不是只引用营销百分比。

## 风险边界

- `npx` 安装器会改写 Claude Code、Codex、OpenCode 或 Pi 配置；hosted 路径会获得 router key 并把请求经过 Weave 服务，不能与自托管数据流混为一谈。
- 自托管只保证 router 控制面在本机，prompt 仍会发给 OpenAI、Anthropic、Gemini、OpenRouter 或自定义 endpoint；OTLP 和 dashboard 还可能保存敏感 trace。
- “降低 40–70% 成本”“<50ms”等主张需按启用模型、缓存、任务和价格复跑。公开结果中 router 对某些对照胜出，对 Sol / Astra 或 OpenRouter 的若干比较则更差或统计上近似持平。
- benchmark 的 router-billed、list 与 OpenRouter-billed 是不同费用口径；缓存写入、analytics 权限、provider 拒绝和 Harbor 环境失败都会影响结论。
- ELv2 允许使用和修改，但限制把软件作为托管服务提供等行为；企业二次分发和商业托管前需法律审查。
- 本页未验证密钥加密、租户隔离、模型目录更新、fallback、tool / vision parity、延迟或质量回归。

## 补充建议

1. 从 `--dry-run`、smoke task 与 route-only endpoint 开始，冻结候选模型、价格、缓存和数据集，再比较 direct、forced-model 与 routed 三条路径。
2. 将 prompt / tool trace 视为敏感数据，对 Postgres、OTLP、analytics、dashboard 与 backup 分别设置访问、脱敏、保留和删除策略。
3. 把 router key 与 upstream provider key 分开轮换；只在本地或受控网络暴露管理接口，并固定 npm、镜像与 HMM artifact digest。
4. 选型报告同时给 pass rate、置信区间、费用、wall time、拒绝和环境失败，不把单个 headline savings 外推到生产任务。

## 参考资料

- 上游 README：https://github.com/weave-os/router
- Benchmark harness：https://github.com/weave-os/router/blob/main/bench/README.md
- Router 语义：https://github.com/weave-os/router/blob/main/docs/SEMANTICS.md
- Analytics export：https://github.com/weave-os/router/blob/main/docs/ANALYTICS_EXPORT.md
- GitHub REST API：https://api.github.com/repos/weave-os/router
- LICENSE：https://github.com/weave-os/router/blob/main/LICENSE
