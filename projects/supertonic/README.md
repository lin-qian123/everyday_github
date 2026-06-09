# supertonic

## 项目定位

- GitHub：<https://github.com/supertone-inc/supertonic>
- 定位：离线可运行、低延迟、多语言 TTS（文本转语音）系统，基于 ONNX 生态。
- 当前信号（2026-05-16 抓取）：约 6k stars。

## 用法

### Python 快速开始

```bash
pip install supertonic
```

- 首次运行会拉取模型资产（Hugging Face）。
- 适合本地工具、桌面应用、浏览器端 TTS 集成实验。

## 原理

- **推理后端**：ONNX Runtime（跨平台推理）。
- **浏览器侧**：onnxruntime-web（前端本地推理能力）。
- **模型策略**：在参数规模与语音质量之间折中，优先实用部署效率。

## 价值

- 对隐私敏感场景可用本地推理，避免文本上传云端。
- 在多终端（桌面/浏览器/边缘设备）上具备较低集成成本。

## 风险边界

- 多语言覆盖不代表各语言体验一致，长文本与专有名词需单测。
- 本地推理效果受硬件差异影响明显。
- 若依赖外部模型仓库拉取资产，需要额外考虑可用性与缓存策略。

## 补充建议

- 建立目标语言的对比测试集（准确率、韵律、延迟）。
- 结合业务场景做分层：高实时场景优先短句，长文转写走异步管道。
- 对模型和运行时版本固定，避免“隐式升级”导致音色漂移。

## 参考资料

- GitHub 仓库：<https://github.com/supertone-inc/supertonic>
- 文档主页：<https://supertone-inc.github.io/supertonic/>
