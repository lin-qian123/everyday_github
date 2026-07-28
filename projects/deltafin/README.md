# deltafin

## 定位

`deltafin` 是一个 Apple Silicon 本地推理实验：用按需读取/缓存 MoE experts、MXFP4 内核与 Metal/MPS 计算，尝试在 64 GB M1 Max 上运行 Kimi K3，并提供 OpenAI-compatible 服务端。

截至 2026-07-29，GitHub API 显示其创建于 2026-07-28，约 73 stars、5 forks；仓库 API 未声明 SPDX 许可证，使用前不能自行假定为可自由再分发。

## 用法

它要求 Apple Silicon、Xcode Command Line Tools、Python 3.12+ 和 Hugging Face 网络访问。项目提供 `--full` 与 `--stream` 两种权重获取模式，官方 README 明示前者约需 1.7 TB 磁盘、后者约需 215 GB；先用 `--dry-run` 核查实际资源与下载许可。

```bash
./venv/bin/python tools/setup_k3.py --stream
./venv/bin/python tools/serve_openai.py --port 8000
```

启动后才可让本地客户端指向 `http://127.0.0.1:8000/v1`。不要把它直接接到无超时、并发或 token 上限的自动化 agent。

## 原理

MoE 每个 token 只会选中部分专家。Deltafin 把常驻 spine 放在本地盘/内存，并对路由到的 experts 从本地 cache 或远端分片读取；其 fused MXFP4 GEMV 与双缓冲加载试图降低逐 token 的数据移动成本。服务层实现了部分 OpenAI 风格 completions、chat completions、models 与流式接口。

## 价值

- 是“大于单机内存的 MoE 如何以磁盘/网络换延迟”的透明实验样本。
- OpenAI-compatible 入口便于把本机模型接到现有聊天 UI 或低频测试客户端。

## 风险边界

- 项目自己报告 M1 Max 约 16 秒/token，流式缺失缓存时可能以小时计；这不是可交互生产推理方案。
- 需要极大磁盘、长期网络访问与上游权重许可，下载成本、缓存增长和内容合规须先评估。
- API 的兼容范围与模型输出质量尚未做独立验证；README 也指出自动化 agent 的长提示会显著增加预填充开销。

## 补充建议

先以极短的确定性 prompt 和单用户回归测量端到端延迟、cache 命中和磁盘增量；仅在 loopback 监听，设置客户端长超时、串行队列、最大生成长度与资源告警。

## 参考资料

- GitHub：<https://github.com/gavamedia/deltafin>
- GitHub API 快照：<https://api.github.com/repos/gavamedia/deltafin>
