<!-- markdownlint-disable MD013 -->

# conversation-steganography

## 定位

`conversation-steganography` 是一个 LLM 隐写 proof of concept，用本地模型把加密后的秘密消息伪装成普通聊天文本。它位于 LLM 安全、隐私、滥用风险和内容检测边界的交叉点，热度很高但不应被视为日常通信工具推荐。

## 用法

```bash
git clone https://github.com/nethical/conversation-stenography.git
cd conversation-stenography
go build -o conversation-stenography ./cmd/conversation-stenography
./conversation-stenography
```

首次运行会选择并下载本地模型、生成配置；`simulate` 模式可在一台机器上模拟 Alice/Bob 两方，验证 cover text 生成和解码流程。

## 原理

项目将原始消息先加密，再用本地 LLM 生成看似自然的 cover text，把编码信息嵌入普通对话。接收方使用共享密钥和相同协议从 cover text 中恢复原文。项目 README 明确将其声明为教育和研究用途，并承认已有检测隐藏内容的技术路线。

## 价值

- 对研究 LLM 隐写、内容扫描规避、加密通信可检测性和模型生成文本水印有参考价值。
- 显示本地小模型也可参与安全敏感的信息伪装流程，不是只有 frontier 模型才有滥用风险。
- 可作为 AI 安全日报中的争议样本，提醒 agent 工具也会被用于规避平台审计。

## 风险边界

- 具有明显双重用途风险，可能被用于规避合法审计、平台治理或调查。
- 隐写文本并不等于不可检测，统计检测、行为关联和端点取证都可能暴露风险。
- 项目本身是 proof of concept，可靠性、密钥管理、威胁模型和法律边界不完整。
- 本仓库收录仅用于安全研究跟踪，不建议用于实际规避通信监管或平台规则。

## 补充建议

- 关注点应放在检测、防护、平台治理和端侧隐私之间的张力，而不是传播使用教程。
- 若用于研究，应在受控环境中测试，并记录模型、密钥、样本和检测方法。
- 与 GPT-Red、prompt injection red teaming、watermark / provenance 讨论放在同一安全趋势下观察。

## 参考资料

- GitHub：<https://github.com/nethical6/conversation-steganography>
- 项目 README：<https://github.com/nethical6/conversation-steganography#readme>
- LLM 隐写研究背景：<https://arxiv.org/search/cs?query=LLM+steganography&searchtype=all>
