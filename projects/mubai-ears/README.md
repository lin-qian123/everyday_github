# mubai-ears

## 定位

`mubai-ears` 是本地优先的语音输入预处理工具：以 Whisper 转写获得带时间戳文本，并把梅尔频谱、基频、能量、停顿和语速做成图像及 JSON 摘要，供多模态 AI 伴侣理解“说了什么”与部分韵律特征。

截至 2026-07-31，GitHub API 快照显示它创建于 2026-07-30，约 18 stars、3 forks，MIT 许可证；这只是早期信号，不能证明情绪识别的准确性。

## 用法

安装依赖与 FFmpeg 后，分别生成声音形态摘要和本地转写。首次转写会下载模型权重。

```bash
git clone https://github.com/hmh323/mubai-ears.git
cd mubai-ears
pip install -r requirements.txt
python cochlea.py recording.m4a
python transcribe.py recording.m4a base
```

输出位于 `out/<文件名>/`：`listen.png`、`summary.json` 与 `transcript.json`。只应把经同意的材料交给后续模型。

## 原理

工具用本地解码与特征提取把连续音频压缩成模型可读取的视觉/数值证据，再以 faster-whisper 生成文本。它分析的是声学相关量，而不是直接测量人的情绪或意图。

## 价值

- 在本机完成转写和韵律预处理，减少把原始音频直接上传的需要。
- 为语音日记、可访问性辅助和语音交互调试提供时间对齐的可复核产物。

## 风险边界

- 音高、能量和停顿不能可靠推出情绪、心理状态或真实性；不得用于诊断、监控、雇佣或高风险决策。
- 本地处理不自动解决录音同意、共享、备份和模型下载产生的隐私义务。
- 转写错误、方言、噪声和跨文化语用都会使下游判断偏移。

## 补充建议

默认最小化保存原音频，明确保留期与删除流程；将摘要视作辅助线索而非人物画像。用已获同意的多口音、噪声和静音样本测试转写与特征稳定性。

## 参考资料

- GitHub：<https://github.com/hmh323/mubai-ears>
- GitHub API 快照：<https://api.github.com/repos/hmh323/mubai-ears>
- faster-whisper：<https://github.com/SYSTRAN/faster-whisper>
