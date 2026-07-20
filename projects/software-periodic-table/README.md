<!-- markdownlint-disable MD013 -->

# software-periodic-table

## 定位

`software-periodic-table` 是一个面向 LLM coding agent 的“软件元素周期表”：把常见业务软件拆成 115 个可复用元素，覆盖对象、属性、动作、界面、智能能力和规则，并提供 TypeScript reference implementation、composition prompt 和评测框架。

## 今日信号

- GitHub：<https://github.com/NullLabTests/software-periodic-table>
- 创建时间：2026-07-19。
- 抓取时约 68 stars、4 forks。
- 语言 / 许可证：TypeScript，MIT。
- Topics：`ai-agents`、`llm`、`typescript`。

## 用法

项目的 canonical source 是 `ontology/periodic-table.json`。coding agent 可通过系统提示和 plan schema 先检索 / 选择元素，再组合为业务应用结构。仓库还包含示例、验证脚本和 eval runner，用来比较“每次重新生成”与“复用元素组合”的 token 成本、结构一致性和正确性。

## 原理

核心假设是：多数业务软件并非从零发明，而是由稳定的 nouns、fields、verbs、views、AI primitives 和 governance rules 组合而成。把这些元素结构化为可检索、可类型检查、可评估的库，可以缩小 agent 搜索空间，减少漂移和重复 token 消耗。

## 价值

- 把 agent 应用生成从 prompt 技巧推进到 ontology / composition layer。
- 对企业 CRUD、内部工具、仪表盘、审批流等场景有潜在复用价值。
- 评测框架如果完善，可以为“模板化是否真的提升 agent 产出质量”提供证据。

## 风险边界

- 115 个元素是否足够覆盖真实软件，仍需要跨行业案例验证。
- 元素组合可能提高一致性，但也可能限制设计空间，导致 agent 过早套模板。
- 当前更像研究 / 方法论仓库，生产级代码生成、权限模型和 UI 适配仍需外部工程补齐。

## 补充建议

- 后续观察是否出现真实业务应用案例和第三方评测。
- 可与 `design-md`、`agent-native`、`fable-method`、`loop-engineering` 结合：前者约束视觉/产品，后者约束执行流程，本项目约束业务对象组合。

## 参考资料

- GitHub 仓库：<https://github.com/NullLabTests/software-periodic-table>
- README：<https://github.com/NullLabTests/software-periodic-table#readme>
- Agent 使用文档：<https://github.com/NullLabTests/software-periodic-table/blob/main/docs/AGENT_USAGE.md>
