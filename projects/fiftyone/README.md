<!-- markdownlint-disable MD013 -->

# FiftyOne

> 上游仓库：[voxel51/fiftyone](https://github.com/voxel51/fiftyone) · 归类：模型、训练与推理基础设施 · 本页基于 2026-08-28 的上游 README、官方文档、许可证文件与 GitHub API 快照整理。

## 定位

FiftyOne 是面向高质量数据集和计算机视觉模型的开源工具，重点是可视化、标注、数据清洗、数据集策展、模型评估和错误分析。它把样本、标签、预测、嵌入和评测结果组织成可查询视图，帮助视觉 AI 团队发现数据问题、理解模型失败并迭代数据。GitHub Trending 的 TypeScript 页面把它列入当日靠前条目，显示约 4 个当日 stars；API 快照为 11,044 stars、816 forks、673 个开放 issue，2026-08-27 有推送，许可证为 Apache-2.0。

## 用法

在虚拟环境中安装稳定版：

```sh
pip install fiftyone
```

基本工作流是导入数据集、启动 FiftyOne App、浏览样本和标签，再运行模型评估或数据查询：

```python
import fiftyone as fo

dataset = fo.Dataset.from_dir(
    dataset_dir="./data",
    dataset_type=fo.types.COCODetectionDataset,
    label_field="ground_truth",
)
session = fo.launch_app(dataset)
session.wait()
```

也可以使用官方 [quickstart notebook](https://colab.research.google.com/github/voxel51/fiftyone-examples/blob/master/examples/quickstart.ipynb)、数据集 zoo、模型 zoo 和评测 API。开发版安装会涉及 Node.js、Yarn、MongoDB 等依赖，先按 [安装文档](https://docs.voxel51.com/installation/index.html) 固定环境。

## 原理

- Dataset、Sample、Field 和 Label 形成可查询的数据模型，允许把图像/视频/点云与 ground-truth、预测、嵌入和元数据关联起来。
- App 将样本、标签、缩略图、筛选条件和视图管线可视化；视图操作可以逐步缩小到错误样本、边界案例或特定数据切片。
- 模型评估器根据任务类型比较预测与 ground-truth，生成 accuracy、precision/recall、mAP 或样本级错误信息；具体指标取决于标签类型和配置。
- 数据导入器、导出器、数据集 zoo、模型 zoo 和插件连接外部数据/模型生态；每个连接器都可能带来下载、许可和网络依赖。
- 数据中心工作流把“发现问题—标注/清洗—重跑模型—比较评测”闭环，但工具本身不会自动证明样本标注正确或评测集没有泄漏。

## 价值

- 把视觉数据质量从静态文件浏览提升为可筛选、可查询、可复盘的工作流。
- 通过错误分析和数据切片帮助团队定位模型失败来自数据、标签、分布还是模型本身。
- 支持多种视觉数据格式、预测类型和评估路径，适合在训练前后建立数据/模型质量门。
- 提供 Notebook、App 和 Python API，方便研究探索与团队协作之间切换。

## 风险边界

- 可视化、筛选和评估结果依赖导入 schema、标签质量、类别映射、坐标格式、评测配置和数据切分；界面显示正确不等于数据语义正确。
- 计算机视觉数据可能包含人脸、车牌、位置、医疗图像或商业素材；本地数据库、缩略图、嵌入、缓存和导出文件都需要隐私控制。
- Dataset zoo、model zoo、插件和外部模型可能下载未审计代码/权重或受限数据；生产环境要限制网络和执行权限。
- 指标可能受类别不平衡、阈值、标注偏差、数据泄漏和切分方式影响；单个 mAP/accuracy 不能代表真实场景可靠性。
- Apache-2.0 只覆盖仓库代码；数据集、模型权重、第三方插件和用户上传内容仍按各自许可证和隐私义务处理。

## 补充建议

1. 先用公开或合成图像建立小数据集，逐项验证导入 schema、标签坐标、类别映射、导出和删除行为。
2. 对训练/验证/测试按主体、时间或场景隔离，保存数据版本、过滤条件、评测配置和错误样本清单。
3. 真实数据部署采用最小权限、加密存储、访问审计、缓存清理和明确保留期；关闭不需要的外部 zoo/插件下载。
4. 把视觉指标、人工抽检、长尾/公平性、安全场景和线上漂移分开评估，并保留模型与数据回滚路径。

## 参考资料

- [上游 README / 安装与能力概览](https://github.com/voxel51/fiftyone)
- [FiftyOne 官方文档](https://docs.voxel51.com)
- [Quickstart Notebook](https://colab.research.google.com/github/voxel51/fiftyone-examples/blob/master/examples/quickstart.ipynb)
- [安装指南](https://docs.voxel51.com/installation/index.html)
- [仓库许可证](https://github.com/voxel51/fiftyone/blob/main/LICENSE)
- [GitHub API 元数据](https://api.github.com/repos/voxel51/fiftyone)
