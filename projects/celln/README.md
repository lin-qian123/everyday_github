# celln

## 定位

Celln 是实验性的 agent 执行隔离工具：它让 agent 在临时“cell”中借用被验证的只读工具，而不是拥有一台完整机器，并对 agent 编写的程序施加更低权限执行通道。截至 2026-08-03 的 GitHub API 快照：项目创建于 2026-08-02，约 9 stars、1 fork，Apache-2.0。

## 用法

可通过 Homebrew 安装，或从源码构建 `celln-cli` 后执行 `celln doctor`。核心流程是 `celln spec init > agent.toml`、`celln spec check agent.toml`、`celln run agent.toml`；完整 sealing 需要 Linux `/dev/kvm`，生成程序还需要 Rust 静态目标及 `gcc`、`cpio`、`e2fsprogs`。非 Linux 环境仍可做规范校验和 demo。

## 原理

规范声明可借用的工具、内存与执行入口；Celln 将宿主提供且已验真的工具放入 tool lane，把 agent 编写的脚本/编译物降入 agent lane。项目以 microVM、只读封装、Landlock、seccomp、哈希和重复构建等机制限制写入、网络与权限，并支持针对网络任务显式声明允许主机。

## 价值

- 将“工具可信”和“agent 生成代码可信”分开建模，减少解释器或编译流程意外继承宿主权限。
- 以可检查 spec 记录能力需求，便于在运行前审查 agent 的执行面。

## 风险边界

- README 所述隔离和证明范围受内核、硬件虚拟化、配置与实现版本限制；不能取代企业隔离、密钥管理或安全审计。
- agent 写代码发生在宿主侧，且启用网络时风险模型会显著扩大；域名 allowlist 不是对远端内容的信任保证。
- 这是新项目的早期信号，缺乏长期跨平台与生产负载验证。

## 补充建议

先在无密钥、无生产数据的 Linux 测试机执行 `doctor`、示例 spec 和 `verify`；将网络、挂载、工具路径和输出目录逐项最小化，并让独立安全人员复核逃逸面。

## 参考资料

- GitHub：<https://github.com/sympozium-ai/celln>
- 文档：<https://sympozium-ai.github.io/celln/>
- GitHub API 快照：<https://api.github.com/repos/sympozium-ai/celln>
