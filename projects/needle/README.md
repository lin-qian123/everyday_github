<!-- markdownlint-disable MD013 -->

# Needle

## 定位

[`cactus-compute/needle`](https://github.com/cactus-compute/needle) 是 Cactus Compute 发布的端侧小型工具调用与结构化抽取模型。上游 README 将 Needle 2 描述为 45M 参数、单个约 14 MB 引擎文件的模型；仓库提供 Python 推理、LoRA 微调与导出工具。它的目标不是替代通用长上下文助手，而是在手机、可穿戴设备、嵌入式控制器等受内存和网络约束的场景，完成已定义 schema 内的工具选择、参数填写或结构化抽取。

## 用法

```bash
pip install cactus-needle
```

```python
import needle

@needle.tool
def get_weather(city: str):
    "Get the current weather for a city."
    return {"city": city, "temp_c": 27}

agent = needle.Needle(tools=[get_weather])
print(agent.run("what's it like in Lagos right now?")["results"])
```

结构化抽取可将 Pydantic 模型传给 `needle.extract()`；微调流程为 JSONL 数据、LoRA 训练、再导出 `.cact` 文件。首次下载推理引擎与权重的网络行为、离线缓存和硬件后端，应按上游 [API 文档](https://github.com/cactus-compute/needle/blob/main/doc/apis.md) 单独验证。

## 原理

- 上游采用 Simple Attention Network，并声称结合 Hadamard MLP、GQA、engram KV memory 与多通道 hyper-connections；具体结构和消融应以其 [论文](https://arxiv.org/abs/2607.18363) 为准。
- 工具调用将输入工具 schema 编译为字节级解码语法，从而限制输出形状；这降低格式错误，但不证明工具选择、参数语义或外部事实正确。
- 运行时保留 256-token 滑动窗口并固定工具 token；大工具目录先由检索头选出候选，再在该子集内生成。其置信度分数可用于阈值化升级人工，但阈值必须在自身任务分布上校准。

## 价值

- 把“文本到受限 JSON/函数参数”的路径压缩到小型、本地可部署的运行单元，适合网络不稳定、响应时间或数据外发受限的原型。
- 同一仓库覆盖推理、schema 约束、LoRA 和导出，便于做端侧工具调用的可复现实验。
- GitHub API 于 2026-08-16 的快照为约 6.1k stars、402 forks、MIT；GitHub Trending 页面当时显示约 +551 stars/day。这只是短期公开关注度，不是模型质量、延迟、能耗或安全认证。

## 风险边界

- 14 MB、28 MB RAM、对比基准与置信度校准均来自项目方材料；在目标设备、语言、工具数量和异常输入下未由本仓库独立复现。
- schema 约束不能阻止已授权但不合意的动作。真正执行支付、门锁、医疗、工业或删除类工具时，仍要在工具侧实施最小权限、allowlist、参数范围、确认与审计。
- 合成数据流程需要 API key；日志、训练数据与工具结果可能包含敏感信息。不得将密钥或真实用户数据直接写入演示 JSONL。
- MIT 覆盖仓库许可证，不自动覆盖下载权重、第三方依赖或训练数据的全部权利义务。

## 补充建议

1. 先用无副作用、可重放的 mock tools 测量 schema 合法率、参数准确率、拒答/升级率、端到端延迟和峰值内存。
2. 将高风险工具拆成“提议—人工确认—执行”三段，并保存输入、模型置信度、最终审批与工具返回值。
3. 与相同约束下的规则解析器及较大模型比较；不要只以项目方榜单或单一成功率决定上线。
4. 锁定 Python 包、引擎和权重版本，记录哈希与设备配置，再评估离线安装及回滚。

## 参考资料

- [GitHub 仓库](https://github.com/cactus-compute/needle)
- [上游 README / Quickstart](https://github.com/cactus-compute/needle#quickstart)
- [API 与离线设置说明](https://github.com/cactus-compute/needle/blob/main/doc/apis.md)
- [Needle 2 权重页](https://huggingface.co/Cactus-Compute/needle2)
- [Simple Attention Network 论文](https://arxiv.org/abs/2607.18363)
- [GitHub REST API 元数据快照](https://api.github.com/repos/cactus-compute/needle)
