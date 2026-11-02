<!-- markdownlint-disable MD013 -->

# Neural Networks: Zero to Hero：从反向传播到 GPT 的代码课程

- 上游：[karpathy/nn-zero-to-hero](https://github.com/karpathy/nn-zero-to-hero)；分类：AI 学习与教育资源。
- 更新：2026-11-03（Asia/Shanghai）；固定主线 SHA：`73c3fcc741f0ec104ca850b1fb0df90e7e8d4cde`。
- 热度快照：Jupyter Notebook daily +45；API 25,233 stars / 3,674 forks / 54 open issues（含 PR）。发行列表为空。
- 证据：官方 Trending / API 与固定源码静态核读；下文用法供复核，不表示本轮已运行。

## 定位

Andrej Karpathy 的神经网络课程以视频边写边讲，仓库保存部分课堂 notebook。顺序覆盖 micrograd、字符级 bigram、MLP、BatchNorm、手写反向传播、WaveNet 风格网络、GPT 和 tokenizer。适合理解机制与调试，先修为基础 Python 和微积分。

## 用法

克隆后按 README 的视频顺序进入 lectures，使用独立 Python / Jupyter 环境。首个 micrograd notebook 静态导入 NumPy、Matplotlib 和 graphviz；Graphviz 渲染还需系统可执行程序。后续 notebook 使用 PyTorch 等，应按具体课件检查依赖。

```sh
git clone https://github.com/karpathy/nn-zero-to-hero
cd nn-zero-to-hero
```

先完成微分与梯度练习，再进入 makemore。README 的 GPT 与 tokenizer 课通过视频说明 / 外部代码仓库继续：当前完整树只有七个 notebook，不能把八个课程条目都写成仓库内有对应 notebook。练习链接在视频描述中。

## 原理

- 先用标量计算图和局部导数累积解释链式法则，再转向张量与训练循环。
- 字符级自回归模型用前文预测下一个字符，从计数 bigram 逐步增加 embedding、隐藏层和更长上下文。
- 手写反传练习把交叉熵、线性层、tanh、BatchNorm 的梯度拆开，帮助定位维度、广播与归一化错误。
- GPT 讲解注意力与语言建模，tokenizer 单独讲 BPE、encode / decode；分词与神经网络训练是不同环节。

## 价值

同一问题由简单实现逐步扩展，容易把公式、张量形状和代码行对应起来。适合作为读现代训练 / 推理框架前的机制基础，也能为自动微分测试提供小规模人工参照。

## 风险边界

- 课程和视频属于长期资源，当前 GitHub 日增不表示新课发布；示例规模、数据集与模型不是前沿大模型能力的替代证据。
- 仓库没有根级统一依赖锁或安装清单；旧 notebook 保存的输出不能视为当前环境可复现。
- MIT 覆盖仓库代码；外部视频、Colab、数据与关联仓库的使用范围要分别核对。
- 本轮只核 README、完整文件树、首个 notebook 导入和许可证；未执行 notebook、训练网络或完整观看视频。

## 补充建议

1. 自己完成有限差分与手写反传，再同自动微分结果比较；保存输入、误差容差和随机种子。
2. 每课记录 tensor shape、训练 / 验证划分、loss 与采样设置，分开观察拟合与泛化。
3. 选定一课建立独立依赖记录和可重复命令，避免为整套历史课程强配同一环境。

[GPT 讲座](https://www.youtube.com/watch?v=kCc8FmEb1nY) 的作者与标题已用 YouTube 元数据核对；本轮未从视频推断教学成效。

## 参考资料

- [README.md](https://github.com/karpathy/nn-zero-to-hero/blob/73c3fcc741f0ec104ca850b1fb0df90e7e8d4cde/README.md)。
- [lectures/micrograd/micrograd_lecture_first_half_roughly.ipynb](https://github.com/karpathy/nn-zero-to-hero/blob/73c3fcc741f0ec104ca850b1fb0df90e7e8d4cde/lectures/micrograd/micrograd_lecture_first_half_roughly.ipynb)。
- [LICENSE](https://github.com/karpathy/nn-zero-to-hero/blob/73c3fcc741f0ec104ca850b1fb0df90e7e8d4cde/LICENSE)。
- [仓库 API](https://api.github.com/repos/karpathy/nn-zero-to-hero)；本轮发行列表为空。
