<!-- markdownlint-disable MD013 -->

# YuE / YuE2（multimodal-art-projection/YuE）中文解读

> 证据快照：2026-09-13（Asia/Shanghai）。GitHub REST API 显示 7,263 stars、820 forks、11 open issues，最新 release 为 `yue2-v0.1.6`。当前分支的一方代码/文档/agent skill 为 Apache-2.0，YuE2 checkpoint 权重另按 CC BY-NC 4.0；本文未下载权重、生成音频或复现实验。

## 定位

YuE2 是把符号音乐规划、完整歌曲生成、零样本翻唱和 agentic editing 放在同一 checkpoint 中的音乐生成系统。输入歌词与风格后，它先形成可读可改的旋律/和弦计划，再生成语义音乐 token、声学 latent 与 48 kHz 立体声音频。

相比直接生成波形，它把 ABC score 暴露为“白盒控制面”：人或 agent 可以在渲染前检查旋律、和声、速度与曲式，并保存 score、token、latent、模型身份和参数作为可比较 artefact。

## 用法

上游要求 Linux、Python 3.12、支持 BF16 的 NVIDIA GPU 与至少 24 GB VRAM，模型首次运行时从 Hugging Face 下载：

```bash
git clone https://github.com/multimodal-art-projection/YuE.git
cd YuE
python3.12 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install .
python examples/generate.py --output outputs/first-song
```

`cot="full"` 生成完整旋律/和弦计划，`cot="melody"` 适合保留旋律后重做伴奏，`abc=...` 可直接提供已审阅 score。翻唱还需要单独环境中的 SheetSage2 先把源录音转成符号旋律。

## 原理

- 同一 AR–NAR Mixture-of-Transformers 骨干先自回归预测 score 与 semantic tokens，再用 flow matching 生成 acoustic latents。
- VAE 将 latent 解码成完整立体声音频；`plan()`、`generate_semantic()`、`synthesize()`、`decode()` 暴露分阶段接口。
- 创作、翻唱和编辑的主要差别是 score 来源：模型生成、录音转写或人工/agent 修改。
- `yue2-music` skill 教 agent 保存原版、修改 score、检查音乐不变量并组织听感 A/B，但 skill 与 Python runtime 分开安装。

## 价值

- 把不可解释的端到端生成拆成可读 score 与多阶段 artefact，便于审阅、复现和版本比较。
- 同一模型支持创作、翻唱与编辑，减少在多个模型间转换表征造成的状态丢失。
- 公开模型、评测数据与生成接口，为音乐生成的算法比较和人机协作研究提供起点。
- 24 GB VRAM 门槛相对可控，但仍应按具体 GPU、时长、候选数与 decoder 测真实吞吐。

## 风险边界

- 上游 WildSongBench 的 `best-of-8` 结果包含候选选择优势；README 也明确最高均值的小差异未建立统计显著性，不能简化为“全面超过商业模型”。
- 代码 Apache-2.0 不代表权重可商业使用；YuE2 checkpoint 是 CC BY-NC 4.0，第三方组件和评测资产另有许可。
- 翻唱、音色、歌词和训练数据可能涉及著作权、表演者人格/声音权与平台政策；技术可行不等于获得授权。
- score 可编辑不保证最终音频严格遵守每个音符，也不保证无伪影、错误歌词或风格模仿风险。
- 技术报告尚未发布，本页没有独立复现 192-prompt benchmark、zero-shot cover 或声称的 SOTA 指标。

## 补充建议

1. 先用自有或明确授权的歌词、旋律和声音素材，在单首短样本上验证显存、延迟和 artefact 完整性。
2. 固定模型 revision、decoder、seed、候选数和输入；比较标准生成与 best-of-N 时单独记录选择成本。
3. 对 score 一致性、歌词可懂度、伪影和身份相似度做人工盲评，不只看自动指标。
4. 商业或公开发布前分别审查代码、权重、源录音、歌词、声音、第三方模型和输出平台条款。

## 参考资料

- GitHub：<https://github.com/multimodal-art-projection/YuE>
- GitHub REST API：<https://api.github.com/repos/multimodal-art-projection/YuE>
- Release：<https://github.com/multimodal-art-projection/YuE/releases/tag/yue2-v0.1.6>
- 项目演示：<https://map-yue2.github.io/>
- YuE2-3B 模型卡：<https://huggingface.co/m-a-p/YuE2-3B>
- Benchmark 协议：<https://github.com/multimodal-art-projection/YuE/blob/main/docs/benchmarks.md>
- 模型权重许可：<https://github.com/multimodal-art-projection/YuE/blob/main/MODEL_LICENSE>
- 源码 LICENSE：<https://github.com/multimodal-art-projection/YuE/blob/main/LICENSE>
