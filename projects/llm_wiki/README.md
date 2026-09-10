<!-- markdownlint-disable MD013 -->

# LLM Wiki（nashsu/llm_wiki）中文解读

> 证据快照：2026-09-11（Asia/Shanghai）。GitHub REST API 显示 18,066 stars、2,098 forks、257 open issues；最新 release 与根 package 均为 `v0.6.11` / `0.6.11`。API 许可证字段为 `NOASSERTION`，但根 README 与 `LICENSE` 明确为 GNU GPL v3。本文未安装应用、导入文档或复现上游检索 benchmark。

## 定位

LLM Wiki 是一个 Tauri 跨平台桌面知识库：把 PDF、Office、EPUB、图片、网页等 source 先分析，再持续编译为用户拥有的 cross-linked Markdown wiki。它强调“知识写入长期 artefact 后复用”，而不是每次 query 都只从向量库临时取 chunk。

项目源于 Andrej Karpathy 的 LLM Wiki pattern，并扩展了 graph、review、deep research、agent tools、MCP、浏览器剪藏和多格式解析。

## 用法

普通用户可从 Releases 下载 macOS、Windows、Linux 二进制；源码构建需要 Node.js 20+、Rust 1.88+ 与 `protoc`：

```bash
git clone https://github.com/nashsu/llm_wiki.git
cd llm_wiki
npm install
npm --prefix mcp-server ci
npm run mcp:build
npm run tauri dev
```

首次创建 project 后配置 ingest/chat provider，导入 source，观察 activity queue 生成 wiki，再用 Chat、Search、Graph、Lint 与 Review 复核。可选 vector search、MinerU 与 web search provider 不应默认开启。

## 原理

- 三层结构是 immutable raw sources、LLM-generated wiki 与 schema/purpose；source hash 用于跳过未变文件。
- ingest 分 analysis 与 generation 两个 LLM call，生成 summary、entity/concept、index、overview 与 `sources[]` provenance。
- query 组合 tokenized search、可选 LanceDB vector search、wikilink/共享 source/Adamic-Adar/type affinity graph expansion 和 context budget。
- persistent queue 处理 crash/retry；cascade deletion 尝试清除已删 source 对应页面与死链。
- Rust backend agent 可调用 wiki/source/graph/web search、workspace 文件与经批准 shell；本地 token-protected HTTP API 和 MCP 默认绑定 `127.0.0.1:19828`。

## 价值

- 把生成知识保存成可读 Markdown，并用 `sources[]` 和 raw files 提供比黑箱向量命中更直观的回溯面。
- incremental ingest、queue、export/import 和 deterministic index rebuild 适合长期积累个人或研究资料。
- graph/community/review/lint 把知识冲突、低连接页面和待人工判断显式化。
- local parser、Ollama/custom endpoint 与只读 skill 提供从本机到 cloud provider 的多种数据边界选择。

## 风险边界

- wiki 是 LLM 生成的二次知识；一次错误可能通过 cross-link、overview 与后续 ingest 持续传播。`sources[]` 是线索，不保证每个句子被原文支持。
- “Read Sources Only”、citation prompt、graph score 或上游 58.2%→71.4% recall benchmark 都不是零幻觉或通用检索证明。
- OpenAI/Anthropic/Google、MinerU Cloud、Tavily/SerpApi/Firecrawl 等配置会把内容发送到外部；local UI 不等于全链路离线。
- source auto-watch、cascade delete、agent workspace 与 shell approval 会写文件；误分类、重命名或删除必须可回滚。
- API `NOASSERTION` 与根 GPL-3.0 的差异要求部署/分发时以实际 LICENSE 为准，不能按未识别字段推断宽松许可。

## 补充建议

1. 用副本资料库和 20–50 份有标准答案的 source 建 golden set，逐句检查 citation、遗漏、冲突与 cascade delete。
2. 默认使用内置/local parser、关闭 web/deep research/shell，把 provider、base URL 与数据去向写入 project 记录。
3. 对每页保存 source hash、ingest model、prompt/schema version 与生成时间；重大事实回到 raw source 核验。
4. 定期导出 ZIP、Git 管理 wiki Markdown，并在升级前验证恢复；分发修改版前审查 GPL-3.0 义务。

## 参考资料

- GitHub：<https://github.com/nashsu/llm_wiki>
- GitHub REST API：<https://api.github.com/repos/nashsu/llm_wiki>
- 中文 README：<https://github.com/nashsu/llm_wiki/blob/main/README_CN.md>
- Releases：<https://github.com/nashsu/llm_wiki/releases>
- 原始 LLM Wiki pattern：<https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f>
- Agent skill：<https://github.com/nashsu/llm_wiki_skill>
- LICENSE：<https://github.com/nashsu/llm_wiki/blob/main/LICENSE>
