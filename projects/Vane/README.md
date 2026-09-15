<!-- markdownlint-disable MD013 MD034 -->

# Vane：自托管的检索增强问答引擎

> 上游仓库：https://github.com/ItzCrazyKns/Vane · 归类：RAG、检索与知识处理 · 本页基于 2026-09-16 的 README、architecture/API 文档、源码、package、release、LICENSE 与 GitHub REST API 静态整理；未部署服务或验证答案质量。

## 定位

Vane 是一个可自托管的 AI answering engine：用 SearXNG 获取网页结果，再调用本地 Ollama 或 OpenAI、Anthropic、Gemini、Groq 等 provider 生成带引用回答；同时支持图片/视频搜索、文件上传、对话历史和深度研究循环。

2026-09-16 的 GitHub 官方 TypeScript Trending 抓取显示约 `+96 stars today`；REST API 快照为 `36,890 stars / 4,086 forks / 352 open issues`，MIT，最新 release 与根 package 均为 `v1.12.2`，master 最近 push 为 2026-09-01。

## 用法

上游推荐使用带 SearXNG 的 Docker 镜像：

```sh
docker run -d -p 3000:3000 \
  -v vane-data:/home/vane/data \
  --name vane itzcrazykns1337/vane:latest
```

打开 `http://localhost:3000` 后再配置模型、embedding 和 API key。已有 SearXNG 时可改用 `slim-latest` 并传入 `SEARXNG_API_URL`；也可从源码执行 `npm i && npm run build && npm run start`。

## 原理

- SearXNG 聚合网页搜索，Speed / Balanced / Quality 模式控制检索深度；深度模式采用 reason-search-scrape-extract-repeat 循环。
- 模型先分类与规划查询，搜索动作抓取网页，再用 embedding 过滤或重排内容，最后让生成模型组织回答和引用。
- 上传文件保存在 `data/uploads`，PDF、Office、图片与文本进入本地解析/语义检索链；聊天和配置使用本地持久化数据。
- `/api/providers` 暴露可用模型，搜索 API 由 caller 选择 chat model、embedding model、sources 和 history。
- `v1.12.2` release 重点修复超时、上传、widget 错误和搜索上下文控制，并加入 Chromium 抓取器。

## 价值

- 将搜索引擎、文件问答、多 provider 与可见引用放进一个可自托管界面，便于替换模型和保留本地历史。
- SearXNG 和本地模型路径让用户能自行控制部分网络与推理组件，而不是绑定单一 SaaS。
- API、架构说明和数据目录公开，适合团队进一步加认证、审计与评测。
- 深度研究的过程块可见，比只返回一句答案更容易定位搜索或抽取失败。

## 风险边界

- README 的“完全私密”不能直接成立：选择云端 chat/embedding provider 会外发 query、history、检索内容或上传文件片段，SearXNG 也会访问外部搜索源。
- README 路线图仍列着“Adding authentication”；不要把默认 `3000` 端口、文件上传或 API 暴露到公网或不可信局域网。
- 引用由模型根据参考内容生成并由 UI 渲染，不证明每个句子被来源支持；网页内容还可能包含 prompt injection、SEO 垃圾或过期事实。
- Chromium 抓取、Office/PDF 解析与上传目录会扩大不可信输入面，需要限制大小、类型、超时、脚本和网络。
- `latest` 镜像不可复现；本地保存历史和 API key 也需要备份、加密、删除和多用户隔离策略。
- 本页未部署 `v1.12.2`，没有验证搜索召回、引用精度、provider 费用、漏洞修复或并发稳定性。

## 补充建议

1. 固定镜像 digest 或 commit，只绑定 loopback，并在反向代理层先加认证、TLS、上传限制与速率限制。
2. 用已知答案与无答案问题建立 citation 金标，分别测检索召回、来源相关性、句子蕴含和拒答。
3. 为 local 与 cloud provider 分别画数据流；敏感文件只允许本地 embedding/chat 路径，并抓包确认没有回退外发。
4. 将历史、上传、API key 和模型 cache 分卷管理，测试导出、删除、备份恢复和多用户越权。

## 参考资料

- 上游 README：https://github.com/ItzCrazyKns/Vane
- Architecture：https://github.com/ItzCrazyKns/Vane/tree/master/docs/architecture
- Search API：https://github.com/ItzCrazyKns/Vane/blob/master/docs/API/SEARCH.md
- `v1.12.2` release：https://github.com/ItzCrazyKns/Vane/releases/tag/v1.12.2
- GitHub REST API：https://api.github.com/repos/ItzCrazyKns/Vane
- LICENSE：https://github.com/ItzCrazyKns/Vane/blob/master/LICENSE
