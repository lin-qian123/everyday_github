<!-- markdownlint-disable MD013 -->

# moonshine

- 主上游：[moonshine-ai/moonshine](https://github.com/moonshine-ai/moonshine)
- 分类：语音、视频与多模态。
- 核验日期：2026-11-02（Asia/Shanghai）；默认分支 `main`，固定快照 `234f60faa0eb`。
- [API](https://api.github.com/repos/moonshine-ai/moonshine) 快照：11,370 stars / 641 forks / 18 open issues（含 PR）；发行列表首项 [v0.1.5](https://github.com/moonshine-ai/moonshine/releases/tag/v0.1.5)（UTC 2026-08-24）。累计量不是今日增量，主线不等于发行包。

## 定位

Moonshine Voice 是面向实时语音界面的端侧工具包，包含流式语音识别、意图识别与语音合成等路径，并提供多平台绑定。其“小模型低延迟”目标需按语言、架构与设备验证，不能把 README 的英文识别比较当作中文或完整语音 Agent 的结论。[README.md](https://github.com/moonshine-ai/moonshine/blob/234f60faa0eb388b01cdf7e60aca232af37aefda/README.md)、[docs/models/available-models.md](https://github.com/moonshine-ai/moonshine/blob/234f60faa0eb388b01cdf7e60aca232af37aefda/docs/models/available-models.md)

## 用法

Python 路线的 PyPI / 包元数据当前为 0.1.5、Python ≥3.8，需设备麦克风权限：

```sh
python -m pip install "moonshine-voice==0.1.5"
moonshine-voice mic --language en
```

先用已获授权的非敏感语音；首次高层 `load()` 通常自动下载模型，离线前应预热缓存或打包 assets。换语言前查当前版本的模型目录，明确 streaming / non-streaming 与默认架构。[docs/quickstart.md](https://github.com/moonshine-ai/moonshine/blob/234f60faa0eb388b01cdf7e60aca232af37aefda/docs/quickstart.md)、[docs/using/downloading-models.md](https://github.com/moonshine-ai/moonshine/blob/234f60faa0eb388b01cdf7e60aca232af37aefda/docs/using/downloading-models.md)、[language-bindings/python/pyproject.toml](https://github.com/moonshine-ai/moonshine/blob/234f60faa0eb388b01cdf7e60aca232af37aefda/language-bindings/python/pyproject.toml)

## 原理

识别过程在用户仍讲话时增量计算，降低等待完整录音后的处理延迟。模型目录以 ONNX 转换的可内存映射 `.ort` 格式分发；高层辅助类可按依赖目录下载，低层 from-files / assets 路径可使用预置文件。STT、TTS、会话逻辑及调用的业务动作需分别配置。[README.md](https://github.com/moonshine-ai/moonshine/blob/234f60faa0eb388b01cdf7e60aca232af37aefda/README.md)、[docs/models/available-models.md](https://github.com/moonshine-ai/moonshine/blob/234f60faa0eb388b01cdf7e60aca232af37aefda/docs/models/available-models.md)、[docs/using/downloading-models.md](https://github.com/moonshine-ai/moonshine/blob/234f60faa0eb388b01cdf7e60aca232af37aefda/docs/using/downloading-models.md)

## 价值

适合本地听写、嵌入式语音入口和需要降低云转写依赖的应用。当前模型表列 Mandarin Tiny Streaming 为 34M、16.1% 无空格 CER，属于作者指定 400-clip panel，不能与英文八数据集平均 WER、旧完整 FLEURS 或量化部署结果直接比较。[docs/models/available-models.md](https://github.com/moonshine-ai/moonshine/blob/234f60faa0eb388b01cdf7e60aca232af37aefda/docs/models/available-models.md)

## 风险边界

- 根 LICENSE 明示代码主体和默认 STT 模型 MIT，但第三方代码另看。历史非英语 non-streaming 模型中的指定 Arabic / Japanese / Korean / Mandarin / Spanish / Ukrainian / Vietnamese 型号仍为非商业 Community License；TTS / G2P 资产又有独立上游条款。不是“整个库全部模型 MIT”。[LICENSE](https://github.com/moonshine-ai/moonshine/blob/234f60faa0eb388b01cdf7e60aca232af37aefda/LICENSE)、[core/moonshine-tts/data/README.md](https://github.com/moonshine-ai/moonshine/blob/234f60faa0eb388b01cdf7e60aca232af37aefda/core/moonshine-tts/data/README.md)
- 端侧推理不覆盖首次下载、CDN、浏览器 demo 或应用自行增加的云模型。Python 缓存与浏览器 Cache Storage 路径不同，语音保留和业务日志也要由应用单独控制。[docs/using/downloading-models.md](https://github.com/moonshine-ai/moonshine/blob/234f60faa0eb388b01cdf7e60aca232af37aefda/docs/using/downloading-models.md)
- 模型表已有明确不可比的语言 / 数据集 / 指标与量化条件；口音、噪声、打断、分段和幻觉需现场测。包仍标 Alpha，主线 API 与既有应用的旧接口不可混用。[docs/models/available-models.md](https://github.com/moonshine-ai/moonshine/blob/234f60faa0eb388b01cdf7e60aca232af37aefda/docs/models/available-models.md)、[language-bindings/python/pyproject.toml](https://github.com/moonshine-ai/moonshine/blob/234f60faa0eb388b01cdf7e60aca232af37aefda/language-bindings/python/pyproject.toml)

## 补充建议

以固定语言 / 模型 revision 和授权语料测 CER 或 WER、分段尾延迟、实时率、内存、静音误触发；单独做冷启动下载失败和断网推理测试。TTS 补核语音 / 词典资产许可。本轮未安装、采音、下载模型或评测准确率。

## 参考资料

- [README.md](https://github.com/moonshine-ai/moonshine/blob/234f60faa0eb388b01cdf7e60aca232af37aefda/README.md)（固定 commit）。
- [docs/quickstart.md](https://github.com/moonshine-ai/moonshine/blob/234f60faa0eb388b01cdf7e60aca232af37aefda/docs/quickstart.md)（固定 commit）。
- [docs/models/available-models.md](https://github.com/moonshine-ai/moonshine/blob/234f60faa0eb388b01cdf7e60aca232af37aefda/docs/models/available-models.md)（固定 commit）。
- [docs/using/downloading-models.md](https://github.com/moonshine-ai/moonshine/blob/234f60faa0eb388b01cdf7e60aca232af37aefda/docs/using/downloading-models.md)（固定 commit）。
- [language-bindings/python/pyproject.toml](https://github.com/moonshine-ai/moonshine/blob/234f60faa0eb388b01cdf7e60aca232af37aefda/language-bindings/python/pyproject.toml)（固定 commit）。
- [LICENSE](https://github.com/moonshine-ai/moonshine/blob/234f60faa0eb388b01cdf7e60aca232af37aefda/LICENSE)（固定 commit）。
- [core/moonshine-tts/data/README.md](https://github.com/moonshine-ai/moonshine/blob/234f60faa0eb388b01cdf7e60aca232af37aefda/core/moonshine-tts/data/README.md)（固定 commit）。
- [仓库 API](https://api.github.com/repos/moonshine-ai/moonshine)、[发行列表](https://github.com/moonshine-ai/moonshine/releases)（动态状态）。
- [PyPI 0.1.5](https://pypi.org/project/moonshine-voice/0.1.5/)。
