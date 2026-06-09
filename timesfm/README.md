# TimesFM（google-research/timesfm）

> 更新日期：2026-04-08（Asia/Shanghai）  
> 项目地址：https://github.com/google-research/timesfm

## 为什么今天值得关注

- GitHub Trending（Today）显示：`google-research/timesfm` 当日约 `380 stars today`。
- 仓库总量（抓取时）：约 `15.4k stars`、`1.4k forks`。
- 这是少数“可直接用于生产预测任务”的时序基础模型开源项目，热度来自“零样本可用 + 可扩展 + 统一API”。

## 这个项目是做什么的

TimesFM 是 Google Research 开源的时序基础模型（Time Series Foundation Model），用于时间序列预测。和传统“每个数据集单独训练一个模型”不同，它走的是 foundation model 路线：

- 先在大规模时序语料上预训练；
- 再在新任务上做零样本/少样本预测；
- 统一覆盖不同历史窗口长度、预测跨度、时间粒度。

适合场景：销售/流量预测、容量规划、金融序列、IoT监控、运营指标预测等。

## 快速上手（官方推荐）

### 1) 安装

```bash
git clone https://github.com/google-research/timesfm.git
cd timesfm
uv venv
source .venv/bin/activate
uv pip install -e .[torch]
```

可选：

- `uv pip install -e .[flax]`（Flax/JAX 后端）
- `uv pip install -e .[xreg]`（外生变量支持）

### 2) 最小预测示例（基于 README 示例改写）

```python
import numpy as np
import timesfm

model = timesfm.TimesFM_2p5_200M_torch.from_pretrained(
    "google/timesfm-2.5-200m-pytorch"
)

model.compile(
    timesfm.ForecastConfig(
        max_context=1024,
        max_horizon=256,
        normalize_inputs=True,
        use_continuous_quantile_head=True,
        force_flip_invariance=True,
        infer_is_positive=True,
        fix_quantile_crossing=True,
    )
)

point_forecast, quantile_forecast = model.forecast(
    horizon=12,
    inputs=[
        np.linspace(0, 1, 100),
        np.sin(np.linspace(0, 20, 67)),
    ],
)
```

输出：

- `point_forecast`：点预测
- `quantile_forecast`：分位数预测（可做不确定性区间）

## 原理（重点）

TimesFM 的核心是“decoder-only + patched time-series attention”：

1. **Decoder-only 架构**
- 借鉴 LLM 的自回归生成思路，在时序上做下一段预测。

2. **Patch 化序列表示**
- 把原始序列分块（patch）送入注意力网络，兼顾长上下文与计算效率。

3. **大规模预训练 + 零样本泛化**
- 在大规模时序数据预训练后，不用每个场景都从零训练。

4. **分位数头（Quantile Head）**
- 不只给单点值，还能给置信区间，适合风险敏感业务。

## 2.5 版本你该知道的变化

仓库更新说明给出的关键点：

- 参数量从 500M 降到 200M；
- 上下文长度支持从 2048 提升到 16k；
- 支持连续分位数预测（到 1k horizon，配可选 30M quantile head）；
- 重新补回了 covariate（XReg）支持。

这意味着：推理成本下降、长序列能力变强、生产上可控性更高。

## 实际落地建议

- 把 TimesFM 当作“强基线模型”先跑通，再和你现有 Prophet/XGBoost/LSTM 对比。
- 业务侧至少监控三类指标：
  - 点预测误差（MAE/MAPE）
  - 区间覆盖率（P90/P95）
  - 极端波动时段误差
- 若强季节性 + 强外部驱动（促销、天气、节假日），优先启用 covariate 路径。

## 风险与争议

- foundation model 在“你所在行业的极端分布”未必稳定；
- 零样本表现通常强于传统默认基线，但不一定在每个垂类都 SOTA；
- 金融/供应链等高风险场景，仍需人类审计与回测机制。

## 参考来源

- GitHub Trending（Today）：https://github.com/trending?since=daily
- 仓库主页：https://github.com/google-research/timesfm
- 论文（ICML 2024）：https://arxiv.org/abs/2310.10688
- Google Research 博文：https://research.google/blog/a-decoder-only-foundation-model-for-time-series-forecasting/
- Hugging Face 模型集合：https://huggingface.co/collections/google/timesfm-release-66c3f8b0f5f3abf53f6d0172
