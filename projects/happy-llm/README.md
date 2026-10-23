<!-- markdownlint-disable MD013 -->

# happy-llm

- 主上游：[datawhalechina/happy-llm](https://github.com/datawhalechina/happy-llm)
- 分类：AI 学习与教育资源。
- 核验日期：2026-10-24（Asia/Shanghai）；默认分支 `main` 快照 `1e0b3a1e6f89`。
- [API](https://api.github.com/repos/datawhalechina/happy-llm) 快照：34,527 stars / 3,268 forks / 75 open issues；发行列表首项 [v1.0.2](https://github.com/datawhalechina/happy-llm/releases/tag/v1.0.2)（UTC 2026-01-29，正式）。累计量不是今日增长，主线也不等于发行版。

## 定位

Happy-LLM 是 Datawhale 中文大模型教程，从 NLP / Transformer / 预训练原理，延伸到手写模型、框架训练、RAG / Agent 和 Agentic RL。面向具备 Python 与深度学习基础的学习者；不是训练即达到工业模型质量的配方。 [README.md](https://github.com/datawhalechina/happy-llm/blob/1e0b3a1e6f8936b8ba4bbd0673e8e2227d196c96/README.md)

## 用法

先读第 1–4 章，再按目标选第 5 章手写实现或第 6 章框架训练。依赖按章节安装；第 2–7 章文档建议 Python 3.10 / 3.11，第 8 章为独立 Python 3.13 环境。以下仅是第六章环境入口：

```sh
python -m venv .venv
source .venv/bin/activate
python -m pip install -r docs/chapter6/code/requirements.txt
```

先阅读实践说明，调整示例磁盘路径、GPU 编号与 DeepSpeed 配置，再做小数据单步训练。PDF 正式发行 v1.0.2 与当前主线内容不是同一更新时间。 [docs/学习与环境准备.md](https://github.com/datawhalechina/happy-llm/blob/1e0b3a1e6f8936b8ba4bbd0673e8e2227d196c96/docs/学习与环境准备.md)、[docs/chapter6/readme.md](https://github.com/datawhalechina/happy-llm/blob/1e0b3a1e6f8936b8ba4bbd0673e8e2227d196c96/docs/chapter6/readme.md)

## 原理

以理论正文、章节代码和实践步骤连接 Tokenizer、Transformer、预训练 / SFT / PEFT、检索与工具调用。当前第八章通过 PyTRIO 在远端执行采样与参数更新，本地处理数据、环境交互和训练调度。 [README.md](https://github.com/datawhalechina/happy-llm/blob/1e0b3a1e6f8936b8ba4bbd0673e8e2227d196c96/README.md)、[docs/学习与环境准备.md](https://github.com/datawhalechina/happy-llm/blob/1e0b3a1e6f8936b8ba4bbd0673e8e2227d196c96/docs/学习与环境准备.md)

## 价值

优势是中文循序讲解与可追溯的代码入口，适合用小模型理解训练链路，并把 RAG / Agent 与底层模型连接起来。完成教程和获得研究结论仍需要独立数据、基线、消融与统计复核。

## 风险边界

- “本地 CPU 可学习第八章”依赖远端账号、网络和计费额度，不表示训练免费或在 CPU 本地完成。ReTool 会执行模型生成的 Python；文档明确配套 sandbox 只限制部分资源，需另外提供可信隔离并移除凭证。 [docs/学习与环境准备.md](https://github.com/datawhalechina/happy-llm/blob/1e0b3a1e6f8936b8ba4bbd0673e8e2227d196c96/docs/学习与环境准备.md)
- 不同章节、SDK、模型与数据集版本不同，不能一次安装全仓库依赖就认为可复现。PDF / 主线 / 配套 PPT / 外部实验仓库也应分别标版本。 [README.md](https://github.com/datawhalechina/happy-llm/blob/1e0b3a1e6f8936b8ba4bbd0673e8e2227d196c96/README.md)
- 根作品许可为 CC BY-NC-SA 4.0，存在非商业与相同方式共享条件；书中引用、数据、外部模型和独立配套仓库需另核。 [LICENSE.txt](https://github.com/datawhalechina/happy-llm/blob/1e0b3a1e6f8936b8ba4bbd0673e8e2227d196c96/LICENSE.txt)

## 补充建议

先完成小模型前向 / 反向传播的可解释检查，再以少量数据跑通保存、重载与评测；第八章保持小 batch / 短轨迹并记录真实远端费用。区分阅读完成、代码运行和结果复现。本轮未训练、下载数据 / 权重、创建远端账号或调用服务。

## 参考资料

- [README.md](https://github.com/datawhalechina/happy-llm/blob/1e0b3a1e6f8936b8ba4bbd0673e8e2227d196c96/README.md)（固定 commit）。
- [docs/学习与环境准备.md](https://github.com/datawhalechina/happy-llm/blob/1e0b3a1e6f8936b8ba4bbd0673e8e2227d196c96/docs/学习与环境准备.md)（固定 commit）。
- [docs/chapter6/readme.md](https://github.com/datawhalechina/happy-llm/blob/1e0b3a1e6f8936b8ba4bbd0673e8e2227d196c96/docs/chapter6/readme.md)（固定 commit）。
- [LICENSE.txt](https://github.com/datawhalechina/happy-llm/blob/1e0b3a1e6f8936b8ba4bbd0673e8e2227d196c96/LICENSE.txt)（固定 commit）。
- [发行列表](https://github.com/datawhalechina/happy-llm/releases)、[仓库 API](https://api.github.com/repos/datawhalechina/happy-llm)（动态状态）。
