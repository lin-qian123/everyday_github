<!-- markdownlint-disable MD013 -->

# ai-smart-contract-auditor（AuditSentry）

- 仓库：[iktok90-design/ai-smart-contract-auditor](https://github.com/iktok90-design/ai-smart-contract-auditor)
- 快照：2026-08-11 抓取；GitHub API 显示其创建于 2026-08-10，约 75 stars、2 forks，MIT。数字会随时间变化。
- 分类：Coding Agents 与终端助手

## 定位

一个面向 Solidity、Vyper 和 EVM 合约的 Claude Code 本地审计技能包。项目将多类安全分析、PoC 生成、fork 模拟和报告产物编排到 MCP 工具与 slash commands 中；它是安全研究/审计辅助工具，不是能替代人工审计的认证产品。

## 用法

需 Node.js 18+、Git 和 `make`。克隆后执行 `make build`，再以 `make audit-demo` 运行自带脆弱合约示例；项目还提供本地 Claude Code skill 安装路径。真实目标合约的审计、mainnet fork 或链上查询前，应先在隔离钱包、测试 RPC 和明确预算下配置所需工具。

## 原理

README 描述了 23 个分工 agent 与 13 个 MCP 服务：静态/符号分析、Foundry/Hardhat、fuzz、历史发现检索、区块浏览器和 fork 模拟等为模型提供证据与执行面。结果经去重、评分和报告生成输出；这种组合可扩大检查面，但 LLM 推理、工具配置、数据源和验证规则都会影响结论。

## 价值

把“发现假设—复现 PoC—回归测试—报告”连成显式工作流，适合用作审计前的结构化辅助、已知漏洞的教育样例或变更审查的第二意见。相比只让模型读合约，外部工具至少为部分断言提供了可执行的复核路径。

## 风险边界

项目声称的基准、历史发现覆盖和检出率目前主要是仓库自述，尚未在本轮独立复现；不能据此推断遗漏率或审计质量。fork、RPC、私钥、合约源码和生成的交易都可能造成费用、数据泄露或误操作；未经人工复核的 PoC、风险评级和“安全”结论不可用于上线或资产决策。

## 补充建议

先用无资产测试地址和固定区块 fork 复跑最小示例，再将每条发现回归到独立的单元/不变量测试。锁定 MCP 依赖版本和 RPC 权限，禁止 agent 使用生产私钥或直接广播交易；高价值协议仍应采用独立人工审计、形式化/静态分析和漏洞响应流程。

## 参考资料

- [项目 README 与源码](https://github.com/iktok90-design/ai-smart-contract-auditor)
- [GitHub API 元数据快照](https://api.github.com/repos/iktok90-design/ai-smart-contract-auditor)
