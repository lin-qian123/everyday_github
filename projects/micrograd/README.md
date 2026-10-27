<!-- markdownlint-disable MD013 -->

# micrograd：用标量计算图看清反向传播

- 主上游：[karpathy/micrograd](https://github.com/karpathy/micrograd)；repository ID `255231293`。
- 采样日期：2026-10-28（Asia/Shanghai）；分类：AI 学习与教育资源。
- API 累计快照：18,171 stars / 2,900 forks / 81 open issues（含 PR 口径），与榜单日增分开。
- 默认分支 `master`；主线依据固定在 `7bc720e951fe422b8f8814aa5aa1b64121d26b4c`。发行 API 本轮返回空列表；此状态不代表没有源码标签或其他分发渠道。
- 核验层级：一手文档、元数据和所列部分实现的静态阅读；未安装运行、调用模型、复现基准或验证真实用户效果。

## 定位

micrograd 是教学用的小型自动微分引擎，以及叠加其上的神经网络库。它把每个神经元拆成标量加乘，以动态有向无环图演示链式法则和反向传播；不是用于大模型训练的高性能 tensor 框架。

## 用法

在专用 Python 环境按 README 安装 `micrograd`，或从固定源码研究实现。最小示例：

```python
from micrograd.engine import Value

x = Value(3.0)
y = x * x + x
y.backward()
print(y.data, x.grad)
```

按公式预期为 `12.0` 和 `7.0`，这是可手算的示例预期，**本轮未执行**。再读 `demo.ipynb` 的二分类和 `trace_graph.ipynb` 的计算图；上游测试以 PyTorch 为参照，运行测试需要额外安装 PyTorch，本轮没有运行。

## 原理

`Value` 保存数值、梯度、前驱节点与每个算子的反向闭包。`backward()` 先递归构造拓扑序，再逆序累加局部梯度。`Neuron`、`Layer`、`MLP` 组合这些标量运算，Module 提供参数列表和 `zero_grad()`；优化步骤由使用者编写。

## 价值

适合在课程中逐行解释共享节点、梯度累加、ReLU 与训练循环，并对照手算、有限差分和 PyTorch。源码可读性有助于理解算法；上游有参照测试不等于覆盖所有表达式、数值范围或深图。

## 风险边界

- 只处理标量计算，缺少生产 tensor 框架的向量化、GPU 和成熟算子体系；不能由二分类演示外推大模型吞吐或训练能力。
- 反向传播通过 `+=` 累加，不能把对同一图反复调用 backward 当作每次自动清零的新梯度；训练应清参数梯度、重新前向构图，并理解中间节点状态。
- 除法、幂和深递归仍受 Python 数值与调用栈约束，未提供完整的形状、定义域和数值稳定性保护。
- README 的 microgpt 链接是另一个实现，不能把它的 Transformer 能力归给 micrograd 本仓库。
- MIT；示例与测试的依赖、图形工具另需准备。发行 API 本轮无条目，不等于 PyPI 无包或项目没有使用者。

## 补充建议

从共享变量 `x*x+x` 开始，手算后用有限差分与独立框架交叉检查，再测试梯度清零、分支图、ReLU 零点及不同随机种子。把教学正确性和性能目标分开记录。

## 参考资料

- [README.md](https://github.com/karpathy/micrograd/blob/7bc720e951fe422b8f8814aa5aa1b64121d26b4c/README.md)。
- [micrograd/engine.py](https://github.com/karpathy/micrograd/blob/7bc720e951fe422b8f8814aa5aa1b64121d26b4c/micrograd/engine.py)。
- [micrograd/nn.py](https://github.com/karpathy/micrograd/blob/7bc720e951fe422b8f8814aa5aa1b64121d26b4c/micrograd/nn.py)。
- [LICENSE](https://github.com/karpathy/micrograd/blob/7bc720e951fe422b8f8814aa5aa1b64121d26b4c/LICENSE)。
- [setup.py](https://github.com/karpathy/micrograd/blob/7bc720e951fe422b8f8814aa5aa1b64121d26b4c/setup.py)。
- [test/test_engine.py](https://github.com/karpathy/micrograd/blob/7bc720e951fe422b8f8814aa5aa1b64121d26b4c/test/test_engine.py)。
- [仓库 API](https://api.github.com/repos/karpathy/micrograd)、[发行 API](https://api.github.com/repos/karpathy/micrograd/releases?per_page=1)；动态字段只代表本轮采样。
- 事实依据为以上一手材料；价值、风险推论与补充建议为本库工程分析。
