<!-- markdownlint-disable MD013 -->

# pytorch-deep-learning：从张量到实验与部署的代码课程

- 上游：[mrdbourke/pytorch-deep-learning](https://github.com/mrdbourke/pytorch-deep-learning)，repository ID `418718534`；2026-11-27 新建档案。
- 快照：19,486 stars / 5,244 forks / 151 open issues（累计，含 PR）；Jupyter Notebook daily +12。
- 默认 SHA `a16552001d963d078390d5bbdfc321e7e7c94bd1`，2026-09-27；提交修复 notebook 的旧 widget metadata，所见 Releases 为空。再次上榜不代表课程、框架或模型今日更新。
- 范围：README、SETUP、01 notebook 及模块化训练 / 数据 / 保存文件静态核读；未安装依赖、运行 notebook、下载数据 / 权重、启动 Colab 或部署服务。

## 定位

Daniel Bourke 的 Zero to Mastery PyTorch 入门课程资料，面向已有基础 Python 能力的学习者。它以实际写代码为主，涵盖 00–09：张量、训练流程、分类、视觉、自定义数据、模块化、迁移学习、实验记录、论文复现和部署，贯穿 FoodVision 食物图像分类项目。

在线书和仓库材料可读；README 链接的免费长视频只覆盖前五节，完整付费视频课程是另一个交付范围。作者的“课程已完成”不等于本轮逐节重跑或当前环境已验收。

## 用法

1. 从 00 的张量形状、dtype、device 开始，再按 01–04 理解数据、模型、训练和评估，先自己写一遍代码，再对照练习与解答。
2. 固定本页 SHA，另记录 Python、PyTorch、torchvision 和设备。SETUP 的 Linux 示例仍是 Python 3.8.13、PyTorch 1.10.0、CUDA Toolkit 11.3，且有 TK / TODO；这属于历史示例，不是当前全平台安装保证。
3. Colab 与本地 Jupyter 是两个入口；使用云 notebook 时先确认数据上传与运行时生命周期。SETUP 对免费 GPU / 超时的历史描述不能作为当前配额承诺。
4. 05 的可执行模块位于双层路径 `going_modular/going_modular/`；不要将外层同名目录直接当成 `engine.py` 所在位置。
5. 到 06–09 再比较迁移学习、实验记录、论文简化复现与部署；需要下载预训练模型或开放网络服务时，单独检查资源与数据边界。

训练循环的核心顺序如下，来自所查 `engine.py` 的简化表达，未执行：

```python
model.train()
prediction = model(batch_x)
loss = loss_fn(prediction, batch_y)
optimizer.zero_grad()
loss.backward()
optimizer.step()
```

## 原理

课程把同一条工作流反复应用到不同任务：准备数据与划分集合，构造 `torch.nn.Module`，前向计算损失，通过 autograd 求梯度并更新参数，再用 `model.eval()` 和 `torch.inference_mode()` 评估。

01 用简单线性数据展示参数拟合，并用前 80% / 后 20% 顺序切片帮助理解训练与测试。这个教学切分并非所有实际数据的通用方案：时间、同一对象或重复样本可能要求按时间 / 组拆分。

模块化版本将 DataLoader、模型、训练与保存拆开。其 `train()` 每个 epoch 调用 `test_step()`，同时记录曲线；所查 `save_model()` 保存的是 `state_dict()`，并没有同时保存优化器、epoch、随机状态和完整实验配置。

## 价值

它将框架 API、完整循环和工程拆分连起来，适合建立可修改的基线，练习从 notebook 迁移到脚本。练习、解答、可读书稿和长视频给出了多种对照途径。

08 的论文复现与 FoodVision 项目适合作为学习实验设计的起点；不能只凭示例图、课程完成度或累计播放量认定复现了原论文全部规模与指标。

## 风险边界

| 议题 | 已核事实与边界 |
| --- | --- |
| 依赖年代 | README 的 PyTorch 2.0 兼容声明来自 2023 年，SETUP 仍有更旧安装组合；本轮未找到或验收统一全课程锁定环境。 |
| 指标聚合 | `engine.py` 先算每个 batch 的 loss / accuracy，再除以 batch 数。末批大小不等时，得到的是等 batch 权重平均，不能直接当严格逐样本总体指标。 |
| 验证与测试 | 每 epoch 查看 `test` 曲线可用于教学；若据此调超参数，它已参与选择，应另留独立最终测试集。文件命名本身不保证独立性。 |
| 保存与恢复 | `state_dict` 是模型参数状态；恢复训练还需要优化器、调度器、随机状态和数据位置等，保存成功不等于可无缝接续。 |
| 计算与隐私 | 预训练模型、数据集、Colab、实验平台和部署各有下载 / 上传与资源成本；本地 notebook 文件不代表所有步骤离线。 |
| 复用 | 仓库 LICENSE 为 MIT；外部数据、预训练权重、平台与课程视频的条件另核，不把源码许可外推到所有关联材料。 |

## 补充建议

1. 为选定章节建立独立环境，保存实际依赖和设备记录；先验证一个小 CPU 任务，再扩到 GPU。
2. 把教学 `test` 与最终盲测分开；按样本数聚合指标，并检查类别不平衡、重复图片与分组泄漏。
3. 保存输入预处理、类别顺序、数据划分、配置与完整训练状态，实际验证重开后的预测一致性和训练恢复。
4. 将论文复现标注为所用数据、训练量和设备下的结果；新任务先做冻结基线，再解释改进来源。

## 参考资料

- [仓库 API](https://api.github.com/repos/mrdbourke/pytorch-deep-learning)、[固定 README](https://raw.githubusercontent.com/mrdbourke/pytorch-deep-learning/a16552001d963d078390d5bbdfc321e7e7c94bd1/README.md)、[SETUP](https://raw.githubusercontent.com/mrdbourke/pytorch-deep-learning/a16552001d963d078390d5bbdfc321e7e7c94bd1/SETUP.md)、[在线书](https://www.learnpytorch.io/)。
- [01 工作流 notebook](https://raw.githubusercontent.com/mrdbourke/pytorch-deep-learning/a16552001d963d078390d5bbdfc321e7e7c94bd1/01_pytorch_workflow.ipynb)、[模块化训练与指标](https://raw.githubusercontent.com/mrdbourke/pytorch-deep-learning/a16552001d963d078390d5bbdfc321e7e7c94bd1/going_modular/going_modular/engine.py)、[数据加载](https://raw.githubusercontent.com/mrdbourke/pytorch-deep-learning/a16552001d963d078390d5bbdfc321e7e7c94bd1/going_modular/going_modular/data_setup.py)、[模型保存](https://raw.githubusercontent.com/mrdbourke/pytorch-deep-learning/a16552001d963d078390d5bbdfc321e7e7c94bd1/going_modular/going_modular/utils.py)。
- [README 关联视频](https://www.youtube.com/watch?v=Z_ikDlimN6A)、[MIT LICENSE](https://raw.githubusercontent.com/mrdbourke/pytorch-deep-learning/a16552001d963d078390d5bbdfc321e7e7c94bd1/LICENSE)。
