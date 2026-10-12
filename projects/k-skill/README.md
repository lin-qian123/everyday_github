<!-- markdownlint-disable MD013 -->

# k-skill（NomaDamas/k-skill）中文解读

> 上游仓库：<https://github.com/NomaDamas/k-skill> · 归类：Agent 框架与技能生态 · 本页基于 2026-10-13 的 README、安装 / proxy / analytics 文档、skills、tag、许可证与 GitHub REST API 静态整理；未登录韩国政府、金融、招聘、电商或消息平台，也未执行预约、支付、提交或发送。

## 定位

k-skill 是面向韩国日常服务的 Agent Skill 集合，收录 125 个交通、政府、法律、房产、招聘、金融、医疗、购物、文化、天气、文档与开发者技能，兼容 Claude Code、Codex、OpenCode、OpenClaw 等宿主。

## 用法

可用 `npx --yes skills add NomaDamas/k-skill --all -g` 全量安装，或只安装一个 skill。许多顶层 `SKILL.md` 是 CLI stub，会要求运行 `@nomadamas/k-skill` 动态取得当前 runtime 对应的完整指令；部分查询经过 `k-skill-proxy`，部分需要 BYOK、浏览器登录或 Python / uv。

## 原理

- 每个 skill 把任务说明、数据源、helper、确认点和输出格式封装为可分发目录。
- CLI 根据 Dolshoi / CloakBrowser / generic 等运行环境返回不同指令，并管理更新、文件与 bundle。
- 数据来源混合官方 Open API、公开网页、远程 MCP、项目 proxy、第三方服务和本地已登录浏览器。
- 通用 hard rules 禁止未即时授权的支付、发送、最终提交、取消以及绕过 CAPTCHA / 身份验证。

## 价值

- 把韩国本地化且分散的公共数据、生活服务和文档流程组织成可发现的 Agent 能力目录。
- 区分查询、准备、预约 / 支付 handoff，并在敏感技能中保留法律免责声明和人工确认点。
- 对中文 / 英文生态少见的韩国公共 API、HWP、交通、税务、招聘与生活服务具有实际参考价值。

## 风险边界

- 全量全局安装 125 个 skills 会扩大 prompt、脚本、网络和更新供应链面；动态 `npx ...@0 instruct` 还会让运行时指令随上游变化。
- proxy 查询可能携带位置、企业、健康、法律或账号相关参数；隐私政策与 opt-out analytics 需要按实际 endpoint 复核。
- 部分 skill 依赖未文档化公开网页、已登录浏览器或第三方商标服务，可能受条款、封禁、页面漂移和个人 / 批量使用边界影响。
- 法律、金融、医疗、招聘和政府流程的检索结果不是专业意见、资格确认或官方提交回执。
- `manus-bundle-latest` 是 tag 而非语义化 Release；若直接追踪浮动 CLI / 指令，复现性有限。

## 补充建议

- 只安装任务所需 skill，并固定仓库 commit、CLI 包版本、helper hash 和实际数据源；不要默认 `--all -g`。
- 在调用 proxy 或已登录浏览器前列出发送字段、服务方、保留期和 side effect；查询与写入使用不同凭据和宿主。
- 对支付、预约、申请、消息和法律 / 医疗判断设置运行时强制确认，而不是只依赖 Markdown 提醒。

## 参考资料

- GitHub 仓库：<https://github.com/NomaDamas/k-skill>
- GitHub REST API：<https://api.github.com/repos/NomaDamas/k-skill>
- 安装说明：<https://github.com/NomaDamas/k-skill/blob/main/docs/install.md>
- Proxy 说明：<https://github.com/NomaDamas/k-skill/blob/main/docs/features/k-skill-proxy.md>
- Usage analytics：<https://github.com/NomaDamas/k-skill/blob/main/docs/usage-analytics.md>
- LICENSE：<https://github.com/NomaDamas/k-skill/blob/main/LICENSE>
