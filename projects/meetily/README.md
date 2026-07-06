<!-- markdownlint-disable MD013 -->

# meetily

## 定位

`meetily` 是一个隐私优先的开源 AI 会议助手，主打本地实时转写、说话人分离、会议摘要和 Ollama / Whisper / Parakeet 等本地或自选模型后端。它面向需要数据主权的个人、团队和企业会议场景。

在 AI meeting note taker 赛道中，它的差异点是“会议数据不离开本机或自有基础设施”，而不是把音频默认上传到云端 SaaS。

## 用法

普通用户可从 release 下载 macOS 或 Windows 安装包。Linux 用户主要走源码构建路径：

```bash
git clone https://github.com/Zackriya-Solutions/meeting-minutes
cd meeting-minutes/frontend
pnpm install
./build-gpu.sh
```

项目支持本地转写、实时 transcript、AI summary、多平台会议捕获，并可选择 Ollama、本地模型、Claude、Groq、OpenRouter 或 OpenAI-compatible endpoint。

## 原理

`meetily` 的基本链路是：

1. 在本机捕获会议音频。
2. 用 Whisper、Parakeet 或相关语音模型做实时转写。
3. 做说话人识别 / diarization 与 transcript 整理。
4. 调用本地或用户指定的 LLM 生成会议摘要、行动项和结构化记录。
5. 把数据保留在本地或用户控制的部署环境中。

项目用 Rust 等技术构建桌面端与处理链路，强调离线、本地和自托管部署。

## 价值

- **隐私与合规**：适合法律、医疗、企业内会、客户访谈等敏感场景。
- **本地模型入口**：把 Ollama、Whisper、Parakeet 等本地 AI 能力落到具体办公工作流。
- **替代云会议助手**：降低对第三方会议录音和摘要服务的依赖。
- **开源可审计**：企业可检查数据路径、模型调用和导出逻辑。

## 风险边界

- 本地转写质量依赖麦克风、设备性能、模型选择和语言场景。
- 会议录音涉及双向同意、公司政策和地区法律，不能因为本地处理就忽略合规。
- PRO 功能与社区版边界需要持续关注，避免把商业功能误写成开源能力。
- 多模型 provider 支持会带来配置复杂度，使用云端模型时仍会有数据外发。

## 补充建议

- 对敏感会议优先使用 Ollama / 本地转写路径，并关闭外部 provider。
- 团队落地前应明确录音告知、存储周期、访问权限和删除流程。
- 与 `claude-video` 一起看，可以覆盖“实时会议记录”和“事后视频理解”两类多模态办公入口。

## 参考资料

- GitHub 仓库：<https://github.com/Zackriya-Solutions/meetily>
- 官方网站：<https://meetily.ai>
- Demo 视频：<https://youtu.be/6FnhSC_eSz8>
- GitHub Trending：<https://github.com/trending>
