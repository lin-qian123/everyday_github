<!-- markdownlint-disable MD013 -->

# BigMoeOnEdge

- 上游：[Helldez/BigMoeOnEdge](https://github.com/Helldez/BigMoeOnEdge)；分类：**模型、训练与推理基础设施**。
- 核验：2026-11-18（Asia/Shanghai）07 时段；仓库 ID `1296688895`，main `85a0a5c0db95d2811bb65c08b236f966eaf9fd8f`。本轮只核文档和部分源码，未下载模型、安装或跑性能实验。
- 热度：官方 C++ daily **+46**；[API](https://api.github.com/repos/Helldez/BigMoeOnEdge)累计 **1,010 stars / 103 forks / 63 open issues（含 PR）**。
- 发行：列表首项 [v0.44.0](https://github.com/Helldez/BigMoeOnEdge/releases/tag/v0.44.0)，UTC 2026-11-17 08:44，**标记为 prerelease**；tag 指向 `5e7e05fdd63fd2acb09bb380fea70e1c7872d210`，与本页 main 快照分开。

## 定位

基于 llama.cpp 的 MoE 流式推理与资源规划工具：让模型完整文件留在闪存，把公共权重和常用专家放入内存 / 显存，按路由读取剩余专家。提供 CLI、本地 HTTP server、桌面和移动端界面。目标是使模型文件大于 RAM 时仍能运行，不意味着任意模型都能以交互速度运行。[固定 README](https://github.com/Helldez/BigMoeOnEdge/blob/85a0a5c0db95d2811bb65c08b236f966eaf9fd8f/README.md)

## 用法

从发行页选择匹配平台的制品，先检查预发行状态、制品来源和所需后端；README 中的远程安装管道应先下载核读。已有经过核验的 CLI 与合法取得的 GGUF 后，可按上游示例：

```bash
bmoe-cli -m model.gguf --plan
bmoe-cli -m model.gguf --auto -p "Explain MoE routing."
bmoe-server -m model.gguf -c 32768
```

`--plan` 用于观察规划，`--auto` 测量并选择配置。server 默认监听 `127.0.0.1:8765`；对接 `/v1/chat/completions` 等接口前，先检查 context、模型模板、tool call 与客户端契约。联网分享时使用 key 文件并另配网络限制；本页未执行这些命令。[API / 服务文档](https://github.com/Helldez/BigMoeOnEdge/blob/85a0a5c0db95d2811bb65c08b236f966eaf9fd8f/docs/server-api.md)

## 原理

- MoE 每个 token 只激活部分专家；缓存高频专家可减少每 token 从闪存读取的字节量，其余专家按需读取。CPU / GPU 分配、cache 大小与预取重叠共同决定延迟。
- 自动规划结合可用内存、设备计算和 I/O 测量；没有路由记录时会使用先验，已有记录后再更新。规划的预测值与真实吞吐必须分开看。
- “lossless”主要描述在相同模型 / 量化 / 路由和确定性条件下，改变存储与调度不主动删专家或降精度；它不等于不同后端、采样策略或量化之间逐 token 相同。

[硬件规划](https://github.com/Helldez/BigMoeOnEdge/blob/85a0a5c0db95d2811bb65c08b236f966eaf9fd8f/docs/hardware-planning.md)、[基准方法](https://github.com/Helldez/BigMoeOnEdge/blob/85a0a5c0db95d2811bb65c08b236f966eaf9fd8f/docs/benchmark-method.md)

## 价值

对已有高速 SSD、RAM 受限且愿意接受更长响应时间的本地推理实验有价值；也能用计划和逐 token 指标区分计算、I/O 与缓存瓶颈。README 中 12 GB 手机、16 GB Apple silicon 等速度属于维护者 / 社区给定模型与设备的记录，本轮没有复现，不能转写为用户设备性能承诺。

## 风险边界

- **吞吐分母**：历史 Android 表使用固定 prompt、greedy 和 256 个生成 token；`wall_ms` 是 decode 时间，排除模型加载和 prompt prefill。热缓存、首轮、长上下文、温控和最慢 token 会改变体验，不能只报最高 tok/s。[已发布方法与记录](https://github.com/Helldez/BigMoeOnEdge/blob/85a0a5c0db95d2811bb65c08b236f966eaf9fd8f/docs/benchmarks.md)
- **数值范围**：v0.43.2 说明把 prompt-width 设备探针容差由 `1e-3` 放宽到 `1e-2`，单 token 保持 `1e-3`。这提醒使用者核固定模型的 logits / KL / 输出任务质量，不能把探针通过扩大成所有输入精确等价。[发行说明](https://github.com/Helldez/BigMoeOnEdge/releases/tag/v0.43.2)
- **版本与文档漂移**：v0.44.0 说明开始读取请求中的 temperature、top-p、seed 等，speculation 时仍保持 greedy；本页 main 的 API 文档却仍写这些字段被忽略。先固定实际制品，再验证参数是否生效，不用两份材料拼出一个已确认接口契约。
- **服务具有主机能力**：默认 loopback 且未设 key 时无认证；非 loopback 启动需要 key 或显式 `--no-api-key`。内置 Agent 的文件路径约束与同用户 shell 执行分开，服务安装还会建立登录用户的常驻服务；本机程序和凭据仍在威胁面内。[服务安全说明](https://github.com/Helldez/BigMoeOnEdge/blob/85a0a5c0db95d2811bb65c08b236f966eaf9fd8f/docs/server-api.md)
- **存储与分发**：模型仍需完整磁盘空间，持续专家读取带来 I/O 与能耗；macOS 制品 README 标明尚未 notarise，iOS 为实验性。主程序 Apache-2.0 与 llama.cpp、模型、GGUF 量化来源的条款分别核对。[安全报告政策](https://github.com/Helldez/BigMoeOnEdge/blob/85a0a5c0db95d2811bb65c08b236f966eaf9fd8f/SECURITY.md)

## 补充建议

先用能完整驻留的较小模型建立基线，再在同机同模型同量化下比较流式配置。记录制品 SHA、backend、磁盘、RAM、温度、context、TTFT、prefill、平均 / P95 decode、cache hit、I/O 字节和输出一致性；首轮与后续轮分开。还应加入长任务与工具调用测试，确认慢速输出下的业务成功率和超时行为。

## 参考资料

- [官方 C++ daily](https://github.com/trending/c++?since=daily)、[仓库 API](https://api.github.com/repos/Helldez/BigMoeOnEdge)、[Releases](https://github.com/Helldez/BigMoeOnEdge/releases)。
- [固定 Apache-2.0 许可](https://github.com/Helldez/BigMoeOnEdge/blob/85a0a5c0db95d2811bb65c08b236f966eaf9fd8f/LICENSE)。
- main README、规划、基准与服务文档见对应段落；本轮未验签、启动服务、下载权重、做数值 / 性能实验或完整观看演示。
