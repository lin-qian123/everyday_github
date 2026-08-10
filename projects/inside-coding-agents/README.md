<!-- markdownlint-disable MD013 -->

# inside-coding-agents

- 仓库：[vpromise/inside-coding-agents](https://github.com/vpromise/inside-coding-agents)
- 快照：2026-08-11 抓取；GitHub API 显示其创建于 2026-08-10，约 8 stars、0 forks，Apache-2.0。数字会随时间变化。
- 分类：Agent 框架与技能生态

## 定位

一个双语、可视化的 coding-agent 与 agent-harness 教材、架构图谱和实验库。它试图把 tool calling、上下文、权限、沙箱、子 agent、协议和 trace 等机制，与“已验证事实/解释/可复现实验”分开保存。

## 用法

教学与实验依 README 需要 Python 3.12+、Node.js 22.13+；可先创建虚拟环境、安装 `requirements-dev.txt`，运行课程 demo、固定实验检查和 registry 校验。网站开发另在 `apps/web` 执行 `npm ci` 和 `npm run dev`；完整质量门包含单测、schema/trace 校验和浏览器测试，适合按需选择而非首次全部运行。

## 原理

项目以版本化 agent snapshot、Claim/Evidence 记录和可运行 trace 管理知识：厂商架构主张需链接到审阅过的证据，参考 harness 的行为则由确定性实验和报告支撑。它不直接复刻或认证任一产品，而是提供可比较的机制层和干净实现。

## 价值

对于要设计、评估或教学 coding agent 的团队，这种“机制—来源—实验”三层组织有助于避免把产品营销、个人推断和可复现观察混为一谈。其零模型调用的示例也便于在不暴露 API key 的条件下学习 agent loop。

## 风险边界

项目自称的快照、实验和产品比较仍受版本、平台与维护节奏限制；它不是厂商官方文档、性能基准或安全认证。运行完整 web/浏览器质量门会下载依赖和浏览器，需在受控网络与磁盘预算内执行；产品行为应以当期官方文档和本地复测为准。

## 补充建议

先运行一个确定性 lesson 与一个 `--check` 实验，检查输出、trace 和证据链接的可重复性。使用其图谱前记录 snapshot 日期和待验证空白；若据此修改本团队 harness，仍要在自身权限、网络和真实任务集上独立验收。

## 参考资料

- [项目 README、实验与在线站点](https://github.com/vpromise/inside-coding-agents)
- [GitHub API 元数据快照](https://api.github.com/repos/vpromise/inside-coding-agents)
