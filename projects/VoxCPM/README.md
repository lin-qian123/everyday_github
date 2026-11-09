<!-- markdownlint-disable MD013 -->

# VoxCPM / VoxCPM2

## 定位

VoxCPM 是 OpenBMB 的 tokenizer-free TTS 系列。当前主推 VoxCPM2，作者描述为 2B 骨干、30种语言、声音设计、参考音色控制与48 kHz输出。VoxCPM-0.5B / 1.5 的语言、采样率、克隆方式不同，本页在原目录更新。

- 上游：[OpenBMB/VoxCPM](https://github.com/OpenBMB/VoxCPM)，仓库 ID `1057664813`。
- 2026-11-10：42,107 stars / 4,799 forks / 173 open issues（含 PR）；Python daily +423。
- 稳定代码发行 [2.0.3](https://github.com/OpenBMB/VoxCPM/releases/tag/2.0.3)，UTC 2026-05-11；PyPI 同版。本页按主线 `300e4260b509066151d623dc9c0aa922cf82232b` 核读，后续文档、模型与第三方后端新增不自动属于该发行。

## 用法

1. 独立环境：README 推荐 Python ≥3.10、<3.13，PyTorch ≥2.5、CUDA ≥12；包元数据只写 Python ≥3.10。安装器接受不代表新 Python 已获验证。
2. 固定包 `python -m pip install "voxcpm==2.0.3"`，核模型 revision 与来源；首次 `from_pretrained` 通常下载权重。主线 `local_files_only=True` 约束主模型解析，denoiser / timestamps 等附加资产另核。
3. 普通 TTS 给文本；声音设计前置描述；可控克隆传 `reference_wav_path`，续接式克隆另给 `prompt_wav_path` / 准确的 `prompt_text`。参考样本须获授权。
4. 主线 Web demo 本机试用 `python app.py --host 127.0.0.1 --port 8808`；默认 `0.0.0.0`，帮助明确会暴露未认证 UI / API。保存波形时使用模型实际 sample rate。

以上仅为阅读入口，本轮未装包、下载权重、合成或试听。

## 原理

模型保留文本 token，绕过离散音频 tokenizer，在连续语音表征上进行扩散自回归生成；语言骨干处理文本与上下文，局部模块生成声学表示，AudioVAE 解码波形。“tokenizer-free”不表示全系统没有 token。

VoxCPM2 的参考编码与续接提示承担不同条件作用；README 描述 AudioVAE V2 接收16 kHz参考、输出48 kHz。输出采样率不证明高频细节真实。流式分块生成的完整延迟还含模型加载、首块等待和播放缓冲。

## 价值

- 提供可修改的本地 TTS 与多语种研究入口，可比较连续声学建模、提示和音色条件。
- 风格服从、内容正确与说话人相似度可分别研究，避免单一指标概括全部质量。
- 作者报告 RTX 4090 标准实现 RTF约0.3、第三方加速约0.13；RTF小于1表示生成快于音频时长，不是首字延迟，也不是本轮测量。

## 风险边界

- **控制波动**：作者承认声音设计 / 可控克隆可能需多次生成；记录全部尝试与失败，避免只报最好样本。
- **评测不同目标**：WER / CER、SIM、风格服从与人工听感不能互代；公开基准、内部30语种 ASR 表不能替代目标口音、长文和专名测试。
- **本地不等于断网**：主模型、denoiser、对齐工具及 serving 的下载 / 请求路径分别核；网络监听与本地推理独立。
- **后端分开**：Nano-vLLM、vLLM-Omni、llama.cpp-omni / GGUF 有各自版本、精度与依赖，量化、RTF和内存宣称不外推。
- **权利与来源**：根代码和官方 VoxCPM2 Hub 元数据为 Apache-2.0；声音授权、文本、第三方权重和服务条款另核。作者禁止冒充、欺诈和虚假信息，建议标记合成音频；本轮未验证自动水印能力，不将水印写成已有功能或普遍法定义务。

## 补充建议

固定模型 revision、设备 / dtype、后端、seed、CFG、步数、文本与授权参考，记录首块延迟、RTF、显存和失败率，再做双盲听评。覆盖短句、长文、数字、专名与目标语言；ASR / SIM辅助诊断，不能替代完整试听或用户接受。

## 参考资料

- [固定 SHA README：系列、接口与限制](https://github.com/OpenBMB/VoxCPM/blob/300e4260b509066151d623dc9c0aa922cf82232b/README.md)
- [依赖与 Python 元数据](https://github.com/OpenBMB/VoxCPM/blob/300e4260b509066151d623dc9c0aa922cf82232b/pyproject.toml)、[PyPI 快照](https://pypi.org/pypi/voxcpm/json)
- [模型解析与生成条件](https://github.com/OpenBMB/VoxCPM/blob/300e4260b509066151d623dc9c0aa922cf82232b/src/voxcpm/core.py)、[CLI 参数](https://github.com/OpenBMB/VoxCPM/blob/300e4260b509066151d623dc9c0aa922cf82232b/src/voxcpm/cli.py)
- [Web demo 监听默认](https://github.com/OpenBMB/VoxCPM/blob/300e4260b509066151d623dc9c0aa922cf82232b/app.py)
- [官方模型许可元数据](https://huggingface.co/openbmb/VoxCPM2)、[代码许可证](https://github.com/OpenBMB/VoxCPM/blob/300e4260b509066151d623dc9c0aa922cf82232b/LICENSE)
