<!-- markdownlint-disable MD013 -->

# FreeToken

- 主上游：[FlashML-org/FreeToken](https://github.com/FlashML-org/FreeToken)
- 分类：模型、训练与推理基础设施。
- 核验日期：2026-11-02（Asia/Shanghai）；默认分支 `main`，固定快照 `ee43b2a11345`。
- [API](https://api.github.com/repos/FlashML-org/FreeToken) 快照：15,362 stars / 1,548 forks / 470 open issues（含 PR）；发行列表首项 [nightly](https://github.com/FlashML-org/FreeToken/releases/tag/nightly)（UTC 2026-09-09，预发行 / 滚动标签）。累计量不是今日增量，主线不等于发行包。

## 定位

FreeToken 是面向消费级硬件的 MoE 模型推理与服务引擎，将 GPU、CPU、主机内存和互连带宽一起调度，提供本地聊天与编码客户端接口。“290B+”描述可承载模型规模，不代表所有参数同时驻留显存，也不代表任何个人电脑都有交互速度。[README.md](https://github.com/FlashML-org/FreeToken/blob/ee43b2a11345d056ba349d22ee073c6828b1364b/README.md)

## 用法

当前 CLI 主安装路线要求 Linux x86_64、NVIDIA GPU、r580+ 驱动 / CUDA 13 与 Python ≥3.10；初次 JIT 还需 `nvcc`。README 的 Windows / Linux 桌面应用是另一入口，AMD 文档标为 WIP；不能据此推定 macOS CLI 可用。[docs/install.md](https://github.com/FlashML-org/FreeToken/blob/ee43b2a11345d056ba349d22ee073c6828b1364b/docs/install.md)、[README.md](https://github.com/FlashML-org/FreeToken/blob/ee43b2a11345d056ba349d22ee073c6828b1364b/README.md)

```sh
uv venv
source .venv/bin/activate
uv pip install "freetoken[accel]"
ft --version
ft serve --model ~/models/Qwen3.6-35B-A3B
curl http://127.0.0.1:1919/v1/models
```

本轮核到 PyPI 0.2.1；上例沿用上游不固定版本的命令，正式试验应锁 runtime、kernel-cache wheel 与模型 revision。先看 `ft launch claude --dry-run` 的配置变化，再决定是否接入已有客户端；`ft launch` 会写 provider 配置，CLI 缺失时还可安装它。[docs/quickstart.md](https://github.com/FlashML-org/FreeToken/blob/ee43b2a11345d056ba349d22ee073c6828b1364b/docs/quickstart.md)、[docs/install.md](https://github.com/FlashML-org/FreeToken/blob/ee43b2a11345d056ba349d22ee073c6828b1364b/docs/install.md)

## 原理

上游设计包括带宽自适应 CPU–GPU 协同、双缓冲 prefill、LRU expert cache、FTW 权重格式与专家 / KV 显存动态分配。利用 MoE 稀疏激活，把有限显存留给更常用专家和上下文；语义 anchor cache 则面向工具调用等上下文编辑后的缓存复用。支持 OpenAI / Anthropic 形式的 API 不意味着每个客户端或工具调用行为都已兼容。[README.md](https://github.com/FlashML-org/FreeToken/blob/ee43b2a11345d056ba349d22ee073c6828b1364b/README.md)、[docs/cli.md](https://github.com/FlashML-org/FreeToken/blob/ee43b2a11345d056ba349d22ee073c6828b1364b/docs/cli.md)

## 价值

适合评估“大模型权重可放入 RAM、显存较小但有独立 GPU”的本地推理路线。应与相同模型、量化、上下文、批量和硬件的基线比较首 token 延迟、decode 吞吐、RAM / VRAM 峰值及长任务正确性；本轮未复现作者或视频性能结论。

## 风险边界

- serve 默认 `127.0.0.1:1919`；API key 默认从环境取，未设置即不认证。配置后除 `/health` 外检查 key。daemon 是另一控制面，默认 `127.0.0.1:1900`，其 `X-FT-Token` 另配；不能只保护推理口。[docs/cli.md](https://github.com/FlashML-org/FreeToken/blob/ee43b2a11345d056ba349d22ee073c6828b1364b/docs/cli.md)、[python/freetoken/server/api_server.py](https://github.com/FlashML-org/FreeToken/blob/ee43b2a11345d056ba349d22ee073c6828b1364b/python/freetoken/server/api_server.py)、[python/freetoken/daemon/server.py](https://github.com/FlashML-org/FreeToken/blob/ee43b2a11345d056ba349d22ee073c6828b1364b/python/freetoken/daemon/server.py)
- 滚动 `nightly` 的发布时间不是当前 wheel 构建时间；标签会移动，需锁带 SHA 的 wheel URL 及匹配缓存包。PyPI 版本与本页主线快照也不可混用为复现实验身份。[docs/install.md](https://github.com/FlashML-org/FreeToken/blob/ee43b2a11345d056ba349d22ee073c6828b1364b/docs/install.md)
- 大参数量仍消耗主机内存、磁盘与 PCIe 带宽；缓存命中、量化、长上下文和并发会改变速度。模型下载、客户端工具与 provider 配置也有独立数据出口。[README.md](https://github.com/FlashML-org/FreeToken/blob/ee43b2a11345d056ba349d22ee073c6828b1364b/README.md)、[docs/cli.md](https://github.com/FlashML-org/FreeToken/blob/ee43b2a11345d056ba349d22ee073c6828b1364b/docs/cli.md)
- 根代码 Apache-2.0；权重、上游组件及桌面制品分别核验，不能由代码许可推导模型使用权。[LICENSE](https://github.com/FlashML-org/FreeToken/blob/ee43b2a11345d056ba349d22ee073c6828b1364b/LICENSE)

## 补充建议

先固定一个可容纳的 MoE 模型跑离线短请求，再增加上下文和并发；记录权重格式、RAM、GPU / 驱动、互连带宽、prefill / decode 分别耗时与 Agent 任务成功率。保留原客户端配置及 dry-run 结果。本轮未安装引擎、改 provider、启动 daemon 或调用模型。

## 参考资料

- [README.md](https://github.com/FlashML-org/FreeToken/blob/ee43b2a11345d056ba349d22ee073c6828b1364b/README.md)（固定 commit）。
- [docs/install.md](https://github.com/FlashML-org/FreeToken/blob/ee43b2a11345d056ba349d22ee073c6828b1364b/docs/install.md)（固定 commit）。
- [docs/quickstart.md](https://github.com/FlashML-org/FreeToken/blob/ee43b2a11345d056ba349d22ee073c6828b1364b/docs/quickstart.md)（固定 commit）。
- [docs/cli.md](https://github.com/FlashML-org/FreeToken/blob/ee43b2a11345d056ba349d22ee073c6828b1364b/docs/cli.md)（固定 commit）。
- [python/freetoken/server/api_server.py](https://github.com/FlashML-org/FreeToken/blob/ee43b2a11345d056ba349d22ee073c6828b1364b/python/freetoken/server/api_server.py)（固定 commit）。
- [python/freetoken/daemon/server.py](https://github.com/FlashML-org/FreeToken/blob/ee43b2a11345d056ba349d22ee073c6828b1364b/python/freetoken/daemon/server.py)（固定 commit）。
- [LICENSE](https://github.com/FlashML-org/FreeToken/blob/ee43b2a11345d056ba349d22ee073c6828b1364b/LICENSE)（固定 commit）。
- [仓库 API](https://api.github.com/repos/FlashML-org/FreeToken)、[发行列表](https://github.com/FlashML-org/FreeToken/releases)（动态状态）。
- [PyPI 0.2.1](https://pypi.org/project/freetoken/0.2.1/)。
