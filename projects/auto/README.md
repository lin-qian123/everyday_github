<!-- markdownlint-disable MD013 -->

# auto

## 定位

`RightNow-AI/auto` 自称 “AGI compiler”，试图把 LLM agent 的重复行为记录、证明、抽取并编译成受能力约束的 WebAssembly 二进制。它关注的不是再做一个 agent，而是把 agent 已经学会且可重复的行为降成本、降延迟、可验证地固化。

## 用法

项目 README 描述了两类核心命令：

- `auto record`：附着到 live agent，记录 prompt、工具调用、参数和结果。
- `auto compile --contract`：把 trace 降到 typed IR，经过抽取、蒸馏、优化和 contract 验证，产出 `.cbin` cognition binary。

具体使用前应先阅读仓库中的 `spec/`、`paper/bench-results.md` 和 `docs/why-agi-compiler.md`，确认当前实现范围。

## 原理

Auto 的 runtime 分成两层：tier-1 是已编译的便宜 fast path，tier-0 是 frontier model interpreter。当 guard 判断输入新颖或越界时回退到 tier-0，捕获新 trace，再尝试重新编译。产物 `.cbin` 包含代码、小模型和 manifest，并声明 capability、eval、成本和延迟边界。

## 价值

- 把 agent 成本优化从 prompt 压缩推进到“记录、验证、编译”的系统路线。
- 用 WASM import confinement 表达能力边界，适合讨论 agent 安全沙箱。
- 对重复性客服、运维、数据处理和开发子任务有潜在降本意义。
- 其论文和 benchmark 文档为后续验证提供了明确入口。

## 风险边界

- “多数 agent cognition 是 symbolic” 是强主张，必须看具体 trace 和任务分布。
- guard 校准决定安全性；README 也指出 guard 过松会导致大量 silent wrong。
- 编译后 fast path 可能在分布变化时失效。
- 目前更像研究型基础设施，生产采用需要非常谨慎的 contract 和监控。

## 补充建议

- 优先在重复、低风险、有明确 contract 的任务上评估。
- 要求每个 `.cbin` 都保留 provenance、输入分布、eval 版本和 fallback 记录。
- 对比传统缓存、规则引擎、小模型蒸馏和 RPA，判断是否真的需要 compiler 复杂度。

## 参考资料

- GitHub: <https://github.com/RightNow-AI/auto>
- Paper: <https://arxiv.org/abs/2607.04542>
- RightNow AI: <https://www.rightnowai.co/>
