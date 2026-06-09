# Burn（tracel-ai/burn）

## 项目定位
Burn 是一个用 Rust 编写的深度学习框架，目标是同时兼顾“灵活、效率、可移植性”，覆盖训练与推理场景。它由 Tracel 团队维护，并强调跨设备/跨硬件的部署能力，以及更少的性能调优成本。

- 官方站点: https://burn.dev/
- GitHub: https://github.com/tracel-ai/burn
- 文档（Burn Book）: https://burn.dev/burn-book/getting-started.html

## 为什么近期值得关注
- 在 GitHub 趋势工具榜单中排名靠前（趋势信号来自第三方趋势榜）。
- Rust 生态中少见的“端到端深度学习框架”，话题聚焦于“性能 + 可移植 + 现代模型研发体验”。

## 核心原理（简述）
Burn 的核心架构基于“张量操作流（tensor operation streams）”，在运行期由 JIT 编译器进行自动优化与硬件自适应调参。它利用 Rust 的所有权规则跟踪张量生命周期与依赖关系，从而实现高动态模型的同时具备接近静态图的性能。

## 适用场景
- 需要在 Rust 生态内做训练与推理的团队
- 需要跨平台部署（云端、桌面、移动端）
- 想要减少手动性能调优/依赖地狱的模型工程

## 快速上手（最小可跑示例）

### 1) 安装 Rust
参考 Rust 官方安装指引（rustup）。

### 2) 新建项目并添加 Burn 依赖
```bash
cargo new my_burn_app && cd my_burn_app
cargo add burn --features wgpu
```

### 3) 写一个简单张量示例
```rust
use burn::tensor::Tensor;
use burn::backend::Wgpu;

type Backend = Wgpu;

fn main() {
    let device = Default::default();
    let tensor_1 = Tensor::<Backend, 2>::from_data([[2., 3.], [4., 5.]], &device);
    let tensor_2 = Tensor::<Backend, 2>::ones_like(&tensor_1);
    println!("{}", tensor_1 + tensor_2);
}
```

### 4) 运行
```bash
cargo run
```

## 使用要点
- Burn 通过 backend 抽象支持多种执行后端（如 `wgpu`），因此要先明确目标硬件与后端选择。
- Rust 的类型系统会让模型代码更“显式”，但也能换来更高的可靠性与可维护性。

## 进一步阅读
- Burn Book（上手与深度使用）: https://burn.dev/burn-book/getting-started.html
- Burn 框架架构介绍: https://burn.dev/
- Tracel 项目介绍: https://tracel.ai/
