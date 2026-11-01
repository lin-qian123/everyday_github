<!-- markdownlint-disable MD013 -->

# ai-engineering-hub

- 主上游：[patchy631/ai-engineering-hub](https://github.com/patchy631/ai-engineering-hub)
- 分类：AI 学习与教育资源。
- 核验日期：2026-11-02（Asia/Shanghai）；默认分支 `main`，固定快照 `042aeb506738`。
- [API](https://api.github.com/repos/patchy631/ai-engineering-hub) 快照：40,181 stars / 6,480 forks / 133 open issues（含 PR）；发行列表当前为空。累计量不是今日增量，主线不等于发行包。

## 定位

AI Engineering Hub 是按难度组织的 LLM、RAG、多模态与 Agent 教程集合，当前首页自述 93+ 项目。它便于寻找具体练习的最小实现；“production-ready”是作者描述，本轮只抽查 Simple RAG 与评估目录，未逐项验收。[README.md](https://github.com/patchy631/ai-engineering-hub/blob/042aeb5067384981eeba6a07fa882f436bb1660d/README.md)

## 用法

先选一个目录，按各自 README 创建独立环境和依赖锁，不要尝试一次安装全库。Simple RAG 路线先准备 Ollama 与 `llama3.2`，再执行对应 notebook / 脚本：

```sh
git clone https://github.com/patchy631/ai-engineering-hub.git
cd ai-engineering-hub
git checkout 042aeb5067384981eeba6a07fa882f436bb1660d
cd simple-rag-workflow
ollama pull llama3.2
ollama serve
```

另一个终端配置与该示例兼容的 LlamaIndex、Ollama、Hugging Face embedding、nest_asyncio 等依赖后，再运行 `python workflow.py`。此处不编造上游没有提供的完整版本锁；README 的“Llama 2”文字与实际 `llama3.2` 命令不一致，以代码与实际模型核对。[simple-rag-workflow/README.md](https://github.com/patchy631/ai-engineering-hub/blob/042aeb5067384981eeba6a07fa882f436bb1660d/simple-rag-workflow/README.md)、[simple-rag-workflow/workflow.py](https://github.com/patchy631/ai-engineering-hub/blob/042aeb5067384981eeba6a07fa882f436bb1660d/simple-rag-workflow/workflow.py)

## 原理

抽查脚本由 LlamaIndex Workflow 将摄入、检索、生成拆为异步 step：SimpleDirectoryReader 读文件，Hugging Face BGE 建向量，top-k=2 检索，Ollama 生成，CompactAndRefine 流式合成。索引存入对象状态，`Settings` 修改全局 LLM / embedding；这不是多租户持久知识服务。[simple-rag-workflow/workflow.py](https://github.com/patchy631/ai-engineering-hub/blob/042aeb5067384981eeba6a07fa882f436bb1660d/simple-rag-workflow/workflow.py)

## 价值

适合通过短链路理解数据如何进入检索与回答，再对比有观测 / 评估的示例。学习路径可以是固定一份文档、准备有证据的十个问题，再量化检索召回和回答引用，逐步接入更复杂 Agent。

## 风险边界

- Simple RAG 的模型 / API 配置与目录 `.env.example` 的 OpenAI key 占位不同；不能把一个模板字段当作该脚本必需凭据，也不能从一个本地示例推定所有教程离线。[simple-rag-workflow/.env.example](https://github.com/patchy631/ai-engineering-hub/blob/042aeb5067384981eeba6a07fa882f436bb1660d/simple-rag-workflow/.env.example)、[simple-rag-workflow/workflow.py](https://github.com/patchy631/ai-engineering-hub/blob/042aeb5067384981eeba6a07fa882f436bb1660d/simple-rag-workflow/workflow.py)
- `eval-and-observability` 明示需要 Opik 与 OpenAI API key，涉及服务端调用和评估数据流；上云前核数据、日志、费用和 provider 配置。[eval-and-observability/README.md](https://github.com/patchy631/ai-engineering-hub/blob/042aeb5067384981eeba6a07fa882f436bb1660d/eval-and-observability/README.md)
- 教程依赖与旧模型会漂移；文档说“最快”“可信”“企业级”不等于有同条件性能、权限、隔离和恢复验收。BGE 英文默认与中文任务也需实测。[README.md](https://github.com/patchy631/ai-engineering-hub/blob/042aeb5067384981eeba6a07fa882f436bb1660d/README.md)、[simple-rag-workflow/workflow.py](https://github.com/patchy631/ai-engineering-hub/blob/042aeb5067384981eeba6a07fa882f436bb1660d/simple-rag-workflow/workflow.py)
- 根代码 MIT；模型、PDF 样本、外部 API、数据和赞助服务分别核授权，仓库许可不统一覆盖这些资产。[LICENSE](https://github.com/patchy631/ai-engineering-hub/blob/042aeb5067384981eeba6a07fa882f436bb1660d/LICENSE)

## 补充建议

只选一条链路建立环境锁、输入 hash、检索片段与输出记录；再加空索引、不可回答问题、失败重试及独立验证集。上游示例安装脚本也应先检查来源与平台适用性。本轮未安装、运行 notebook、调用模型或向观测服务上传数据。

## 参考资料

- [README.md](https://github.com/patchy631/ai-engineering-hub/blob/042aeb5067384981eeba6a07fa882f436bb1660d/README.md)（固定 commit）。
- [simple-rag-workflow/README.md](https://github.com/patchy631/ai-engineering-hub/blob/042aeb5067384981eeba6a07fa882f436bb1660d/simple-rag-workflow/README.md)（固定 commit）。
- [simple-rag-workflow/workflow.py](https://github.com/patchy631/ai-engineering-hub/blob/042aeb5067384981eeba6a07fa882f436bb1660d/simple-rag-workflow/workflow.py)（固定 commit）。
- [simple-rag-workflow/.env.example](https://github.com/patchy631/ai-engineering-hub/blob/042aeb5067384981eeba6a07fa882f436bb1660d/simple-rag-workflow/.env.example)（固定 commit）。
- [eval-and-observability/README.md](https://github.com/patchy631/ai-engineering-hub/blob/042aeb5067384981eeba6a07fa882f436bb1660d/eval-and-observability/README.md)（固定 commit）。
- [LICENSE](https://github.com/patchy631/ai-engineering-hub/blob/042aeb5067384981eeba6a07fa882f436bb1660d/LICENSE)（固定 commit）。
- [仓库 API](https://api.github.com/repos/patchy631/ai-engineering-hub)、[发行列表](https://github.com/patchy631/ai-engineering-hub/releases)（动态状态）。
