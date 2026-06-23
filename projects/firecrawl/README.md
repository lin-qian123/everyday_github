# firecrawl（firecrawl/firecrawl）

- GitHub: https://github.com/firecrawl/firecrawl
- 官网: https://firecrawl.dev
- 记录日期: 2026-06-23 (Asia/Shanghai)

## 定位

`firecrawl` 是一个面向 LLM / agent 的 Web 数据 API，目标不是做通用浏览器自动化，而是把搜索、抓取、交互、站点爬取和结构化提取封成稳定接口，直接输出 Markdown、JSON、截图等更适合模型消费的结果。

## 热度信号

1. GitHub API 在 2026-06-23 抓取时显示约 `137.3k stars`、`8.0k forks`，`updated_at` 为 `2026-06-23T01:00:07Z`。
2. GitHub Trending 日榜在 2026-06-23 抓取时仍出现该项目，当日新增星标约 `615 stars today`。
3. 官方 README 把自己定义为 `The API to search, scrape, and interact with the web at scale`，并明确强调 `LLM-ready output`、`agent ready`、`media parsing` 和 `actions`。

## 用法

### 1) 申请 API Key

官方托管服务入口是 `firecrawl.dev`，README 默认以 API 方式使用：

```python
from firecrawl import Firecrawl

app = Firecrawl(api_key="fc-YOUR_API_KEY")
```

### 2) 搜索 Web 并直接拿正文内容

```python
search_result = app.search("firecrawl", limit=5)
```

它不是只返回链接列表，而是会把搜索结果页对应的内容一并转成更适合 LLM 消费的格式。

### 3) 抓取和交互

README 给出的核心接口包括：

- `search`：搜网页并带回内容
- `scrape`：把页面转成 Markdown / HTML / JSON / screenshot
- `interact`：对页面执行点击、输入、等待等动作后再抽取
- `crawl` / `map` / `batch scrape`：大规模站点级数据采集

CLI 也支持直接运行：

```bash
firecrawl search "firecrawl" --limit 5
firecrawl scrape https://firecrawl.dev
```

## 原理

1. 它把搜索、抓取、JS 页面处理、反爬代理、速率限制和媒体文档解析都藏在服务端，用户只消费统一 API。
2. 输出层专门针对 LLM 场景设计，避免用户自己再把原始 HTML 清洗成 Markdown 或结构化 JSON。
3. 除了“读页面”，还提供 action/interaction 能力，使它能在一定程度上覆盖需要先操作再抓取的网页。
4. 从 README 看，`firecrawl` 的价值在于把“网页上下文接入”标准化成 agent 可复用能力，而不是每个项目都自写一套爬虫管线。

## 价值

- 对 RAG、deep research、网页监控、自动化情报采集和网站数据接入非常实用。
- 它已经从单一 scraping 工具进化成“agent 的 Web context 层”，这也是它长期高热的重要原因。
- 如果团队经常在“搜索 -> 打开页面 -> 清洗正文 -> 再喂模型”之间重复造轮子，`firecrawl` 这类 API 的工程价值很高。

## 风险边界

- 默认主路径是托管 API，不是纯本地工具；敏感数据或受限网页场景要特别注意合规与出网边界。
- README 中的覆盖率、延迟与 benchmark 数据主要来自官方，适合做方向判断，不应直接等价为你自己的生产表现。
- 大规模网页抓取会碰到网站条款、robots、版权和频控问题，工程可用不代表使用上没有法律与平台规则风险。

## 补充建议

1. 先区分你的需求是“网页检索增强”还是“批量站点采集”，前者适合快速接入，后者要更重视成本和合规。
2. 可以把它与 `crawl4ai` 对照看：`crawl4ai` 更偏开源本地抓取流水线，`firecrawl` 更偏成熟 API 产品层。
3. 真正落地前最好测三件事：命中率、清洗质量、复杂页面交互后提取的稳定性。

## 参考资料

- https://github.com/firecrawl/firecrawl
- https://firecrawl.dev
- https://github.com/trending
