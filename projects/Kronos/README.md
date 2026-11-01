<!-- markdownlint-disable MD013 -->

# Kronos

- 主上游：[shiyu-coder/Kronos](https://github.com/shiyu-coder/Kronos)
- 分类：办公、商业与行业应用。
- 核验日期：2026-11-02（Asia/Shanghai）；默认分支 `master`，固定快照 `67b630e67f6a`。
- [API](https://api.github.com/repos/shiyu-coder/Kronos) 快照：45,323 stars / 7,495 forks / 294 open issues（含 PR）；发行列表当前为空。累计量不是今日增量，主线不等于发行包。

## 定位

Kronos 是针对金融 K 线序列预训练的 decoder-only 模型族。输入是 OHLC 价格与可选成交量 / 成交额，不是将新闻、公告或金融文本直接融合进模型的通用金融 LLM。本轮纠正旧页的输入与机制描述。作者报告其预训练数据来自 45 个以上交易所，当前公开 mini / small / base，large 在模型表中仍未开放。[README.md](https://github.com/shiyu-coder/Kronos/blob/67b630e67f6a18c9e9be918d9b4337c960db1e9a/README.md)

## 用法

按当前仓库示例，在独立环境安装依赖并加载匹配 tokenizer / checkpoint：

```sh
git clone https://github.com/shiyu-coder/Kronos.git
cd Kronos
git checkout 67b630e67f6a18c9e9be918d9b4337c960db1e9a
python -m pip install -r requirements.txt
python examples/prediction_example.py
```

示例从 Hugging Face 加载 `Kronos-Tokenizer-base` 与 `Kronos-small`，取历史 400 条、预测未来 120 条，`max_context=512`。输入时间戳要对应真实交易频率与时区，未来时间戳只应给日历信息，不能带未来价格。当前预测器在缺 volume 时将 volume / amount 补零；已有 volume 但缺 amount 时，按 volume 乘 OHLC 均价构造 amount，这些补值不等同于真实行情字段。[README.md](https://github.com/shiyu-coder/Kronos/blob/67b630e67f6a18c9e9be918d9b4337c960db1e9a/README.md)、[examples/prediction_example.py](https://github.com/shiyu-coder/Kronos/blob/67b630e67f6a18c9e9be918d9b4337c960db1e9a/examples/prediction_example.py)、[model/kronos.py](https://github.com/shiyu-coder/Kronos/blob/67b630e67f6a18c9e9be918d9b4337c960db1e9a/model/kronos.py)

## 原理

先将连续多维 K 线用专用 tokenizer 量化为层级离散 token，再自回归预测后续 token 并解码回数值。预测器处理标准化、截断与逆标准化；temperature、top-p 和 sample_count 影响采样，多个样本被平均后的路径不等于校准过的概率区间。[README.md](https://github.com/shiyu-coder/Kronos/blob/67b630e67f6a18c9e9be918d9b4337c960db1e9a/README.md)、[model/kronos.py](https://github.com/shiyu-coder/Kronos/blob/67b630e67f6a18c9e9be918d9b4337c960db1e9a/model/kronos.py)

## 价值

适合作为金融时间序列 token 化、预训练与迁移的研究基线，也便于比较不同历史窗口和资产。预测误差、方向判断与扣费后策略表现是不同目标；可视化示例和实时 demo 不构成交易收益证据。上游也明确微调 / 回测只是简化示范。[README.md](https://github.com/shiyu-coder/Kronos/blob/67b630e67f6a18c9e9be918d9b4337c960db1e9a/README.md)

## 风险边界

- small / base 上下文上限 512，超长输入会截断；批量预测要求样本历史和预测长度一致。模型尺寸、tokenizer 与窗口不可随意混搭。[README.md](https://github.com/shiyu-coder/Kronos/blob/67b630e67f6a18c9e9be918d9b4337c960db1e9a/README.md)
- 默认微调配置的 train / validation / test 日历范围存在交叠；需继续核样本构造、窗口、标签和 purge / embargo，不能直接据此认定已经发生泄漏，也不能不复核就据其做严格独立泛化结论。默认 `use_comet=True`，不使用时应关闭并核数据出口。[finetune/config.py](https://github.com/shiyu-coder/Kronos/blob/67b630e67f6a18c9e9be918d9b4337c960db1e9a/finetune/config.py)
- 市场分布、复权、幸存者偏差、数据重叠、交易成本和滑点都会改变评估。作者历史研究 / 仓库热度不等于当前市场可获利，本轮没有策略回测。根代码 MIT，行情源和权重许可需另核。[README.md](https://github.com/shiyu-coder/Kronos/blob/67b630e67f6a18c9e9be918d9b4337c960db1e9a/README.md)、[LICENSE](https://github.com/shiyu-coder/Kronos/blob/67b630e67f6a18c9e9be918d9b4337c960db1e9a/LICENSE)

## 补充建议

先锁模型 revision、tokenizer、输入数据与交易日历，以纯时间外样本对照 last-value / 简单统计基线；报告误差分布并检查切分交叠。若研究策略，再加入费用、滑点、仓位与多重选择偏差。本轮只核源码和资料，未下载权重、训练、回测或读取交易账户。

## 参考资料

- [README.md](https://github.com/shiyu-coder/Kronos/blob/67b630e67f6a18c9e9be918d9b4337c960db1e9a/README.md)（固定 commit）。
- [model/kronos.py](https://github.com/shiyu-coder/Kronos/blob/67b630e67f6a18c9e9be918d9b4337c960db1e9a/model/kronos.py)（固定 commit）。
- [examples/prediction_example.py](https://github.com/shiyu-coder/Kronos/blob/67b630e67f6a18c9e9be918d9b4337c960db1e9a/examples/prediction_example.py)（固定 commit）。
- [finetune/config.py](https://github.com/shiyu-coder/Kronos/blob/67b630e67f6a18c9e9be918d9b4337c960db1e9a/finetune/config.py)（固定 commit）。
- [requirements.txt](https://github.com/shiyu-coder/Kronos/blob/67b630e67f6a18c9e9be918d9b4337c960db1e9a/requirements.txt)（固定 commit）。
- [LICENSE](https://github.com/shiyu-coder/Kronos/blob/67b630e67f6a18c9e9be918d9b4337c960db1e9a/LICENSE)（固定 commit）。
- [仓库 API](https://api.github.com/repos/shiyu-coder/Kronos)、[发行列表](https://github.com/shiyu-coder/Kronos/releases)（动态状态）。
