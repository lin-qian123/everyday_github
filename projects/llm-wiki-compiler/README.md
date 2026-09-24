<!-- markdownlint-disable MD013 -->

# llm-wiki-compiler（atomicstrata/llm-wiki-compiler）

- GitHub：<https://github.com/atomicstrata/llm-wiki-compiler>
- 抓取快照：2026-09-25，2,111 stars、223 forks、7 open issues
- 热度信号：GitHub TypeScript Trending 抓取时约 +13 当日 stars
- 版本与许可：MIT；latest GitHub Release / tag 为 `v1.3.0`，根 package 已是 `1.4.0-dev.20260919`

## 定位

llm-wiki-compiler（CLI 名 `llmwiki`）把论文、笔记、README、transcript、PDF、图像与网页等原始材料编译为可追踪引用、可互链、可审阅的 Markdown wiki。它强调把重复的 query-time 重建前移到 compile-time，并通过 lifecycle profile 支持研究、新闻等领域的 typed records、relations、states 和 gates。

## 用法

用户安装 npm package 后初始化 wiki，配置 provider 与 source，再执行 ingest / compile / query / lint / view / refresh / eval。默认生成 concept、entity、comparison、overview；可用 `autosci`、`newsroom` 或自定义 `.llmwiki/profile.json` 增加 schema / workflow，也可通过 MCP server、TypeScript SDK、OKF、JSON-LD、GraphML、Marp 和 `llms.txt` 接入其他 Agent / 工具。

## 原理

两阶段 LLM pipeline 先抽取概念，再生成带 source file / line range 的 typed pages；检索层组合 semantic chunk search、BM25 reranking 与 wikilink graph expansion。profile runtime 在写路径实施 relation、evidence、artifact 与 human / agent gate，lint / eval 再检查 citation、freshness、孤立页面和 regression；签名 template distribution 用 Ed25519、catalog trust、key rotation 与 revocation 管理模板交换。

## 价值

对于会反复使用的稳定材料，编译后的 wiki 能保留来源、审阅状态、关系和上下文包，减少每次让 Agent 从散乱原文重新解释。CLI、viewer、MCP、SDK 与开放导出格式也使知识资产更容易在人工阅读、Agent query 和版本控制之间复用。

## 风险边界

- 引用到文件 / 行只证明 provenance link 存在，不证明抽取、合并、实体消歧和结论正确；生成页面仍可能漏证据、误引或把模型推断固化为事实。
- compile-time 错误会被后续 query 重复消费；source freshness、contradiction、review queue 和人工抽检不是可选装饰。
- provider portable 不等于数据永远本地：Anthropic、OpenAI、Copilot、Atlas、OrcaRouter 等路径会发送原始材料或证据包；PDF、transcript 与企业文档还可能受保密 / 版权约束。
- MCP write、template tap、OKF import 与 connector 会扩大供应链和写入面；签名只验证发布者 / 完整性，不证明模板逻辑、数据源或提示安全。
- Release `v1.3.0` 与开发 manifest `1.4.0-dev.20260919` 已漂移，profile / export compatibility 要固定版本验证。

## 补充建议

先用十几份有已知答案和刻意矛盾的公开材料建立小型金标，固定模型、prompt、chunking、profile 和 commit；比较 raw search 与 compiled wiki 的 citation precision、遗漏、staleness、成本和复核时间。默认把外部 import 放进 review queue，MCP 仅给测试 wiki 写权限，并为敏感 source 选择本地 provider 与独立加密存储。

## 参考资料

- [GitHub 仓库](https://github.com/atomicstrata/llm-wiki-compiler)
- [GitHub REST API](https://api.github.com/repos/atomicstrata/llm-wiki-compiler)
- [v1.3.0 Release](https://github.com/atomicstrata/llm-wiki-compiler/releases/tag/v1.3.0)
- [官方文档](https://llmwiki.atomicstrata.ai/)
- [Karpathy LLM Wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)
- [Configurable Lifecycle Profiles](https://github.com/atomicstrata/llm-wiki-compiler/blob/main/docs/concepts/configurable-lifecycle-profiles.mdx)
- [LICENSE](https://github.com/atomicstrata/llm-wiki-compiler/blob/main/LICENSE)
