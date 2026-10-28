<!-- markdownlint-disable MD013 -->

# Prompt Engineering Interactive Tutorial

## 定位

这是 Anthropic 的交互式提示词教程，围绕 Claude 给出九章练习与附录，覆盖清晰指令、角色、数据与指令分隔、输出格式、示例和减少幻觉等内容。仓库分为 Anthropic 直连与 Amazon Bedrock 两条路线，适合用小实验学习提示设计。

2026-10-29 快照：Jupyter Notebook daily +94 stars；API 38,897 stars / 4,313 forks / 64 open issues（含 PR），license 字段为 null。主线 `0d277542e927`，本轮发行 API 为空。本文读取 README、入门 notebook、Bedrock 文档 / LICENSE 与完整文件树，未执行 notebook 或调用 API。

## 用法

1. 选定 `Anthropic 1P/` 或 `AmazonBedrock/`，从各自的 `00_Tutorial_How-To.ipynb` 顺序学习。
2. 直连入门 notebook 使用 anthropic SDK 和 Messages API；运行前核对当前可用模型、SDK 与计费，使用合成输入和预算。
3. 复制练习时以环境变量 / 秘密管理提供凭据，避免将真实 key 写入 notebook 并提交；每次运行后检查输出与保存状态。
4. 对同一组测试输入比较提示修改前后的结果，并保留失败例，而非只看一次输出。

上游原例把 `API_KEY` 与 `MODEL_NAME` 写在 notebook 中并执行 IPython `%store`。这是原例行为，复用时应先移除真实 key 的持久保存；只读教程内容无需 API key，交互调用则需要对应服务访问权限。

## 原理

每章先展示一个可调整的提示，再给练习与检查，引导学习者把输入结构、输出约束和少样本示例变为可比较变量。直连 helper 通过 `client.messages.create` 发出请求，返回文本；temperature 设为 0 也不能作为跨模型、跨时间完全确定的保证。

## 价值

- 将抽象提示技巧转成可修改的 notebook 单元，适合入门教学。
- 便于建立提示回归集，观察格式错误、拒答、幻觉与迁移差异。
- 两种服务路线有助于理解 SDK、访问控制与部署入口的区别。

## 风险边界

- README 与初始配置仍以 **Claude 3 Haiku / 2024-03-07 model ID** 为例，并含当时的模型排序。它们是历史课程语境，本页不据此推荐当前型号或保证该 ID 可调用。
- API 输入和练习内容会发往所选服务；敏感数据、成本、速率限制与 AWS 权限须自行控制。
- 角色、XML 分隔、输出格式和“减少幻觉”技巧不能保证事实正确，也不形成提示注入安全边界；应以可信检索、权限与独立判分配套。
- 根目录及完整树未见覆盖整库的根 LICENSE；`AmazonBedrock/LICENSE` 为 **MIT No Attribution**。API license null 不等于整库 MIT，也不能把子目录文本自动扩展到 Anthropic 1P 内容。
- notebook 的保存输出及 IPython store 可能保留凭据 / 数据；运行前后应检查本机状态。

## 补充建议

把旧模型示例迁移到实际可用的固定模型后，先重建基线，再比较修改收益。记录模型 ID、日期、token、费用、输入集与判分规则，区分课程题正确率与业务任务效果。教学再分发前核清各部分许可。

## 参考资料

- [上游仓库](https://github.com/anthropics/prompt-eng-interactive-tutorial)、[GitHub API](https://api.github.com/repos/anthropics/prompt-eng-interactive-tutorial)。
- [固定 README：课程与历史模型说明](https://github.com/anthropics/prompt-eng-interactive-tutorial/blob/0d277542e927652da25b0014c9b346723af55881/README.md)。
- [直连入门：API、模型与持久变量](https://github.com/anthropics/prompt-eng-interactive-tutorial/blob/0d277542e927652da25b0014c9b346723af55881/Anthropic%201P/00_Tutorial_How-To.ipynb)。
- [Bedrock 路线](https://github.com/anthropics/prompt-eng-interactive-tutorial/blob/0d277542e927652da25b0014c9b346723af55881/AmazonBedrock/README.md)、[子目录 MIT No Attribution](https://github.com/anthropics/prompt-eng-interactive-tutorial/blob/0d277542e927652da25b0014c9b346723af55881/AmazonBedrock/LICENSE)。
