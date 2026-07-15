<!-- markdownlint-disable MD013 -->

# tura

## 定位

`Tura-AI/tura` 是一个本地开源 coding agent，主打长任务中的 token、轮次和上下文效率。项目 README 公开宣称在 DeepSWE 与 rewrite benchmark 上，相比 Codex CLI 配置减少大量 turn / token，并提升 verifier success rate。

## 用法

项目提供官网、npm 包和本地 GUI/TUI 入口。使用前建议先阅读：

- 官方 benchmark: <https://turaai.net/benchmark>
- GitHub benchmark 记录: <https://github.com/Tura-AI/benchmark/blob/main/doc/current-test-set-record.md>
- 仓库 roadmap 与 known issues。

因为它是 coding agent，真实使用前应在隔离仓库或 disposable worktree 中验证权限、diff、测试和回滚流程。

## 原理

Tura 的核心思路是减少重复上下文和模型往返。README 将其与传统 tool-calling loop 对比，强调 macro CLI command run、多 session 并发、HTML rich text GUI/TUI 和 benchmark artifact 归档。它把节省下来的预算用于两种模式：Direct 偏成本，Balanced 把部分预算再投入推理、调查和验证。

## 价值

- 切中当前 coding agent 的关键痛点：长任务轮次多、上下文重复、token 成本高。
- 公布 benchmark artifact 和已知证据缺口，比只给宣传数字更可审查。
- 对团队评估 agent harness 的“成本 / 成功率 / 证据”三角很有参考价值。
- Rust 实现和本地优先路线适合关注可控工具链的开发者。

## 风险边界

- GitHub 星标仍很低，生态和第三方复测不足。
- benchmark 数字来自项目方，需要独立复现。
- README 中的 Codex CLI / GPT-5.6 对比依赖特定时间点、模型和配置。
- coding agent 具备改代码和运行命令能力，必须明确 sandbox、权限和审查边界。

## 补充建议

- 先在一组内部历史 bugfix 上复跑，比较成功率、成本、耗时和 diff 质量。
- 不只看 pass rate，还要看失败时是否可诊断、是否过度修改、是否留下证据。
- 跟踪其跨 OS、跨 provider、本地模型和 UI latency 的后续测量。

## 参考资料

- GitHub: <https://github.com/Tura-AI/tura>
- Website: <https://turaai.net/>
- Benchmark: <https://turaai.net/benchmark>
- Benchmark record: <https://github.com/Tura-AI/benchmark/blob/main/doc/current-test-set-record.md>
