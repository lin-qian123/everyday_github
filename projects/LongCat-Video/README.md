<!-- markdownlint-disable MD013 -->

# LongCat-Video（meituan-longcat/LongCat-Video）

> 上游仓库：<https://github.com/meituan-longcat/LongCat-Video> · 归类：语音、视频与多模态 · 本页基于 2026-10-04 的 GitHub API、README、技术报告、Hugging Face 权重页、requirements 与 LICENSE 静态整理，未下载 13.6B 模型、运行 GPU 推理、复测 benchmark 或审查训练数据。

- 抓取快照：8,720 stars、1,523 forks、80 open issues。
- 热度信号：GitHub 综合 / Python Trending 抓取时约 +43 当日 stars。
- 版本与许可：API 与根 LICENSE 为 MIT，README 称模型权重同为 MIT；无 GitHub Release / tag，基础模型与 Avatar / Avatar 1.5 为独立权重制品。

## 定位

LongCat-Video 是美团 LongCat 团队发布的 13.6B 视频生成模型和推理代码，统一文本到视频、图像到视频、视频续写与长视频生成；同仓库还支持音频驱动的单人 / 多人 Avatar 及续写。上游把它视为迈向 world model 的早期基础模型。

## 用法

上游建议 Python 3.10、PyTorch 2.6 / CUDA 12.4、FlashAttention 2，并从 Hugging Face 分别下载基础、Avatar 和 Avatar 1.5 权重。`torchrun` 脚本覆盖单 / 多 GPU 的 T2V、I2V、continuation、long video、interactive video 与音频 Avatar；Streamlit 提供交互入口，Avatar 1.5 可选 distillation 与 INT8 DiT。

## 原理

基础模型用统一 dense video diffusion 架构处理多任务，并以时间 / 空间 coarse-to-fine 与 Block Sparse Attention 降低 720p、30 fps 生成成本；Video-Continuation 预训练支撑分段长视频。上游还使用多奖励 GRPO 做偏好优化。Avatar 1.5 用 Whisper-Large-v3 编码音频，以蒸馏缩短采样并支持单流 / 多流说话人控制。

## 价值

同一套代码覆盖生成、续写、长视频与音频角色，可减少多模型拼接和任务间接口差异；开放权重、技术报告与可执行脚本为长视频一致性、音画同步、稀疏注意力和推理加速提供了可复查起点。

## 风险边界

- README 的 MOS、与商业模型“可比”及分钟级长视频质量来自作者内部 / 公开 benchmark 汇总，本轮没有复跑、盲评或核对评测样本与成本。
- 13.6B dense 模型、720p / 30 fps、FlashAttention 与多 GPU 命令意味着显著显存、存储、编译和运行成本；“数分钟生成”强依赖硬件、长度、分辨率和采样设置。
- 上游 tips 已记录重复动作、artifact、CFG、参考帧和 mask range 的敏感性；视频续写不保证物理一致、身份稳定、口型准确或无颜色漂移。
- README 声称代码和权重 MIT，但模型下载仍应固定 Hugging Face revision，并分别核对权重卡、训练数据、肖像 / 声音 / 音乐 / 商标和输出权利。
- Avatar、声音克隆和人物生成可被用于冒充、未授权肖像 / 声音合成与误导内容；必须取得同意并保留 provenance / watermark / 发布审核。
- 上游 usage considerations 明确没有覆盖所有下游场景；隐私、内容安全、公平性和高风险使用仍由部署者负责。

## 补充建议

固定仓库 commit 和每个 Hugging Face revision，在授权素材上建立短片金标，分开量化文本 / 图像一致性、身份漂移、口型、重复动作、色漂、时序断裂、VRAM、延迟和失败率。先生成低分辨率 / 短时长预览，再做长视频与超分；所有真人音频和肖像都应记录授权、输入哈希、模型版本与发布审批。

## 参考资料

- [GitHub 仓库](https://github.com/meituan-longcat/LongCat-Video)
- [GitHub REST API](https://api.github.com/repos/meituan-longcat/LongCat-Video)
- [README 与运行说明](https://github.com/meituan-longcat/LongCat-Video/blob/main/README.md)
- [技术报告 arXiv:2510.22200](https://arxiv.org/abs/2510.22200)
- [基础模型权重](https://huggingface.co/meituan-longcat/LongCat-Video)
- [Avatar 1.5 权重](https://huggingface.co/meituan-longcat/LongCat-Video-Avatar-1.5)
- [依赖清单](https://github.com/meituan-longcat/LongCat-Video/blob/main/requirements.txt)
- [LICENSE](https://github.com/meituan-longcat/LongCat-Video/blob/main/LICENSE)
