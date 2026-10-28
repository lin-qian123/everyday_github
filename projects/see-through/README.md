<!-- markdownlint-disable MD013 -->

# See-through

## 定位

See-through 是把单张动漫角色图拆成可编辑语义图层的研究实现。上游将其对应到 SIGGRAPH 2026 论文，当前 V3 流程最多分出 23 类身体部件，并补绘被遮挡区域、推断图层顺序，导出 PSD。它为 2.5D 动画制作准备素材，后续仍需美术修整和绑骨。

2026-10-29 快照：Python daily 榜 +78 stars；API 累计 5,095 stars / 450 forks / 23 open issues（含 PR）。主线固定到 `df019de5129d`，发行 API 本轮为空；根代码许可 Apache-2.0。本文核读文档、依赖与入口参数，未运行推理或复现实验。

## 用法

1. 准备 Python 3.12 独立环境，按固定 README 匹配 PyTorch 与 CUDA / ROCm；不要将 CUDA 安装命令直接套到 macOS。
2. 从仓库根目录安装 requirements，建立 assets 链接；SAM2、实例分割等可选依赖按任务添加。
3. 对有权处理的图片运行主入口，再在图像编辑器检查 PSD 的透明度、遮挡和命名。

```bash
python inference/scripts/inference_psd.py \
  --srcp assets/test_image.png \
  --save_to_psd
```

默认输出目录 `workspace/layerdiff_output/`。README 给出的 1280 分辨率 bf16 显存约 12–16 GB，以及 group offload / NF4 的节省幅度，均为作者说明，本轮没有测量。HF / ModelScope 演示涉及上传图片及平台配额，应先查看当时页面。

## 原理

LayerDiff 3D 生成带透明通道的图层，面向动漫微调的 Marigold 估计伪深度，再组织语义部件和绘制顺序。遮挡补绘是模型生成的推断，不能当作原画中确实存在的细节。主入口显式设置随机种子、图层 / 深度模型 ID、分辨率和采样步数，便于固定条件比较。

## 价值

- 将手工切图和补绘的部分重复劳动变为可检查的 PSD 起点。
- 把视觉生成、深度估计和语义分层连接起来，适合研究动漫素材处理与编辑流程。
- 训练脚本和分层结果可用于方法研究，但产出质量需按角色、遮挡与服饰复杂度分别评估。

## 风险边界

- 上游明确表示尚非完整 Image-to-Live2D：变形网格、物理参数和动作曲线不在该项目范围内。
- 语义分对不保证层级适合自然运动；手指、透明衣饰、左右部件、遮挡后纹理都需逐层审阅。
- 代码 Apache-2.0 不替代各下载权重、第三方依赖、样例角色和输入图片的使用许可。
- 首次模型下载、GPU 与可选原生依赖影响可复现性；低显存方案可能改变速度或质量，不能套用作者数字作本机保证。
- README 声明作者未开设付费服务。收费同名网站不能仅凭名称认定为官方。

## 补充建议

先固定源码、权重 revision、种子和输入，用少量授权角色建立遮挡 / 重叠 / 半透明测试集。验收应包括 PSD 能否打开、图层内容与顺序、合成回原图差异、人工返工时间，以及后续绑骨能否运动；分别记录作者声明与本地实测。

## 参考资料

- [上游仓库](https://github.com/shitagaki-lab/see-through)、[GitHub API](https://api.github.com/repos/shitagaki-lab/see-through)。
- [固定 README：安装、模型、显存与 Live2D 边界](https://github.com/shitagaki-lab/see-through/blob/df019de5129d6c4b406587a14c3501669441a783/README.md)。
- [主入口参数](https://github.com/shitagaki-lab/see-through/blob/df019de5129d6c4b406587a14c3501669441a783/inference/scripts/inference_psd.py)、[依赖清单](https://github.com/shitagaki-lab/see-through/blob/df019de5129d6c4b406587a14c3501669441a783/requirements.txt)、[代码许可](https://github.com/shitagaki-lab/see-through/blob/df019de5129d6c4b406587a14c3501669441a783/LICENSE)。
