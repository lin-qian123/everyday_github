<!-- markdownlint-disable MD013 -->

# CLIP：用对比学习连接图片与文字

- 上游：[openai/CLIP](https://github.com/openai/CLIP)，仓库 ID `321960447`；本页新增于 2026-11-26。
- 快照：34,659 stars / 4,068 forks / 274 open issues（累计，含 PR）；Jupyter Notebook daily +8。
- 默认 SHA `d05afc436d78f1c48dc0dbf8e5980a9d471f35f6`，2026-03-25 18:46 UTC，提交为固定 GitHub Actions 引用；所见 Releases 集合为空，setup.py 版本为 1.0。此次上榜不代表新模型发布。
- 范围：README、模型卡、loader / forward 局部源码与依赖 / 许可静态核读；未安装、下载权重、处理用户图片或执行推理。

## 定位

CLIP 将图片和文本编码到可比较的特征空间，用自然语言描述候选类别，进行零样本图像分类与图文相似度研究。它输出特征或匹配分数，没有在此仓库中提供生成式问答、自由描述生成或物体框检测接口。

模型卡将其定位为研究成果，并要求部署前做具体任务验证；它和 OpenCLIP、第三方中文 CLIP、扩散模型中的图文组件并非同一训练权重与评测对象。

## 用法

先固定仓库 SHA，选择与目标设备兼容的 PyTorch / torchvision 环境。README 的 PyTorch 1.7.1 / CUDA 11.0 是历史示例，requirements 也未锁定版本；本轮未验证该旧组合在当前机器的安装情况。

以下是环境已准备且自行允许下载官方权重后的最小示意，未执行：

```python
import clip
import torch
from PIL import Image

model, preprocess = clip.load("ViT-B/32", device="cpu")
image = preprocess(Image.open("example.png")).unsqueeze(0)
text = clip.tokenize(["a photo of a cat", "a photo of a dog"])
with torch.no_grad():
    logits, _ = model(image, text)
    scores = logits.softmax(dim=-1)
print(scores)
```

`clip.load` 可能联网下载权重，并写入默认 `~/.cache/clip`；本地 checkpoint 路径也是输入选项。`tokenize` 默认长度 77，包含特殊 token；超长默认报错，显式 `truncate=True` 才截断。不要用 77 字符解释这一限制。

## 原理

图像编码器与文本 Transformer 分别提取向量，训练时通过对比目标提高成对图文相似度并区分批内其他配对。图像分支有修改版 ResNet 和 ViT 等选择。

推理时 `forward` 将两类特征按范数归一化，再计算矩阵乘积并乘 `exp(logit_scale)`。README 将其概述为余弦相似度乘 100，源码实际使用权重中的可学习尺度；不要把手写常数 100 当所有 checkpoint 的接口不变量。直接使用 `encode_image` / `encode_text` 时，应自行处理检索所需归一化。

对一组候选描述做 softmax，只得到该候选集合内的相对分数。增加类别或改写 prompt 会改变结果；它不是对现实世界所有类别校准后的正确概率，也没有自动给出“所有候选均不匹配”的拒绝类别。

## 价值

它提供了透明、简洁的图文表示学习基线，适合比较 prompt、类别集合、向量检索与零样本 / linear probe 的差异。预处理与模型一起固定，才能让比较具有意义。

README 的 ImageNet 零样本表现对照原始 ResNet50 是特定论文条件下的历史结果，不能外推到中文、专业图像、计数或所有分布变化，更不构成本轮性能测量。

## 风险边界

| 议题 | 已核事实与边界 |
| --- | --- |
| 模型用途与许可 | 仓库 LICENSE 为 MIT；模型卡另将任意部署列为 out of scope，并明确监控 / 人脸识别及未充分验证用途的限制。模型卡的用途建议与许可证条款分开记录，不把它改写成新增的 MIT 法律条件。 |
| 语言与偏差 | 模型卡称未专门训练 / 评估英语以外语言，并讨论类别设计、人口偏差、计数和细粒度识别局限。中文输入能被 tokenize 不代表中文任务已验证。 |
| 类别与置信度 | softmax 随候选集合和措辞变化；高分不等于已校准概率，开放集需单独设计并验证拒识。 |
| checkpoint 信任 | 内置 URL 下载路径核 SHA256；本地任意 checkpoint 不能由此获得信任。loader 先尝试 torch.jit.load，失败后走 torch.load，具体反序列化行为还取决于安装的 PyTorch。 |
| 环境与版本 | setup.py 的 1.0 不是不可变发行身份；无版本约束的 torch 等依赖不保证旧源码可在任意新版本运行。 |
| 数据与应用 | 训练资料来自互联网；模型卡不发布训练集。仓库许可不能替代输入图片、下游资料及输出用途的权利确认。 |

## 补充建议

1. 固定 SHA、模型名 / 权重哈希、预处理、硬件与依赖，记录图片来源和候选描述全文。
2. 分开评估候选排序、检索 recall@K、类别准确率、校准与拒识；加入不属于候选类的样本。
3. 对中文和专业领域建立人工标注测试集，比较英语描述、翻译与领域适配，避免以单张演示图证明能力。
4. 只加载可信权重；将下载、模型初始化、编码耗时与检索耗时分别测量。

## 参考资料

- [仓库 API](https://api.github.com/repos/openai/CLIP)、[固定 README](https://raw.githubusercontent.com/openai/CLIP/d05afc436d78f1c48dc0dbf8e5980a9d471f35f6/README.md)、[模型卡](https://raw.githubusercontent.com/openai/CLIP/d05afc436d78f1c48dc0dbf8e5980a9d471f35f6/model-card.md)。
- [loader / tokenize](https://raw.githubusercontent.com/openai/CLIP/d05afc436d78f1c48dc0dbf8e5980a9d471f35f6/clip/clip.py)、[forward 与尺度](https://raw.githubusercontent.com/openai/CLIP/d05afc436d78f1c48dc0dbf8e5980a9d471f35f6/clip/model.py)。
- [requirements](https://raw.githubusercontent.com/openai/CLIP/d05afc436d78f1c48dc0dbf8e5980a9d471f35f6/requirements.txt)、[setup.py](https://raw.githubusercontent.com/openai/CLIP/d05afc436d78f1c48dc0dbf8e5980a9d471f35f6/setup.py)、[MIT LICENSE](https://raw.githubusercontent.com/openai/CLIP/d05afc436d78f1c48dc0dbf8e5980a9d471f35f6/LICENSE)。
