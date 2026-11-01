<!-- markdownlint-disable MD013 -->

# LiteRT-LM

- 主上游：[google-ai-edge/LiteRT-LM](https://github.com/google-ai-edge/LiteRT-LM)
- 分类：模型、训练与推理基础设施。
- 核验日期：2026-11-02（Asia/Shanghai）；默认分支 `main`，固定快照 `b91a4d7b38be`。
- [API](https://api.github.com/repos/google-ai-edge/LiteRT-LM) 快照：6,797 stars / 776 forks / 748 open issues（含 PR）；发行列表首项 [v0.19.0](https://github.com/google-ai-edge/LiteRT-LM/releases/tag/v0.19.0)（UTC 2026-10-30）。累计量不是今日增量，主线不等于发行包。

## 定位

LiteRT-LM 是 Google 在 LiteRT 之上运行大语言模型的编排层，面向手机、Web、桌面和 IoT，提供多语言 API、硬件后端、多模态与工具调用。README 的 production-ready 是作者产品定位；具体绑定与后端仍各有状态和约束。[README.md](https://github.com/google-ai-edge/LiteRT-LM/blob/b91a4d7b38beb07025c24b6af2ec119bba14369f/README.md)

## 用法

PyPI / 正式发行当前均为 0.19.0。CLI 可通过 uv 安装，然后加载已取得访问权的适配模型：

```sh
uv tool install "litert-lm==0.19.0"
litert-lm run \
  --from-huggingface-repo=google/gemma-3n-E2B-it-litert-lm \
  gemma-3n-E2B-it-int4 \
  --prompt="What is the capital of France?"
```

模型可能要求先接受许可并登录 Hugging Face；仓库名和文件名需以该模型当前清单为准。源码构建按官方指南 checkout 稳定 tag，再核 LFS、Bazel 和平台工具链；不能只 clone 主线便认为与发行包同一身份。[README.md](https://github.com/google-ai-edge/LiteRT-LM/blob/b91a4d7b38beb07025c24b6af2ec119bba14369f/README.md)、[docs/getting-started/build-and-run.md](https://github.com/google-ai-edge/LiteRT-LM/blob/b91a4d7b38beb07025c24b6af2ec119bba14369f/docs/getting-started/build-and-run.md)

## 原理

编排 tokenizer、模型数据处理、会话、生成与 LiteRT 执行后端。v0.19.0 的更新包括 GPU logit masking、MTP 相关解码、Web 流式模型加载，以及若干 ASR / TTS 模型接入；这是不同组件的能力，不能直接合成端到端应用性能承诺。[README.md](https://github.com/google-ai-edge/LiteRT-LM/blob/b91a4d7b38beb07025c24b6af2ec119bba14369f/README.md)

## 价值

适合将适配过的 LLM 放入原生或浏览器应用，并复用 Python / Kotlin / C++ 等接口。README 将这些接口列为稳定，Swift 与 JavaScript 仍为 Early Preview、Flutter 为社区维护；需按目标平台选取交付范围。[README.md](https://github.com/google-ai-edge/LiteRT-LM/blob/b91a4d7b38beb07025c24b6af2ec119bba14369f/README.md)

## 风险边界

- v0.19.0 的 C API 1.0.0 有破坏性变更：可失败函数返回状态码，结果经 out 参数传回，导出符号统一前缀。现有 FFI / 插件不能只换动态库而忽略绑定版本。[README.md](https://github.com/google-ai-edge/LiteRT-LM/blob/b91a4d7b38beb07025c24b6af2ec119bba14369f/README.md)
- 主线 CLI serve 默认 `127.0.0.1:9379`、OpenAI 协议，CORS 默认关闭；这些是监听 / 浏览器策略，不能视为跨机调用认证。此结论只来自当前入口源码，未完成全部 handler 的安全审计。[python/litert_lm_cli/commands/serve/module.py](https://github.com/google-ai-edge/LiteRT-LM/blob/b91a4d7b38beb07025c24b6af2ec119bba14369f/python/litert_lm_cli/commands/serve/module.py)
- 模型格式、GPU / NPU 支持与工具调用能力按具体模型 / 设备核验。函数调用生成仍需业务权限和参数校验，模型缓存与可选应用网络另管。根代码 Apache-2.0 不替代 Gemma 等模型条款。[README.md](https://github.com/google-ai-edge/LiteRT-LM/blob/b91a4d7b38beb07025c24b6af2ec119bba14369f/README.md)、[LICENSE](https://github.com/google-ai-edge/LiteRT-LM/blob/b91a4d7b38beb07025c24b6af2ec119bba14369f/LICENSE)

## 补充建议

固定 SDK、模型文件 / 量化、设备与后端；先测纯文本，再测图像 / 音频与工具调用。分别记录冷加载、首 token、持续吞吐、峰值内存、耗电和热降频，升级时增加 C API 错误路径验证。本轮未安装 SDK、构建源码、下载模型、启动服务或测性能。

## 参考资料

- [README.md](https://github.com/google-ai-edge/LiteRT-LM/blob/b91a4d7b38beb07025c24b6af2ec119bba14369f/README.md)（固定 commit）。
- [docs/getting-started/build-and-run.md](https://github.com/google-ai-edge/LiteRT-LM/blob/b91a4d7b38beb07025c24b6af2ec119bba14369f/docs/getting-started/build-and-run.md)（固定 commit）。
- [python/litert_lm_cli/commands/serve/module.py](https://github.com/google-ai-edge/LiteRT-LM/blob/b91a4d7b38beb07025c24b6af2ec119bba14369f/python/litert_lm_cli/commands/serve/module.py)（固定 commit）。
- [LICENSE](https://github.com/google-ai-edge/LiteRT-LM/blob/b91a4d7b38beb07025c24b6af2ec119bba14369f/LICENSE)（固定 commit）。
- [仓库 API](https://api.github.com/repos/google-ai-edge/LiteRT-LM)、[发行列表](https://github.com/google-ai-edge/LiteRT-LM/releases)（动态状态）。
- [PyPI 0.19.0](https://pypi.org/project/litert-lm/0.19.0/)。
