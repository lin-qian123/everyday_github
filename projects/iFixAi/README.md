<!-- markdownlint-disable MD013 -->

# iFixAi（ifixai-ai/iFixAi）

> 上游仓库：<https://github.com/ifixai-ai/iFixAi> · 归类：Agent 框架与技能生态 · 本页基于 2026-10-01 的 GitHub API、README、methodology、reproducibility、Security Policy、Release 与 LICENSE 静态整理，未连接真实 Agent、购买 judge 调用或复跑 60 项检查。

- 抓取快照：17,354 stars、1,361 forks、23 open issues。
- 热度信号：GitHub Python Trending 抓取时约 +250 当日 stars。
- 版本与许可：Apache-2.0；latest Release 与 tag 均为 `v4.0.0`。

## 定位

iFixAi 是面向 AI Agent 治理行为的诊断工具，用固定检查与 fixture 观察 Agent 是否遵守业务规则、组织结构和预期职责。它支持 CLI、Claude Code / Codex plugin 及多宿主 skill，可测试模型 API、OpenAI-compatible HTTP endpoint 或自定义 adapter，并输出 JSON、Markdown 和 A--F scorecard。

## 用法

可安装 `ifixai[provider]`，运行 `ifixai setup` 与 `ifixai run`；无密钥的 mock 路径用于验证流程，默认 fixture 故意含缺陷，不能拿其分数评价自己的 Agent。可通过 `--provider http --endpoint ... --grounding sut` 对真实部署做观察，或安装 plugin / scaffolded skill 让 Agent 协助生成 fixture、估算费用并解释报告。

## 原理

60 项检查分为 32 个 core 与 28 个 extended；证据路径包括结构化 capability 调用、按公开 YAML rubric 的 judge 评分与 atomic-claims 核对。最终字母等级只由五个 core pillar 加权形成，并带 mandatory minimum；跨 provider judge 是推荐路径，自评会显式标记偏差。每次运行记录 fixture digest、judge / rubric 版本和 nonce，便于追踪输入，但 live LLM 本身不保证字节级复现。

## 价值

它将“Agent 看起来能工作”拆成固定问题、证据和报告，适合在版本、prompt、tool 或治理规则变更后做回归。独立 judge、`insufficient_evidence` 状态和 manifest 能减少把缺少证据误写为通过的风险，也便于团队讨论哪些规则只是声明、哪些真正被观测。

## 风险边界

- 官方方法明确这是 diagnostic，不是认证；通过公开对抗集不能证明能抵抗有动机攻击者。
- 某些治理 hook 来自 fixture 声明而非运行时实测；不同 fixture、release、judge 集合的分数不可直接横比。
- live LLM 评分不确定，跨 provider 也不消除 judge 偏差、污染、供应商变化或提示敏感性。
- scorecard 与中断 checkpoint 会保存完整模型输入输出，可能含敏感内容；不能随意上传到 pastebin、diagram 或 issue。
- provider 与 judge 调用会产生费用和外发，README 的成本只是项目方估算，本轮未核账。
- 默认发送有限伪匿名 telemetry，首次披露、CI 自动关闭，可用 `IFIXAI_TELEMETRY=0` 或 `DO_NOT_TRACK=1` 退出；上游说明事件无限期保留。

## 补充建议

先用 mock 证明流程，再用自有脱敏 fixture 和固定 Agent endpoint；把版本、fixture digest、judge、模型、nonce 和原始报告一并归档。关键结论至少重复运行并人工抽查失败样例，将高后果规则改造成结构化 / 确定性检查。共享报告前扫描 prompt、回复、路径、凭据与业务数据，并在预算上限内隔离 SUT 与 judge。

## 参考资料

- [GitHub 仓库](https://github.com/ifixai-ai/iFixAi)
- [GitHub REST API](https://api.github.com/repos/ifixai-ai/iFixAi)
- [README](https://github.com/ifixai-ai/iFixAi/blob/main/README.md)
- [Methodology](https://github.com/ifixai-ai/iFixAi/blob/main/docs/methodology.md)
- [Reproducibility](https://github.com/ifixai-ai/iFixAi/blob/main/docs/reproducibility.md)
- [Security Policy 与 telemetry 说明](https://github.com/ifixai-ai/iFixAi/blob/main/SECURITY.md)
- [v4.0.0 Release](https://github.com/ifixai-ai/iFixAi/releases/tag/v4.0.0)
- [LICENSE](https://github.com/ifixai-ai/iFixAi/blob/main/LICENSE)
