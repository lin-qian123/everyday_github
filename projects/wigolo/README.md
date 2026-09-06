<!-- markdownlint-disable MD013 -->

# wigolo（KnockOutEZ/wigolo）

> 记录日期：2026-09-07（Asia/Shanghai）。本页依据上游 README、文档、benchmark、release、LICENSE 与 GitHub REST API 做静态整理；本轮未安装浏览器引擎或本地模型，未接入任何 agent，也未复现检索质量、费用或隐私声明。

## 定位

`wigolo` 是为 coding agents 与自托管 agents 提供 search、fetch、crawl、extract、cache、find-similar、research 和 gather loop 的 local-first Web intelligence 层，支持 MCP、REST 和 SDK。基础检索路径主打无需商业搜索 API key；合成回答可选本地或云端 LLM。

2026-09-07 的 GitHub 官方 TypeScript Trending 抓取显示约 `+96 stars today`；REST API 快照为 `5,132 stars / 410 forks / 60 open issues`，最新 release 为 `v0.2.1`。API 许可证字段为 `NOASSERTION`，但仓库 LICENSE/README 明确标示 `AGPL-3.0-only`。

## 用法

上游的初始化命令要求 Node.js 20+，会下载浏览器引擎和端侧模型；带 `--agents` 时还会写入宿主 MCP/指令配置：

```bash
npx wigolo init
npx wigolo doctor
```

建议先在临时 profile 运行裸 `init` 并审查 `~/.wigolo/`、下载物和网络流量，再决定是否让命令改写 Codex、Claude Code 或其他主力 agent 配置。

## 原理

- **单进程入口**：Node 进程通过 MCP stdio、REST 或 SDK 暴露 Web 工具。
- **多引擎检索与排序**：上游描述为多个搜索引擎的 rank fusion、ML rerank、去重和可解释 evidence score。
- **分层抓取**：根据 SPA、challenge、正文稀薄等信号升级到浏览器，并缓存域名级处理经验。
- **本地索引**：抓取内容、keyword/vector index、embedding 和 reranker 默认放在本机数据目录。
- **可选合成**：`research`、`agent` 和 answer 模式可接 Gemini、Anthropic、OpenAI、Groq 或 Ollama；无 LLM 时返回 evidence brief。
- **Agent 配置写入**：初始化可为多个宿主注册 MCP server 和配套 instructions。

## 价值

- 把 Agent Web 获取从单一 search API 扩展到抓取、缓存、相似检索和证据片段。
- 本地基础组件避免每次查询都产生商业 API 费用，并允许检查缓存与模型资产。
- 结果包含 citation ID、source span 和评分结构，为下游核验提供更明确入口。
- MCP、REST 与 SDK 三种表面便于个人 coding agent 和自托管服务复用。

## 风险边界

- “local-first / nothing leaves”只适用于所选配置的上游描述：查询仍发送到公共搜索引擎和目标站点，云 LLM、代理与可选 backend 会增加外发。
- 搜索引擎结果、抓取正文、rank fusion 与 ML rerank 仍可能遗漏、偏置、过时或被 SEO/prompt injection 操纵。
- README benchmark 是上游设计的少量对比，不能证明对所有语言、站点、时效、深度或付费工具具有同等质量。
- 浏览器引擎和抓取行为受 robots、站点条款、登录、版权、频率限制与地区法律约束；技术可取不等于允许批量复用。
- 自动写入 agent 配置扩大供应链和工具权限；网页中的恶意指令可能借 MCP 输出进入高权限 agent。
- AGPL 网络服务义务与商用边界应按实际修改和部署方式审查，不能只依赖 README 的简化解释。

## 补充建议

- 固定 release/commit，在隔离 profile 记录安装前后文件、进程、端口、下载 hash、网络域名和卸载残留。
- 用带已知答案、动态页面、robots、登录墙、恶意 prompt 和内容更新的 golden set 测 precision、recall、引用定位与失败标记。
- 默认只把网页内容当不可信数据，禁止其更改系统提示、权限、凭据或后果性操作。
- 为缓存设置项目隔离、容量、加密、保留期和 purge 验证；不要索引含 secrets 的内部页面。
- 若部署 REST/HTTP 服务，增加鉴权、loopback/网段限制、并发/抓取速率、审计和 AGPL 法务评估。

## 参考资料

- [GitHub 仓库](https://github.com/KnockOutEZ/wigolo)
- [GitHub REST API](https://api.github.com/repos/KnockOutEZ/wigolo)
- [v0.2.1 Release](https://github.com/KnockOutEZ/wigolo/releases/tag/v0.2.1)
- [文档索引](https://github.com/KnockOutEZ/wigolo/tree/main/docs)
- [Benchmark](https://github.com/KnockOutEZ/wigolo#benchmark)
- [AGPL-3.0-only License](https://github.com/KnockOutEZ/wigolo/blob/main/LICENSE)
