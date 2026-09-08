<!-- markdownlint-disable MD013 MD034 -->

# notfair-plugin（nowork-studio/notfair-plugin）

> 记录日期：2026-09-09（Asia/Shanghai）。本页依据上游 README、CHANGELOG、plugin / MCP 配置、隐私入口、LICENSE 与 GitHub REST API 做静态整理；本轮未安装 plugin、未完成 OAuth、未读取任何广告或分析账户，也未执行营销变更。

## 定位

`notfair-plugin` 是面向 Claude Code、Codex、Cursor、Gemini CLI 等 agent 宿主的开源 SEO、GEO/AEO、广告与分析技能库。上游当前列出 45 个 skills，覆盖站点与页面审计、Search Console / GA4、Google / Meta / X / LinkedIn Ads、内容规划、跨模型复核等场景；需要实时账户数据时，通过一个 hosted NotFair MCP 完成 OAuth 连接。

2026-09-09 的 GitHub 官方 TypeScript Trending 抓取显示约 `+51 stars today`；REST API 快照为 `3,680 stars / 467 forks / 14 open issues`，MIT。仓库没有 GitHub release；默认分支可持续改变，安装前应固定 commit 并审阅 CHANGELOG。

## 用法

上游为 Codex 给出的 plugin 安装入口是：

```bash
codex plugin marketplace add nowork-studio/notfair-plugin --json
codex plugin add notfair@nowork-studio --json
codex mcp login NotFair
```

也可只克隆仓库审阅 `AGENTS.md` 与各目录的 `SKILL.md`，或运行可选本地 goal-loop 应用：

```bash
git clone https://github.com/nowork-studio/notfair-plugin.git
cd notfair-plugin
npx notfair@latest
```

真实试用应从离线 export 或只读账号开始；不要在尚未验证 connector capability、change preview 和 rollback 时接入生产广告预算。

## 原理

- **专业化 skills**：把 SEO、GEO、paid media、analytics 等任务拆成带输入、决策规则、证据和输出格式的独立流程。
- **通用入口**：根 `AGENTS.md` 将用户意图路由到 canonical `SKILL.md`，避免把逻辑绑死到单一宿主。
- **单一 hosted MCP**：OAuth 后由一个 `NotFair` server 暴露当前 workspace 已连接的 Search Console、GA4、广告、CRM 与 CMS 能力。
- **占位符解析**：skill 使用 tool-agnostic connector 名称，由当前会话解析到可用工具，而不是硬编码 MCP namespace。
- **只读到写入**：上游强调先 review、再明确批准 mutation；不支持的 TikTok、Amazon、ChatGPT Ads 保持规划或 export-review。
- **可选循环应用**：本地 app 把可量化目标变成周期 agent loop，但不是使用 skills 的必需组件。

## 价值

- 将营销建议从通用 prompt 推向有数据源、口径、审批边界和可复核输出的流程。
- 开源 skill 文本便于企业把规则、品牌和测量标准 fork 成自己的版本。
- 一个 MCP 入口减少多平台连接配置重复，并能按实际授权暴露 capability。
- SEO / GEO、广告与分析放在同一证据链中，有利于区分内容动作、流量变化与业务结果。

## 风险边界

- Hosted MCP 与 OAuth 可能接触搜索、分析、广告、CRM 和 CMS 的敏感业务数据；开源 skill 不代表托管服务、token 保留和子处理方已被本页审计。
- “safe by design”“evidence-led”是上游设计主张。行为规则不能替代服务端权限、账户 change history、预算上限、幂等和独立审批。
- 广告归因、GEO 可见性、ROAS 与自然流量都受延迟、季节、实验设计和平台黑箱影响；一次 agent 分析不能证明因果。
- 自动生成内容、schema、creative 或 targeting 可能触发平台政策、隐私、品牌、版权和地区监管风险。
- CHANGELOG 曾明确描述本地 app 中 Codex 作为 trusted unsandboxed automation 运行；workflow/PR 限制只是行为 guardrail，不能当 OS sandbox。
- Trending 与 stars 不证明营销效果；本轮也没有读取真实账户、执行 mutation 或验证 connector 返回值。

## 补充建议

- 先用脱敏 CSV/export 做 read-only audit，固定完整时间区间、时区、币种、归因窗口和分母，再与平台 UI 抽样对账。
- OAuth 使用单独测试 workspace、最小 scope 和低预算 sandbox；将 proposal、approval、execution、post-readback 四步写入不可变日志。
- 对每类 mutation 设置预算 / bid / targeting allowlist、idempotency key、dry-run diff 和自动 rollback，不允许模型自行扩大目标。
- 自托管或采购前分别审阅开源仓库、hosted MCP、隐私政策、数据保留与删除流程，不把它们视为同一个许可或信任对象。

## 参考资料

- GitHub 仓库：https://github.com/nowork-studio/notfair-plugin
- GitHub REST API：https://api.github.com/repos/nowork-studio/notfair-plugin
- Skill catalog：https://github.com/nowork-studio/notfair-plugin#skill-catalog
- MCP connection：https://github.com/nowork-studio/notfair-plugin/blob/main/docs/mcp-connection.md
- CHANGELOG：https://github.com/nowork-studio/notfair-plugin/blob/main/CHANGELOG.md
- 隐私政策：https://notfair.co/privacy
- LICENSE：https://github.com/nowork-studio/notfair-plugin/blob/main/LICENSE
