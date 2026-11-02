<!-- markdownlint-disable MD013 -->

# MLX：惰性数组计算、自动微分与多后端机器学习

- 上游：[ml-explore/mlx](https://github.com/ml-explore/mlx)；分类：模型、训练与推理基础设施。
- 更新：2026-11-03（Asia/Shanghai）；固定主线 SHA：`ba8c005c1b687227ff79a55da5b8aa062d92541f`。
- 热度快照：C++ daily +19；API 29,029 stars / 2,398 forks / 122 open issues（含 PR）。最新发行 v0.32.4，UTC 2026-10-14；PyPI 同为 0.32.4，Python >=3.10。
- 证据：官方 Trending / API 与固定源码静态核读；下文用法供复核，不表示本轮已运行。

## 定位

MLX 由 Apple 机器学习研究团队发起，是具有 NumPy 风格数组接口、自动微分、向量化、神经网络和优化器的计算框架。它以 Apple silicon 体验著称，但当前官方安装说明也覆盖 Linux CUDA 和 CPU 包，不宜继续概括为“只能在 Mac 上运行”。

## 用法

Apple silicon 路线要求原生 Python >=3.10、macOS >=14.0；建议在独立环境固定已核版本：

```sh
python -m pip install "mlx==0.32.4"
```

最小数组 / 梯度检查可按以下思路执行；本轮没有运行该示例：

```python
import mlx.core as mx

x = mx.array([1.0, 2.0, 3.0])
y = mx.sum(x * x)
g = mx.grad(lambda a: mx.sum(a * a))(x)
mx.eval(y, g)
print(y, g)  # 预期 14 与 [2, 4, 6]
```

Linux 按环境选择 mlx[cpu]、mlx[cuda12] 或 mlx[cuda13]。当前文档要求 glibc >=2.35；CUDA 12 路线还要求 SM >=7.5、driver >=550.54.14、toolkit >=12.0，CUDA 13 的 driver 门槛是 >=580 或适配兼容包。README 的 cuda 通用入口与详细安装页的具体 extras 要结合 wheel 元数据核对。

## 原理

- 数组运算先构造计算图，显式 mx.eval、打印、读取数组内存等操作再触发求值。
- grad / vmap 等函数变换可组合；动态构图与图优化支持研究迭代。
- Apple silicon 统一内存让 CPU / GPU 共享数组所在内存池，操作选择 device / stream，无需显式复制数组到另一个设备。此架构描述不应直接外推到 Linux 独立显存硬件。
- 训练循环需要在合适的位置求值参数与状态；每步过细求值增加调度开销，长期不求值也会积累图。

## 价值

适合 Mac 上的数组、梯度与模型原型，以及在同一接口下探索 CPU / GPU 分工。C++、Python 和独立 C / Swift 生态提供接入选择；MLX 本体不是完整聊天服务，模型加载、量化和应用层仍须另选组件。

## 风险边界

- 统一内存不代表内存无限或所有算子都更快；模型权重、KV cache、中间张量和系统余量应一起计算。
- 比较性能必须包括求值 / 同步、冷启动与预热；仅计时 Python 构图会低估实际计算时间。
- 发行说明包含梯度、stride、归约与内存修复，采用时应核目标算子、dtype、梯度和后端覆盖，不能从框架支持推出数值等价。
- 本体 MIT 不覆盖任意模型权重和数据。本轮未安装框架、下载模型或执行性能 / 梯度测试。

## 补充建议

1. 从解析梯度和小矩阵运算验证 dtype、容差与求值时机，再扩展到完整模型。
2. 固定 OS、芯片、wheel、模型、上下文长度和 batch，同时记录峰值内存及吞吐。
3. 把 Apple 统一内存实验与 Linux CUDA 实验分别报告，避免混用硬件结论。

## 参考资料

- [README.md](https://github.com/ml-explore/mlx/blob/ba8c005c1b687227ff79a55da5b8aa062d92541f/README.md)。
- [docs/src/install.rst](https://github.com/ml-explore/mlx/blob/ba8c005c1b687227ff79a55da5b8aa062d92541f/docs/src/install.rst)。
- [docs/src/usage/unified_memory.rst](https://github.com/ml-explore/mlx/blob/ba8c005c1b687227ff79a55da5b8aa062d92541f/docs/src/usage/unified_memory.rst)。
- [docs/src/usage/lazy_evaluation.rst](https://github.com/ml-explore/mlx/blob/ba8c005c1b687227ff79a55da5b8aa062d92541f/docs/src/usage/lazy_evaluation.rst)。
- [LICENSE](https://github.com/ml-explore/mlx/blob/ba8c005c1b687227ff79a55da5b8aa062d92541f/LICENSE)。
- [仓库 API](https://api.github.com/repos/ml-explore/mlx)；[发行记录](https://github.com/ml-explore/mlx/releases/tag/v0.32.4)。
