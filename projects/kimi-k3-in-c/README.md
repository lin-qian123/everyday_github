<!-- markdownlint-disable MD013 -->

# kimi-k3-in-c：用磁盘流式读取换取低常驻内存的 C99 推理引擎

- 上游：[FareedKhan-dev/kimi-k3-in-c](https://github.com/FareedKhan-dev/kimi-k3-in-c)；repository ID `1319154759`。
- 更新：2026-11-05（Asia/Shanghai）；分类：模型、训练与推理基础设施。
- 固定 main SHA：`81bb6c23ccee2154bc35cad922588ab66494a9a9`；API 10,255 stars / 1,625 forks / 26 open issues（含 PR）；综合 daily +351。
- 发行列表首项 v1.1.0，UTC 2026-10-02；Apache-2.0 代码与模型自身许可分别适用。
- 核验范围：官方榜单、仓库 API、完整树、固定文档 / I/O 实现与模型元数据；未编译、下载权重或复现数值与性能。

## 定位

为 Kimi K3 文本推理实现便于阅读的 CPU C99 引擎，重点是权重读取、MoE 专家缓存、dense trunk 分层驻留及增量状态。“2.78T、8.24 GB”是上游对模型总参数和某次运行峰值 RSS 的说明，不表示全部权重压缩到 8 GB，也不是普通笔记本实时聊天的实测结论。

## 用法

先在隔离目录固定源码，只做不需要模型的编译与 fixture 检查：

```sh
git clone https://github.com/FareedKhan-dev/kimi-k3-in-c.git
cd kimi-k3-in-c
git checkout 81bb6c23ccee2154bc35cad922588ab66494a9a9
make -j
make test
```

上游要求 GCC 9+ 或 Clang 10+；x86-64 主路径使用 AVX2 / FMA，arm64 有 NEON 路径。上述测试包含小型合成参考，不能替代完整模型验收。

完整推理另外需要约 1.56 TB checkpoint 和约 109 GB packed trunk，建议预留约 1.7 TB 磁盘；下载 / 打包工具需要 Python 3.9+。先核模型版本、许可与空间，再按上游 Full setup 执行。批处理默认 greedy；`--chat` 为文本 XTML 多轮入口，`--preset ultra`、`laptop`、`server` 决定驻留 / 缓存预算。v1.1.0 的保存状态改为 v2，旧 v1 文件须重新生成。

## 原理

- safetensors 读取器按需读取权重；MoE 每层路由 16 / 896 个专家，并直接使用已发布 MXFP4 表示，减少不活跃专家的驻留需求。
- trunk 按层选择固定内存或从磁盘读取；所读 `k3_trunk.c` 有分块读取和预取同步，I/O 调度也是正确性约束的一部分。
- KDA 递归状态与 MLA 压缩注意力状态减少历史上下文存储；专家 LRU、trunk 预算和增量状态共同决定速度与 RSS。
- 上游用 token / logits 对照、缓存 trace 和原始运行记录建立验收链；“相同输出”声明只覆盖对应配置、输入和参考路径。

## 价值

适合研究模型总大小、活跃计算、常驻工作集与磁盘带宽之间的关系，也可作为 C 推理和文件格式防御性解析的学习材料。节省 RAM 的代价转移到存储容量与逐 token I/O，采用价值需按实际硬件和时延预算判断。

## 风险边界

- README 顶部 8 / 32 / 64 / 128 GB 的时间比较来自同一台有 124 个可见 CPU、快速 NVMe 的机器；表格的“笔记本”标签不是多款笔记本测试。8.24 GB 峰值也不保证物理 8 GB 主机无交换运行。
- 顶部“128 GB+ 模型全部驻留”措辞与后文约 1.45 TB 专家按需读取的机制不一致；不能据此认为完整 checkpoint 驻留 RAM。应检查实际读取字节、页缓存、专家命中率和 RSS。
- Jetson 文档是四次同一短提示、生成一个 token 的上游记录，平均约 949.4 秒，峰值约 2.573 GiB；证明范围是该配置完成路径，不是交互速度、通用能力或本轮独立复现。
- 上游基准文档记录相同配置三次时间 spread 约 33%；这是特定样本的波动，不能当所有硬件通用的统计显著性阈值。固定生成长度、冷 / 热缓存、存储和线程，并报告各次数据。
- 当前范围为文本聊天，不含视觉编码器、工具调用、HTTP serving 或 context compaction；文档明确没有 perplexity / 下游任务质量 benchmark。fixture 一致不证明全部模型语义或全部平台正确。
- Apache-2.0 只描述引擎代码。Hugging Face 模型元数据的 license 为 `other`，使用与再分发权重需另核模型许可；本轮只核模型身份，未审查其全部条款。

## 补充建议

先验证无权重测试，再用固定模型 revision、短输入和预期 token / logits 验证完整路径；分别记录 RSS、系统总内存 / 页缓存、磁盘占用、每 token 读取量及墙钟时间。性能比较用重复运行和完整配置，不从短提示或一个 token 推断生产适用性。

## 参考资料

- [README、安装与范围](https://github.com/FareedKhan-dev/kimi-k3-in-c/blob/81bb6c23ccee2154bc35cad922588ab66494a9a9/README.md)、[v1.1.0](https://github.com/FareedKhan-dev/kimi-k3-in-c/releases/tag/v1.1.0)。
- [基准方法](https://github.com/FareedKhan-dev/kimi-k3-in-c/blob/81bb6c23ccee2154bc35cad922588ab66494a9a9/docs/BENCHMARKING.md)、[参考环境](https://github.com/FareedKhan-dev/kimi-k3-in-c/blob/81bb6c23ccee2154bc35cad922588ab66494a9a9/docs/data/environment.txt)、[内存阶梯原始表](https://github.com/FareedKhan-dev/kimi-k3-in-c/blob/81bb6c23ccee2154bc35cad922588ab66494a9a9/docs/data/memory-ladder.tsv)。
- [Jetson 单 token 记录与来源](https://github.com/FareedKhan-dev/kimi-k3-in-c/blob/81bb6c23ccee2154bc35cad922588ab66494a9a9/docs/results/jetson-orin-nano-super/README.md)、[trunk I/O 实现](https://github.com/FareedKhan-dev/kimi-k3-in-c/blob/81bb6c23ccee2154bc35cad922588ab66494a9a9/src/io/k3_trunk.c)。
- [引擎 API](https://api.github.com/repos/FareedKhan-dev/kimi-k3-in-c)、[模型元数据](https://huggingface.co/api/models/moonshotai/Kimi-K3)。
