<!-- markdownlint-disable MD013 -->

# Cloudflare OS（cloudflare/cloudflare-os）

> 上游仓库：<https://github.com/cloudflare/cloudflare-os> · 归类：办公、商业与行业应用 · 本页基于 2026-10-04 的 GitHub API、README、sharing / blueprint / OAuth / public-server 文档、manifest 与 LICENSE 静态整理，未部署 Workers / workerd、连接企业数据、运行 Agent、创建 Gadget 或复测隔离。

- 抓取快照：10,549 stars、1,283 forks、128 open issues。
- 热度信号：GitHub 综合 / TypeScript Trending 抓取时约 +84 当日 stars。
- 版本与许可：Apache-2.0；无 GitHub Release / tag，根 manifest 为 `1.0.0`，README 将 2026 年 8 月后的 v2 标为 Early Access。

## 定位

Cloudflare OS 是面向组织 AI 生产力的 Agent 工作区，不是传统操作系统。它将企业上下文聊天、AI 生成的个人应用（Gadget）、实时协作和外部服务连接集中在一套 Workers / workerd 架构中，目标是让每个用户拥有独立应用实例并通过 Gatekeeper 按资源授权。

## 用法

本地体验需安装 pnpm 后运行 `pnpm run-local`，数据保存在 `.wrangler`；上游明确该路径不适合生产。生产方向可部署到 Cloudflare account，并为 GitHub、Google、Cloudflare、Supabase、Notion、Slack 等 Gatekeeper 配置独立 OAuth；完全自托管的 `workerd` 部署文档仍标为 `COMING SOON`。

## 原理

每个 workspace 由 Durable Object 保存状态，每个 Gadget server 在 Dynamic Worker Facet 中运行，前端置于 sandboxed iframe。Gadget 默认无外网，由显式 Workers Binding / Gatekeeper 获得 capability；有副作用的 Gatekeeper 调用可先返回模拟结果并排队，最终由人类批量批准或拒绝。Blueprint 只复制代码与 binding 形状，不携带聊天、SQLite 数据或凭据。

## 价值

相较把广域 MCP 权限预装给每段会话，按具体资源 introduction 的 capability 模型更适合企业逐资源授权和审计。每人一份 Gadget、可修改源码、Blueprint 复制和 Durable Object 协作，也提供了“AI 生成内部小应用”而非继续堆叠中心化 SaaS 的工程路径。

## 风险边界

- README 使用“不会泄露”“完全安全”等绝对表述，但本轮只有设计与源码静态证据，没有独立渗透、多租户、浏览器 sandbox escape、SSRF 或 Gatekeeper bypass 测试。
- delayed approval 会向 Agent 返回模拟成功与模拟读结果；若模拟语义和真实服务不一致，后续计划、幂等、顺序、补偿和用户最终审批可能出现偏差。
- sharing 文档仍列出 binding-aware access control 等未来工作；share link、collaborator、presence 与 live-session 撤销需按实际版本复测，不能只依赖 capability 设计。
- OAuth client secret、AI Gateway token、组织内容、trace 和外部服务数据集中在多个 Workers / Durable Objects；每个 Gatekeeper 的 scope、日志、撤销和租户隔离必须单独验收。
- 根 manifest `1.0.0` 不是已发布稳定制品；无 Release / tag 且项目为 Early Access，应固定 commit，而不是按 `main` 部署后默认自动追随。
- 开源代码可在 workerd 上运行不等于当前已具备完整自托管交付；上游文档明确生产自托管工具尚未完成。

## 补充建议

先固定 commit，在独立 Cloudflare 测试账户中只启用一个只读 Gatekeeper 和合成数据；用恶意 Gadget / Blueprint、跨用户 share、撤销后长连接、模拟写后读、OAuth scope growth、外网绕过与日志脱敏 fixture 验证 fail-closed。任何写能力都应保留服务端幂等键、真实写后回读和人工审批，不把 README 的绝对安全表述写入组织风险结论。

## 参考资料

- [GitHub 仓库](https://github.com/cloudflare/cloudflare-os)
- [GitHub REST API](https://api.github.com/repos/cloudflare/cloudflare-os)
- [README 与架构概览](https://github.com/cloudflare/cloudflare-os/blob/main/README.md)
- [Sharing 权限模型](https://github.com/cloudflare/cloudflare-os/blob/main/docs/sharing.md)
- [Blueprint 数据边界](https://github.com/cloudflare/cloudflare-os/blob/main/docs/blueprints.md)
- [OAuth sign-in](https://github.com/cloudflare/cloudflare-os/blob/main/docs/oauth-signin.md)
- [Public server 配置](https://github.com/cloudflare/cloudflare-os/blob/main/docs/public-server.md)
- [Connect handoff 威胁模型](https://github.com/cloudflare/cloudflare-os/blob/main/docs/connect-handoff.md)
- [LICENSE](https://github.com/cloudflare/cloudflare-os/blob/main/LICENSE)
