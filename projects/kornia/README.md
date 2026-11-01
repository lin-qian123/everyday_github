<!-- markdownlint-disable MD013 -->

# kornia

- 主上游：[kornia/kornia](https://github.com/kornia/kornia)
- 分类：模型、训练与推理基础设施。
- 核验日期：2026-11-02（Asia/Shanghai）；默认分支 `main`，固定快照 `ff6774d332d9`。
- [API](https://api.github.com/repos/kornia/kornia) 快照：11,759 stars / 1,465 forks / 133 open issues（含 PR）；发行列表首项 [v0.9.0](https://github.com/kornia/kornia/releases/tag/v0.9.0)（UTC 2026-10-23）。累计量不是今日增量，主线不等于发行包。

## 定位

Kornia 是基于 PyTorch 的可微计算机视觉与几何库，覆盖颜色、滤波、相机、单应性、特征匹配、图像增强与损失。它提供张量算子，可接入训练或推理计算图；“Spatial AI”是应用方向，不能据此把每个算子都当作学习模型。当前维护重点转向几何核心、明确约定与一致性测试。[README.md](https://github.com/kornia/kornia/blob/ff6774d332d98a7ba78a09d058bb40998d9774d4/README.md)、[ROADMAP.md](https://github.com/kornia/kornia/blob/ff6774d332d98a7ba78a09d058bb40998d9774d4/ROADMAP.md)

## 用法

在独立环境安装已核存在的 PyPI 0.9.0；当前主线要求 Python ≥3.11、PyTorch ≥2.5.1。先从无权重下载的张量算子开始：

```sh
python -m pip install "kornia==0.9.0"
```

```python
import torch
import kornia

image = torch.rand(2, 3, 64, 64, requires_grad=True)
blurred = kornia.filters.gaussian_blur2d(image, (5, 5), (1.2, 1.2))
blurred.mean().backward()
print(blurred.shape, image.grad is not None)
```

这是待执行的最小示例；几何增强还要明确 BCHW、通道、数值范围、像素 / 归一化坐标、角度单位及 `align_corners`。[README.md](https://github.com/kornia/kornia/blob/ff6774d332d98a7ba78a09d058bb40998d9774d4/README.md)、[pyproject.toml](https://github.com/kornia/kornia/blob/ff6774d332d98a7ba78a09d058bb40998d9774d4/pyproject.toml)

## 原理

以张量批处理和 PyTorch 自动微分组合经典视觉算法；几何变换可产生采样网格，再对图像插值，增强容器可将同一随机变换同步用于图像、mask、点或框。可微性取决于具体算子、输入与分支，离散选择、退化求解和后端限制需按 API 检查。[README.md](https://github.com/kornia/kornia/blob/ff6774d332d98a7ba78a09d058bb40998d9774d4/README.md)、[ROADMAP.md](https://github.com/kornia/kornia/blob/ff6774d332d98a7ba78a09d058bb40998d9774d4/ROADMAP.md)

## 价值

适合把图像预处理、可微配准、几何损失或多模态标签增强放进现有 PyTorch 流程，减少逐样本 CPU / GPU 来回搬运。真正收益需同时测传输、批量、分辨率、梯度和精度，不能从单算子宣传倍数推成完整训练管线提速。

## 风险边界

- 当前 README 的半精度表明确是特定 Linux CPU / Python / PyTorch 条件下的参数化测试；记录 243 个 float16、256 个 bfloat16 已知失败，并非对应数量的“不支持函数”。未覆盖 CUDA / MPS 半精度 CI，不能从 CPU 结果外推。[README.md](https://github.com/kornia/kornia/blob/ff6774d332d98a7ba78a09d058bb40998d9774d4/README.md)
- 返回 dtype 为半精度不表示内部全部用半精度计算；部分颜色、滤波、增强会先转 float32。几何坐标约定和病态矩阵的数值误差可能比运行时间更关键。[README.md](https://github.com/kornia/kornia/blob/ff6774d332d98a7ba78a09d058bb40998d9774d4/README.md)、[ROADMAP.md](https://github.com/kornia/kornia/blob/ff6774d332d98a7ba78a09d058bb40998d9774d4/ROADMAP.md)
- `torch.compile`、ONNX、设备 / dtype 支持按算子核对。模型库扩展当前冻结，不宜把路线图候选项写成已交付能力。根代码 Apache-2.0，下载模型和数据另核。[ROADMAP.md](https://github.com/kornia/kornia/blob/ff6774d332d98a7ba78a09d058bb40998d9774d4/ROADMAP.md)、[LICENSE](https://github.com/kornia/kornia/blob/ff6774d332d98a7ba78a09d058bb40998d9774d4/LICENSE)

## 补充建议

从实际任务挑 3–5 个算子，对固定输入建立数值、梯度、坐标 round-trip 和标签同步对照；分别记录 CPU / CUDA / MPS、float32 / float16 / bfloat16。性能比较保留 warm-up、同步、传输与误差门槛。本轮只核文档、清单和元数据，未安装或运行上述示例。

## 参考资料

- [README.md](https://github.com/kornia/kornia/blob/ff6774d332d98a7ba78a09d058bb40998d9774d4/README.md)（固定 commit）。
- [pyproject.toml](https://github.com/kornia/kornia/blob/ff6774d332d98a7ba78a09d058bb40998d9774d4/pyproject.toml)（固定 commit）。
- [ROADMAP.md](https://github.com/kornia/kornia/blob/ff6774d332d98a7ba78a09d058bb40998d9774d4/ROADMAP.md)（固定 commit）。
- [LICENSE](https://github.com/kornia/kornia/blob/ff6774d332d98a7ba78a09d058bb40998d9774d4/LICENSE)（固定 commit）。
- [仓库 API](https://api.github.com/repos/kornia/kornia)、[发行列表](https://github.com/kornia/kornia/releases)（动态状态）。
- [PyPI 0.9.0](https://pypi.org/project/kornia/0.9.0/)。
