<!-- markdownlint-disable MD013 MD034 -->

# open-seo：把 SEO 数据、MCP 与 agent skills 放进可自托管工作台

## 项目概览

- 上游仓库：https://github.com/every-app/open-seo
- GitHub API 快照（2026-09-02）：16,123 stars、1,958 forks、126 个开放 issue
- 当前 release：`v0.1.6`
- 主要技术：TypeScript、Web UI、MCP、Agent Skills、Docker / Cloudflare 自托管
- 许可证：MIT

## 定位

OpenSEO 是面向个人与团队的开源 SEO 工作台，覆盖关键词研究、排名跟踪、竞品、反向链接、站点审计和 AI 搜索可见性。它同时暴露 MCP server 和 agent skills，让 Claude Code、OpenClaw、Hermes 等 agent 读取 SEO 数据并执行结构化工作流。

它不是免费的全量搜索数据源：自托管仍需要 DataForSEO API key，并按调用付费；官方托管版则在数据请求成本上增加服务费。

## 用法

上游提供两条自托管路径：个人测试可用 Docker，面向多设备或团队的互联网部署推荐 Cloudflare。无论哪种路径，都需要单独申请 DataForSEO key。

接入 agent 前，应先在 Web UI 中用少量已知关键词核对数据口径，再按官方文档配置 MCP 与 skills。不要一开始就允许 agent 批量抓取、改站或自动向外部系统发布内容。

## 原理

OpenSEO 将 DataForSEO 等外部数据请求组织成面向关键词、排名、链接和审计的应用工作流，并通过 Web UI 给人使用、通过 MCP 给 agent 调用。Agent Skills 提供步骤约束，MCP server 提供数据与动作接口。

这种结构能降低 agent 使用 SEO 数据的接入成本，但输出仍受数据覆盖、地区、设备、时间窗口、搜索引擎个性化和关键词定义影响；LLM 的解释也不会自动消除这些偏差。

## 价值

- 将常见 SEO 工作流、数据与 agent 接口放在一个可修改的开源项目中。
- BYO DataForSEO key 让数据成本和平台服务费更容易拆开审计。
- MCP 与 skills 适合把重复报告、问题分诊和站点审计步骤结构化。
- 自托管便于团队控制 UI、工作流和部分业务数据。

## 风险边界

- 自托管不等于零成本或完全离线；核心 SEO 数据依赖第三方 API 与其许可、配额和保留政策。
- MCP key、站点清单、竞品与搜索策略属于敏感商业数据，须限制日志、agent 上下文和网络出口。
- 排名与 AI visibility 是采样指标，不能直接等同于真实转化、品牌影响或因果效果。
- 批量查询、抓取、内容生成和自动改站可能触发平台条款、费用失控、错误发布和搜索质量风险。
- 本页只核对上游静态资料、release 与 API，未部署，也未复算其数据准确率或节省成本主张。

## 补充建议

1. 用固定地区、设备、关键词与抓取时间建立小型基线，记录 DataForSEO 原始响应和 OpenSEO 展示差异。
2. 给 MCP 使用只读、低配额 key，按项目隔离客户域名、竞品和导出数据。
3. 把 agent 建议分成诊断、候选动作和已人工批准动作，禁止直接批量发布或改生产站。
4. 同时跟踪查询费用、数据新鲜度、误报和实际转化，不用单一可见性分数决策。
5. 对互联网自托管单独配置认证、密钥轮换、备份、审计日志和 Cloudflare 权限。

## 参考资料

- 仓库与 README：https://github.com/every-app/open-seo
- 官方站点：https://openseo.so
- Releases：https://github.com/every-app/open-seo/releases
- MCP 设置：https://openseo.so/docs/mcp
- Agent Skills 设置：https://openseo.so/docs/skills/setup
- Docker 自托管：https://github.com/every-app/open-seo/blob/main/docs/SELF_HOSTING_DOCKER.md
- 官方 X 账号：https://x.com/bensenescu
