<!-- markdownlint-disable MD013 -->

# Scrapling：HTTP、浏览器与爬虫工作流的统一采集层

- 上游：[D4Vinci/Scrapling](https://github.com/D4Vinci/Scrapling)；分类：RAG、检索与知识处理。
- 更新：2026-11-03（Asia/Shanghai）；固定主线 SHA：`95cf9019ab5a5d6f3e9654b7ef1c6a26e29dc5c0`。
- 热度快照：综合 daily +858；API 92,764 stars / 9,771 forks / 9 open issues（含 PR）。最新发行 v0.5，UTC 2026-10-17；PyPI 0.5，Python >=3.10。
- 证据：官方 Trending / API 与固定源码静态核读；下文用法供复核，不表示本轮已运行。

## 定位

Scrapling 统一 HTTP、浏览器渲染、CSS / XPath、自适应选择、并发 spider、导出与 MCP。它可为检索 / Agent 提供采集内容，但不会自动验证来源事实、消除网页注入或取得目标站点访问授权。

本页修订 2026-06-02 的旧说明。0.5 迁移文档明确删除普通 DynamicFetcher / DynamicSession 后端，改用对应 Stealthy 类；MCP 工具和网络记录接口也有变化。

## 用法

按任务选择 extras，当前获取器所需依赖不应只靠基础解析包：

```sh
python -m pip install "scrapling[fetchers]==0.5"
scrapling install
```

```python
from scrapling.fetchers import Fetcher

page = Fetcher.get("https://quotes.toscrape.com/")
quotes = page.css(".quote .text::text").getall()
print(quotes)
```

上例来自当前 README；本轮未执行。需要浏览器时使用 StealthyFetcher，异步 / 会话按当前公开接口配置。MCP 另安装 ai extra，可用 scrapling-mcp 的 stdio 接入。旧页的 Fetcher 构造器、page.soup / smart_xpath 和 AsyncFetcher 用法不再作为当前推荐示例。

## 原理

- HTTP 请求、持久浏览器会话和并发 spider 分层复用连接、cookies 与调度。
- CSS / XPath 等解析配合自适应元素追踪；DOM 变化后仍应核字段和数据质量。
- 0.5 浏览器路线使用 Patchright；record_requests 网络记录、页面 snapshot、截图与 JS 执行扩展 Agent 的观察 / 操作面。
- Spider 的重试、限速、恢复和流式输出处理采集生命周期；单次运行内的去重集合不等于跨运行持久去重。

## 价值

适合把静态 HTTP 优先、必要时浏览器回退、字段清洗与批量输出串成可维护流程。它比“让模型读整个页面”更容易控制输入体积，但 extraction 正确性仍应靠字段样本和来源回链验收。

## 风险边界

- “不可检测”“绕过验证码”等是上游宣传或功能描述，本页未验证成功率，也不意味着可访问任意站点。应限定授权目标、请求范围与频率。
- MCP 包括 POST / PUT / DELETE、网页操作、JS、登录状态与网络响应读取，不能当作纯只读搜索工具。页面内容是不可信输入，cookies / 网络日志也可能含凭据。
- 当前 HTTP transport 默认绑定 127.0.0.1，要求 token；--no-auth 是显式关闭。共享单 token 不区分客户端权限，公网还需 TLS / allowed-host 和网络限制；stdio 的边界不同。
- BSD-3-Clause 覆盖框架，不改变采集内容、目标网站和代理服务的条款。README 有商业代理赞助，相关服务宣传不能作为独立性能证据。
- 本轮未安装浏览器、连接 MCP、登录站点、抓取数据集或验证认证 / 反爬效果。

## 补充建议

1. 按 0.5 迁移清单逐项替换旧类、网络记录和 MCP 工具名，保存小规模字段回归样本。
2. 默认使用轻量 HTTP，遇到确有授权的动态场景再启浏览器，记录回退原因和成本。
3. 对 MCP 限制网络与凭据；需要跨运行去重时持久化稳定键，校验恢复后重复 / 丢失情况。

## 参考资料

- [README.md](https://github.com/D4Vinci/Scrapling/blob/95cf9019ab5a5d6f3e9654b7ef1c6a26e29dc5c0/README.md)。
- [pyproject.toml](https://github.com/D4Vinci/Scrapling/blob/95cf9019ab5a5d6f3e9654b7ef1c6a26e29dc5c0/pyproject.toml)。
- [docs/migrating-to-v0.5.md](https://github.com/D4Vinci/Scrapling/blob/95cf9019ab5a5d6f3e9654b7ef1c6a26e29dc5c0/docs/migrating-to-v0.5.md)。
- [docs/ai/mcp-server.md](https://github.com/D4Vinci/Scrapling/blob/95cf9019ab5a5d6f3e9654b7ef1c6a26e29dc5c0/docs/ai/mcp-server.md)。
- [scrapling/core/ai/server.py](https://github.com/D4Vinci/Scrapling/blob/95cf9019ab5a5d6f3e9654b7ef1c6a26e29dc5c0/scrapling/core/ai/server.py)。
- [LICENSE](https://github.com/D4Vinci/Scrapling/blob/95cf9019ab5a5d6f3e9654b7ef1c6a26e29dc5c0/LICENSE)。
- [仓库 API](https://api.github.com/repos/D4Vinci/Scrapling)；[发行记录](https://github.com/D4Vinci/Scrapling/releases/tag/v0.5)。
