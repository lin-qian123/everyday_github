# Scrapling（D4Vinci/Scrapling）

- GitHub：https://github.com/D4Vinci/Scrapling
- 更新日期：2026-06-02（Asia/Shanghai）

## 定位

`Scrapling` 是一套面向现代网页的自适应抓取框架，目标不是“把 HTML 抓下来”这么简单，而是把抓取、动态渲染、反爬绕过、结构化抽取和 AI/Agent 接入放到同一条工程链路里。

## 用法

### 1) 安装

```bash
pip install scrapling
```

### 2) 最小同步示例

```python
from scrapling import Fetcher

page = Fetcher(url="https://example.com").fetch()
print(page.soup.title.text)
print(page.smart_xpath("//h1").get_text())
```

### 3) 动态页面或异步抓取

```python
import asyncio
from scrapling import AsyncFetcher

async def main():
    page = await AsyncFetcher(url="https://example.com").fetch()
    print(page.soup.title.text)

asyncio.run(main())
```

### 4) 工程化使用建议

```python
from scrapling import StealthyFetcher

page = StealthyFetcher(url="https://example.com").fetch()
cards = page.css(".card", adaptive=True)
for card in cards:
    print(card.get_text())
```

## 原理（工程视角）

1. 多获取器分层：轻量场景用 HTTP Fetcher，动态页面可切到 Playwright/Chrome，反爬更重时可用 `StealthyFetcher`。
2. 自适应定位：在 CSS/XPath 失效时，通过相似文本、结构匹配和 `adaptive=True` 降低 DOM 变更带来的维护成本。
3. Spider 化调度：既能写单页脚本，也能扩展到批量并发、断点续跑、流式导出。
4. Agent 协同：仓库自带 MCP 方向能力，适合先抽内容、再把高质量文本交给模型，减少 token 浪费。

## 价值

- 比“requests + BeautifulSoup”更接近真实生产抓取链路。
- 对 agent 系统很友好，因为它强调先稳定提取，再交给大模型处理。
- 同时覆盖脚本级快速验证与爬虫级工程化扩展，迁移成本较低。

## 风险边界

- 反爬绕过、代理轮换、自动化渲染都可能触碰站点条款与法律边界。
- 动态浏览器抓取成本明显高于普通 HTTP 请求，不适合无差别全量使用。
- MCP 接入虽然方便，但如果抓取源不可信，仍可能把脏内容送入下游 agent。

## 补充建议

1. 默认先用最轻的 `Fetcher`，只在必要时升级到动态或 stealth 模式。
2. 对关键字段建立回归样本，避免“抓到了页面但字段已漂移”。
3. 如果要接 agent，优先把 Scrapling 放在“采集层/清洗层”，不要把它直接等同于完整研究代理。

## 参考资料

- GitHub：https://github.com/D4Vinci/Scrapling
- 文档：https://scrapling.readthedocs.io/
- 趋势汇总页（2026-06-01 快照）：https://github.com/Lilembas/detailed-github-trending
