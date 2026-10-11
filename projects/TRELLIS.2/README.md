<!-- markdownlint-disable MD013 -->

# TRELLIS.2（microsoft/TRELLIS.2）中文解读

> 上游仓库：<https://github.com/microsoft/TRELLIS.2> · 归类：语音、视频与多模态 · 本页基于 2026-10-12 的 README、论文、模型卡、SECURITY、许可证与 GitHub REST API 静态整理；未下载 4B 权重、运行 H100 推理、训练模型或验收生成网格。

## 定位

TRELLIS.2 是 Microsoft 开源的单图生 3D 模型与训练 / 推理代码。它用 O-Voxel 表示几何和外观，目标是生成带 Base Color、Roughness、Metallic、Opacity 等 PBR 材质的复杂 3D 资产，并支持开放表面、非流形和内部结构。

## 用法

上游要求 Linux、Python 3.8+、CUDA 工具链和至少 24 GB NVIDIA GPU，并在 A100 / H100 上验证。克隆时需递归获取 submodule，再用 `setup.sh` 安装 PyTorch、attention、mesh、O-Voxel 等组件；`example.py` 从 `microsoft/TRELLIS.2-4B` 加载 pipeline，将输入图生成 3D 表示和网格。

## 原理

- O-Voxel 以稀疏 voxel 结构统一编码任意拓扑几何与 PBR 外观。
- Sparse 3D VAE 做 16× 空间下采样，把高分辨率资产压缩进较短 latent 序列。
- 4B flow-matching transformer 在 latent 空间生成形状与材质，再由 CUDA / mesh 工具转换为可渲染资产。
- shape-conditioned texture 路径可在既有 mesh 和参考图条件下生成纹理。

## 价值

- 相比只输出封闭等值面的方案，更直接覆盖服装、叶片、透明材质等复杂资产。
- 代码、权重、论文、训练脚本和演示入口同时公开，便于做端到端复现与消融。
- 输出包含 PBR 属性，较适合进入 DCC / 游戏资产的人工修订流程。

## 风险边界

- README 的 512³ 约 3 秒、1536³ 约 60 秒均为作者 H100 环境数据，不能外推到其他 GPU、输入或批量生产。
- 模型卡明确记录小孔和拓扑不连续；后处理可修补部分缺陷，但不能证明水密、可打印、可制造或满足工程公差。
- 基础模型未做人类偏好对齐，输出质量和风格会随输入变化；几何、材质、透明度和碰撞仍需人工验收。
- 代码 / 模型卡标为 MIT 不自动解决训练数据、输入图片、品牌、角色、肖像和生成资产的权利问题。

## 补充建议

- 先用许可清晰的自有图片建立固定测试集，记录 mesh holes、non-manifold edges、UV / PBR 完整度和显存 / 时间。
- 把“视觉相似”“拓扑可编辑”“渲染正确”“可打印 / 可制造”作为四个独立验收层。
- 正式使用时固定代码 commit、模型 revision、submodule SHA、CUDA / PyTorch 版本，并保存导出前后的资产 hash。

## 参考资料

- GitHub 仓库：<https://github.com/microsoft/TRELLIS.2>
- GitHub REST API：<https://api.github.com/repos/microsoft/TRELLIS.2>
- 论文：<https://arxiv.org/abs/2512.14692>
- 模型卡：<https://huggingface.co/microsoft/TRELLIS.2-4B>
- 项目主页：<https://microsoft.github.io/TRELLIS.2>
- SECURITY：<https://github.com/microsoft/TRELLIS.2/blob/main/SECURITY.md>
- LICENSE：<https://github.com/microsoft/TRELLIS.2/blob/main/LICENSE>
