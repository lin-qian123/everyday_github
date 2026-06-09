# Fish Speech：高性能开源语音合成工具

## 项目概述

Fish Speech 是由 Fish Audio 团队开发的开源文本转语音（TTS）项目，旨在通过先进的深度学习技术，提供多语言、高自然度的语音合成解决方案。项目自开源以来，凭借低硬件门槛和强大的自定义能力，迅速成为全球开发者和创作者的热门选择。

- **GitHub 地址**：https://github.com/fishaudio/fish-speech
- **在线体验**：https://fish.audio/zh-CN/
- **星标数**：25,736+ ⭐（日增 2,172）
- **开发语言**：Python
- **开源协议**：CC-BY-NC-SA-4.0
- **开发者**：Fish Audio 团队

---

## 核心特性

### 1. 多语言支持

| 版本 | 支持语言 |
|------|----------|
| 基础版本 | 中文、英文、日文 |
| 1.5 版本 | 扩展至 **13 种语言**（含韩语、法语、西班牙语、德语、意大利语等） |

模型使用约 **十五万小时** 三语数据训练，对中文支持非常完美，语言处理能力接近人类水平。

### 2. 语音克隆与情感合成

**10 秒快速克隆**：
- 仅需少量参考音频（10-30 秒）
- 即可生成高相似度的个性化语音

**情感调节**：
- 支持自定义语音的情感风格（喜悦、悲伤、愤怒等）
- 提升内容表现力

### 3. 灵活部署方式

| 部署方式 | 说明 |
|----------|------|
| **WebUI 图形界面** | 可视化操作，适合非技术用户 |
| **HTTP API** | 适合集成到应用程序 |
| **命令行** | 适合批处理和自动化 |
| **Docker** | 一键部署，环境隔离 |

支持 Linux、Windows 系统，可云端或本地部署。

---

## 技术架构

### 模型特点

```
┌─────────────────────────────────────────────┐
│            Fish Speech 架构                  │
├─────────────────────────────────────────────┤
│  ┌─────────────────────────────────────┐    │
│  │        文本编码器 (Text Encoder)      │    │
│  │   多语言文本 → 语义向量表示           │    │
│  └─────────────────────────────────────┘    │
│                    ↓                         │
│  ┌─────────────────────────────────────┐    │
│  │        声学模型 (Acoustic Model)     │    │
│  │   语义向量 → 声学特征（梅尔频谱）     │    │
│  └─────────────────────────────────────┘    │
│                    ↓                         │
│  ┌─────────────────────────────────────┐    │
│  │        声码器 (Vocoder)              │    │
│  │   声学特征 → 音频波形                │    │
│  └─────────────────────────────────────┘    │
└─────────────────────────────────────────────┘
```

### 训练数据

- **数据量**：超过 100 万小时音频数据（1.5 版本）
- **语言覆盖**：中文、英文、日文等 13 种语言
- **数据质量**：高质量、多样化的语音数据

---

## 安装教程

### 环境要求

- Python 3.10+
- PyTorch 2.3+
- CUDA 12.1+（GPU 加速）

### 方式一：Conda 安装（推荐）

```bash
# 创建虚拟环境
conda create -n fish-speech python=3.10
conda activate fish-speech

# 安装 PyTorch
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121

# 克隆项目
git clone https://github.com/fishaudio/fish-speech.git
cd fish-speech

# 安装依赖
pip install -e .
```

### 方式二：Docker 安装

```bash
# 拉取镜像
docker pull fishaudio/fish-speech:latest

# 运行容器
docker run -it --gpus all --net host --shm-size 16G fishaudio/fish-speech:latest
```

### 方式三：Windows 本地部署

```bash
# 创建环境
conda create -n fish-speech python=3.10
conda activate fish-speech

# 安装 PyTorch（需要手动下载对应 CUDA 版本）
pip install torch-2.4.1+cu121-cp310-cp310-win_amd64.whl

# 安装项目
pip install -e .
```

---

## 使用方法

### 命令行使用

```bash
# 基础语音合成
python fish_speech/text_to_speech.py \
  --text "你好，这是 Fish Speech 的语音合成示例。" \
  --output output.wav

# 使用参考音频进行语音克隆
python fish_speech/text_to_speech.py \
  --text "这是克隆语音的示例。" \
  --reference reference_audio.wav \
  --output cloned_output.wav
```

### Python API 使用

```python
from fish_speech import TextToSpeech

# 初始化模型
tts = TextToSpeech(
    model="fish-speech-1.5",
    device="cuda"
)

# 基础语音合成
audio = tts.synthesize("你好，这是语音合成示例。")
audio.save("output.wav")

# 语音克隆
audio = tts.synthesize(
    text="这是克隆语音的示例。",
    reference_audio="reference.wav"
)
audio.save("cloned_output.wav")

# 情感调节
audio = tts.synthesize(
    text="今天天气真好！",
    emotion="happy"  # 支持 happy, sad, angry, neutral 等
)
```

### HTTP API 使用

```bash
# 启动 API 服务
python -m fish_speech.server --port 8080

# 调用 API
curl -X POST "http://localhost:8080/synthesize" \
  -H "Content-Type: application/json" \
  -d '{"text": "你好，这是 API 调用示例", "language": "zh"}' \
  --output output.wav
```

---

## WebUI 使用

启动 WebUI 界面：

```bash
python -m fish_speech.webui
```

访问 `http://localhost:7860` 即可使用图形界面进行：

- 文本转语音
- 语音克隆
- 情感调节
- 参数微调

---

## 性能对比

| 模型 | 中文自然度 | 英文自然度 | 克隆相似度 | 推理速度 |
|------|------------|------------|------------|----------|
| **Fish Speech 1.5** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | 快 |
| ChatTTS | ⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ | 中等 |
| VITS | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ | 快 |
| 传统 TTS | ⭐⭐ | ⭐⭐ | ⭐ | 很快 |

---

## 应用场景

### 内容创作
- 视频配音、有声书制作
- 播客、自媒体音频

### 教育领域
- 智能课件语音生成
- 语言学习辅助
- 无障碍教育

### 企业应用
- 客服语音系统
- 新闻播报
- 智能助手

### 个人使用
- 个人语音助手
- 消息朗读
- 创意项目

---

## 风险与注意事项

### 版权与伦理

1. **声音克隆版权**：克隆他人声音需获得授权
2. **身份冒用风险**：禁止用于欺诈、诈骗等违法行为
3. **内容合规**：生成内容需遵守法律法规

### 技术限制

1. **复杂情感表达**：极端情绪的表现力仍有提升空间
2. **特殊领域术语**：专业术语发音可能需要微调
3. **长文本一致性**：超长文本可能出现语气波动

---

## 最佳实践

1. **参考音频质量**：使用清晰、无噪音的参考音频（建议 10-30 秒）
2. **文本预处理**：对数字、缩写进行规范化处理
3. **参数调优**：根据场景调整语速、音调参数
4. **批量处理**：使用 API 进行大规模语音生成

---

## 相关资源

- [GitHub 仓库](https://github.com/fishaudio/fish-speech)
- [在线体验](https://fish.audio/zh-CN/)
- [官方文档](https://fish.audio/docs)
- [模型下载](https://wisemodel.cn/models/Fish_Audio/Fish-Speech-V1.5)

---

## 社区热度

Fish Speech 是 2026 年 3 月 GitHub Trending 热门项目：

- 日增星标 2,172+
- 开源 TTS 领域的领军项目
- 语音生成正从 demo 走向生产化

---

*更新时间：2026年3月12日*
