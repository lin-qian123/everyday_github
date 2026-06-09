# notebooklm-py

- 项目地址：https://github.com/teng-lin/notebooklm-py
- GitHub 热度（2026-03-13 抓取快照）：约 `2,756 stars`、`457 stars today`
- 定位：NotebookLM 的非官方 Python API，支持创建笔记本、上传来源、生成聊天/播客内容，并可在异步工作流中集成。

## 这是什么
`notebooklm-py` 是一个面向开发者的 Python 客户端，目标是把 NotebookLM 从“网页手工操作”变成“代码可编排的知识处理流程”。

它覆盖的核心能力包括：
- Notebook 全生命周期：创建、更新、删除、归档
- Source 管理：文本/URL/PDF/YouTube 等来源处理
- 对话与内容生成：问答、摘要、Audio Overview（播客样式）
- 异步并发：适合批量任务和后端服务化

## 怎么用（最短路径）

## 1. 安装
```bash
pip install notebooklm-py
```

## 2. 首次登录（浏览器流程）
```bash
notebooklm auth login
```

## 3. 快速创建并提问
```python
import asyncio
from notebooklm_py import NotebookLMClient

async def main():
    client = NotebookLMClient()

    nb = await client.create_notebook(title="AI Daily Research")
    await nb.add_source(content="RAG combines retrieval with generation.")

    answer = await nb.chat("Explain RAG in 3 bullet points.")
    print(answer)

    await client.aclose()

asyncio.run(main())
```

## 4. 直接用 CLI（适合轻量自动化）
```bash
notebooklm --help
```

## 原理是什么（工程视角）

## 1. API 适配层
该库基于 NotebookLM 的网络请求协议做了 SDK 封装（项目文档明确提到“reverse-engineered undocumented Google APIs”）。

## 2. 会话与鉴权层
通过浏览器登录拿到会话，再由客户端复用鉴权上下文执行后续 API 调用。

## 3. 资源模型层
把 Notebook、Source、Chat/Audio 等对象统一抽象，屏蔽网页端的复杂交互步骤，变成可组合的方法调用。

## 4. 异步执行层
基于 Python `async` 设计，支持并发任务（例如一次性处理多个 Notebook 或多条来源文档）。

## 5. 风险与边界
- 非官方 API 可能随 NotebookLM 前端/后端变更而失效
- 受 Google 账号状态、风控和速率限制影响
- 不适合作为“强 SLA 核心链路”的唯一依赖，建议预留降级方案

## 适用场景
- AI 资讯日报自动化：批量喂给来源后统一问答/总结
- 研究助手：把 YouTube、网页、PDF 聚合到 notebook 再做主题提炼
- 企业知识中台 PoC：先用 NotebookLM 验证人机协作流程，再决定是否自建

## 与同类方案的区别
- 相比纯 RAG 框架：`notebooklm-py` 更接近“直接调用 NotebookLM 产品能力”
- 相比手工网页操作：可脚本化、可批处理、可接入 CI/定时任务
- 相比自建 Agent 全栈：上线更快，但平台依赖更强

## 今天建议
1. 先做 1 个最小用例：自动导入 3 条来源 + 生成 1 份摘要。
2. 增加失败重试与速率限制（避免批量任务被封控）。
3. 给生产流程加兜底：NotebookLM 调用失败时回退到本地 RAG。

## 参考来源
- GitHub 仓库：https://github.com/teng-lin/notebooklm-py
- 项目 README（功能、鉴权、用法）：https://github.com/teng-lin/notebooklm-py
- GitHub Trending 快照（stars today）：https://github.com/trending
