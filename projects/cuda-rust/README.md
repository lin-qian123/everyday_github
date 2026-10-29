<!-- markdownlint-disable MD013 -->

# cuda-rust

## 定位

CUDA Rust 是 NVIDIA 的早期 Rust GPU 研究平台，提供 host runtime、cuda-oxide 的 SIMT 编程，以及 cutile-rs 的 Tile 编程。它不是通用 CPU / GPU 跨厂商后端；研究性 API、工具链和设备支持仍会变化。

2026-10-30 快照：Rust daily +32 stars；API 累计 3,889 stars / 349 forks / 234 open issues（含 PR）。核读 main `023f2ac3b842`；发行 API 首项 [cutile-rs/v0.4.0](https://github.com/NVIDIA/cuda-rust/releases/tag/cutile-rs/v0.4.0)，2026-10-12 UTC。以下为文档与有限源码核读，未安装运行。

## 用法

先确定 kernel 适合哪种模型。SIMT 路径阅读固定 installation，核对 NVIDIA GPU（文档列 Ampere / sm_80+）、驱动、CUDA、Clang / LLVM 和由 cargo oxide 管理的 Rust 工具链，再运行官方最小例子。Tile 路径从固定 Hello World 与兼容表入手。

```bash
# 在配置好的 cuda-oxide 环境中检查解析到的组件
cargo oxide doctor
```

不同子组件使用不同依赖；不要把 SIMT 的 CUDA 13.0+ 入门要求直接套在所有 Tile IR 功能上。项目未在本机安装或编译，也未执行 NVIDIA kernel。

## 原理

SIMT 允许显式控制 thread / block、共享内存和同步，Rust 代码提前编译为 PTX；Tile 以张量分块操作表达计算，首次 launch 经 Tile IR 编译为 cubin。共享 runtime 管理 context、stream、buffer 和异步操作，launch 借用约束尝试把 Rust ownership 延续到 GPU 工作完成。

## 价值

为 Rust 系统提供直接 GPU kernel 和 host 编排的研究入口。规则张量计算可尝试 Tile，稀疏结构或精细控制可评估 SIMT；两者可在同一 stream 上共享设备 buffer。选型仍应由目标工作负载和实际测量决定。

## 风险边界

- 根 Apache-2.0，第三方通知另列。作者明确 early-stage research，存在 bug、缺失能力与 API breakage。
- 数据竞争约束有适用范围，SIMT 仍需正确同步与共享内存管理；Rust 类型约束不自动证明数值正确、无所有 GPU 竞争或无 unsafe 风险。
- Toolkit、driver、PTX / cubin 与 Tile IR 是不同兼容轴。兼容表显示 Tile baseline IR 13.2、部分操作需 13.3 / 13.4，目标架构还有额外限制。
- 新 toolkit 生成的 PTX 可能超出旧驱动 JIT 能力；驱动较新也不能让旧 tileiras 理解新 IR。
- 首次 JIT、后续缓存和 warm kernel 计时要分开。GPU 不同、精度不同或省略传输的倍数不能直接比较。
- cutile-rs/v0.4.0 是组件发行；不能当作整个单仓库所有 crate 的统一版本。

## 补充建议

先用向量加法与小矩阵做 CPU 参考、边界尺寸和 Compute Sanitizer 检查；固定 GPU、驱动、toolkit、编译器与 commit。分别报告编译 / JIT、host-device 传输、warm kernel、误差与显存，并保留不支持设备的 SKIP 和真实失败。

## 参考资料

- [上游仓库](https://github.com/NVIDIA/cuda-rust)、[仓库 API](https://api.github.com/repos/NVIDIA/cuda-rust)。
- [README.md](https://github.com/NVIDIA/cuda-rust/blob/023f2ac3b842ff9b7e8aca501998899bcd81efca/README.md)。
- [cuda-oxide/cuda-oxide-book/getting-started/installation.md](https://github.com/NVIDIA/cuda-rust/blob/023f2ac3b842ff9b7e8aca501998899bcd81efca/cuda-oxide/cuda-oxide-book/getting-started/installation.md)。
- [LICENSE](https://github.com/NVIDIA/cuda-rust/blob/023f2ac3b842ff9b7e8aca501998899bcd81efca/LICENSE)。
- [cutile-rs/cutile-book/reference/compatibility.md](https://github.com/NVIDIA/cuda-rust/blob/023f2ac3b842ff9b7e8aca501998899bcd81efca/cutile-rs/cutile-book/reference/compatibility.md)。
- [cutile-rs/cutile-book/tutorials/01-hello-world.md](https://github.com/NVIDIA/cuda-rust/blob/023f2ac3b842ff9b7e8aca501998899bcd81efca/cutile-rs/cutile-book/tutorials/01-hello-world.md)。
