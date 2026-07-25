# Verchestra

## 定位

`Verchestra` 是一个面向 AI 软件交付的可验证 harness：将发现、规划、实现、验证与人工批准打包成可移植、可签名、可复核的交付过程。截至 2026-07-26，仓库创建于 2026-07-25，约 4 stars、0 forks，版本为 `0.0.0-qualification`，尚未提供公开安装器或发行包，许可证为 GPL-3.0-only。

## 用法

当前只适合贡献者在源码树中评估：克隆仓库后，使用 Node 24.14.0 与 pnpm 10.34.5，执行 `pnpm install --frozen-lockfile` 和 `pnpm gate:quick`。文档站可通过 `pnpm site:dev` 启动；完整站点检查涉及 Playwright 浏览器、可访问性和 Lighthouse，不应把开发命令误当成生产安装方式。

## 原理

项目将 execution package、策略、审批、租约、外联规则、只读数据 probe、证据 digest 和交接报告连成一条链。合格的 Claude Code、Codex、OpenCode/Qwen 环境可以恢复包，但执行前应重建本地权限并运行声明的 gate；关键结论以签名证据而非会话断言为依据。

## 价值

- 把 agent 交付从“聊天记录可用”提升为可移植、可审查的工程产物。
- 把外部影响前的 policy gate 和人工批准显式化，适合受控环境探索。
- 只读探针与证据摘要有助于降低数据库发现阶段的不可审计性。

## 风险边界

- 仍在 qualification 阶段，API、工作流和信任模型均可能快速变动。
- 签名、gate 与证据不能自动保证需求正确、数据无误或审批人判断可靠。
- GPL-3.0-only 可能影响与专有交付工具的组合方式；跨 agent 兼容也需实测。

## 补充建议

从无生产权限的样例仓库开始，刻意制造策略拒绝、失效 lease 和不匹配 digest，验证系统是否真的拒绝执行。将每个 gate 绑定到可重复命令，并由独立 reviewer 复核证据来源。

## 参考资料

- GitHub：<https://github.com/accd/verchestra>
- 项目文档：<https://accd.github.io/verchestra/>
- 架构说明：<https://github.com/accd/verchestra/blob/main/docs/architecture.md>
