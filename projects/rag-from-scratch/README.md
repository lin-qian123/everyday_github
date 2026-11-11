<!-- markdownlint-disable MD013 -->

# RAG From Scratch：用五份 Notebook 拆解检索增强生成

- 上游：[`langchain-ai/rag-from-scratch`](https://github.com/langchain-ai/rag-from-scratch)；仓库 ID：`750618502`。
- 核读：2026-11-12（Asia/Shanghai）；主线固定于 [`1fdb7d0e4f1d`](https://github.com/langchain-ai/rag-from-scratch/tree/1fdb7d0e4f1d3e731c8397332452715512f18667)。
- 热度快照：9,845 stars / 2,268 forks / 46 open issues（含 PR）；来自 [GitHub API](https://api.github.com/repos/langchain-ai/rag-from-scratch)，不代表采用量或质量。

## 定位

LangChain 的历史教学仓库，以五份 Notebook 配套视频，从索引、检索、生成讲到查询变换、路由、索引改进和纠错流程。今天官方 Jupyter Notebook daily +164，是本仓库首次建档，不是新发布课程；主线最后提交在 UTC 2025-06-26，发行列表为空。

固定目录树只有 README 和五份 Notebook，未发现根 LICENSE、依赖锁文件或独立测试配置；GitHub API 也未返回 license。公开可读不等于已有明确再分发授权。

## 用法

先固定版本，再在独立环境打开入门文件（命令未在本轮执行）：

```bash
git clone https://github.com/langchain-ai/rag-from-scratch.git
cd rag-from-scratch
git checkout 1fdb7d0e4f1d3e731c8397332452715512f18667
python -m venv .venv
```

在选用的 Jupyter 环境打开 `rag_from_scratch_1_to_4.ipynb`，先检查安装与凭据单元，逐个执行，不要直接 Run All。Notebook 中 `<your-api-key>` 是要替换的示意占位，不是有效 Python 表达式；实际实验应从受控环境变量读取，并避免把 key 保存进 Notebook 或输出。

教学单元直接 `pip install` 多个未锁版本的 LangChain / Chroma 依赖。应先确认兼容组合、形成独立环境记录，再按 1–4、5–9、10–11、12–14、15–18 学习。README 提供[原始播放列表](https://www.youtube.com/playlist?list=PLfaIDFEXuae2LXbO1_PKyVJiQ23ZztA0x)，不需先接生产知识库。

## 原理

入门示例从公开网页加载文档，按字符或 token 切块并重叠，用 `OpenAIEmbeddings` 生成向量、Chroma 建索引；retriever 返回片段，将上下文和问题送入提示词，再调用聊天模型、解析文本。

后续 Notebook 对“查什么、从哪里查、怎样组织检索结果”逐层扩展；本轮采读 1–4 与 15–18 文件，不声称完整逐单元运行。入门代码使用历史 `gpt-3.5-turbo` 名称、旧 LangChain 导入与动态 `hub.pull("rlm/rag-prompt")`，主线内容固定不代表远端模型、包和 prompt 也固定。

## 价值

适合用小而可检查的材料理解 chunk、embedding、retriever、prompt 与生成之间的数据流，也能做检索方案的课堂对照。代码和视频相互对应，便于定位问题在检索还是生成。

“从零”指循序解释 RAG 流程，不是从零实现向量库或训练模型；单篇博客演示不能代表大规模、多租户或受限资料的效果。

## 风险边界

- 示例显式设置 `LANGCHAIN_TRACING_V2=true` 和 LangSmith endpoint；还调用远端 embeddings / chat，后续文件包含 Cohere key 配置。本地 Chroma 不保证资料、问题或生成内容只留本机。
- 依赖未锁、旧 API 和模型名可能已不可直接使用；本轮只确认源码写法，没有验证当前服务可用性或迁移后的等价性。
- 远端网页、Hub prompt 和模型响应会变。复现须保存获授权的资料快照、prompt 版本、依赖和模型标识。
- 提示词要求按上下文回答，不会自动阻止幻觉、检索漏召回或文档注入；教程不自带生产 ACL、隔离、成本上限和可靠拒答保证。
- 无明确根许可时，先确认使用 / 再分发权；视频播放量也不能作为教程当前可运行或方法更优的证据。

## 补充建议

用可公开、可手工标注的十余个问题先量 recall@k、引用支持、正确拒答、费用与延迟。分别比较未检索、基础 RAG 与一个改进，不要一次叠加所有技术。处理私人资料前先关闭不需要的 tracing，并检查全链路数据出口和数据使用许可。

本轮核完整六文件目录树、README 与两份 Notebook 源码、视频元数据；未安装依赖、执行单元、调用模型或完整观看课程。

## 参考资料

- [课程说明与配套视频](https://github.com/langchain-ai/rag-from-scratch/blob/1fdb7d0e4f1d3e731c8397332452715512f18667/README.md)。
- [入门索引、检索、生成与 tracing](https://github.com/langchain-ai/rag-from-scratch/blob/1fdb7d0e4f1d3e731c8397332452715512f18667/rag_from_scratch_1_to_4.ipynb)。
- [后续检索流程和 provider 配置](https://github.com/langchain-ai/rag-from-scratch/blob/1fdb7d0e4f1d3e731c8397332452715512f18667/rag_from_scratch_15_to_18.ipynb)。
