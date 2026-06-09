# heretic

## 为什么是今天的热门
GitHub 今日趋势榜单显示 `p-e-w/heretic` 处于靠前位置，并标注“stars today”快速增长（约 946）。citeturn1search2

## 这是什么
Heretic 是一个**全自动**的“去安全对齐/去审查（decensor）”工具，用于移除语言模型中的拒答/安全对齐行为，基于“方向消融（directional ablation, 又称 abliteration）”思想，通过优化器在“减少拒答”与“保持模型质量（KL 偏差）”之间做权衡。citeturn2search0

## 能做什么（关键能力）
- **全自动流程**：无需人工微调与复杂手工调参，自动搜索消融权重。citeturn2search0
- **减少拒答同时尽量保留能力**：目标是共同最小化拒答率与 KL divergence，保持模型质量。citeturn2search0
- **支持多种模型形态**：对稠密 Transformer 模型有效；部分多模态模型也可行，但不支持 SSM/Hybrid 等架构。citeturn2search0

## 工作原理（简述）
1. **方向消融**：计算“拒答方向”，对关键权重矩阵做正交化/消融，降低拒答行为。citeturn2search0
2. **跨层权重优化**：引入可参数化的层间权重，用 Optuna TPE 优化器搜索最优消融比例，以平衡拒答率和 KL 偏差。citeturn2search0
3. **无需昂贵后训练**：避免 RLHF/再训练的成本，直接在权重空间进行操作。citeturn2search0

## 快速上手

### 安装与环境
```bash
pip install -U heretic-llm
```
citeturn2search0turn2search1

- Python 3.10+，PyTorch 2.2+。citeturn2search0

### 最小示例
```bash
heretic Qwen/Qwen3-4B-Instruct-2507
```
citeturn2search0

### 配置与量化（可选）
- 默认配置文件：`heretic/config.default.toml`。citeturn2search1
- 支持 bitsandbytes 量化，例如 `quantization = "bnb_4bit"`。citeturn2search1

## 使用注意
- Heretic 明确以“去安全对齐/去审查”为目标，实际使用需考虑合规、伦理与安全风险。

## 参考链接

```text
https://github.com/p-e-w/heretic
https://pypi.org/project/heretic-llm/
https://github.com/trending
```
