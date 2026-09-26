<!-- markdownlint-disable MD013 -->

# Monty（pydantic/monty）

> 上游仓库：<https://github.com/pydantic/monty> · 归类：Agent 框架与技能生态 · 本页基于 2026-09-27 的 GitHub API、README、Security Model、Resource Limits、Limitations、Release 与 LICENSE 静态整理，未执行模型生成代码或复现延迟数字。

- 抓取快照：8,344 stars、423 forks、123 open issues。
- 热度信号：GitHub Rust Trending 抓取时约 +48 当日 stars。
- 版本与许可：MIT；latest Release、tag 与 Cargo workspace version 均为 `v1.0.0` / `1.0.0`。

## 定位

Monty 是用 Rust 编写、专门运行 AI 生成 Python 的语言级 sandbox。开源版本提供 Python、JavaScript / TypeScript 与 Rust 接口，默认不具备文件、环境变量、网络、子进程、FFI 或第三方 package 能力；商业 Full Monty 在其上增加服务与 OS 级隔离。

## 用法

可分别安装 `pydantic-monty`、`@pydantic/monty` 或 Rust crate，创建 pool、checkout session，再用 `feed_run` 执行代码。宿主可显式注入输入、host functions、host objects、mount 与 resource limits；最小安全路径应从零 capability 开始，只加入参数验证过的窄接口，并为 untrusted source 设置 memory、feed duration、turn duration、suspension 和 request timeout。

## 原理

隔离来自解释器本身不实现 ambient host operations，而不是 seccomp、容器或 VM。外部访问只能经 host function / object、mount 与 OS callback 三类显式能力；VM 遇到宿主操作会 suspend，由 host 决定。Rust worker 还提供 memory、执行时间、递归、suspension、sleep 和 protocol size 等限制，并支持 snapshot / restore。

## 价值

对 Agent code mode 而言，Monty 用较小的启动与调用开销提供比 `eval` 更窄的默认能力面，并把宿主接口变成可审计的显式 contract。Python 子集、类型检查、资源上限和跨语言 bindings 适合计算、转换和受控工具编排，但上游延迟数字仍需在具体机器与 workload 独立复现。

## 风险边界

- 上游明确称其为 language-level sandbox，不是 OS-level isolation；开源 Monty 没有 container、seccomp 或 VM。
- host function、class method、mount 与 callback 以宿主进程完整权限运行；一个可读取任意 path 或 fetch 任意 URL 的接口就会重新引入文件 / 网络风险。
- 多个资源限制是可选的，memory 不是 RSS 上限；host callback 时间不计入 VM 执行预算，仍需宿主 deadline、cgroup 或进程级限制。
- memory / time limit 触发后 heap 状态不再有保证，上游要求丢弃 session；pool 不会自动代办这一生命周期处理。
- 它只实现 Python 3.14 子集，无第三方 package，缺少 inheritance、generator、threading、socket、subprocess 等能力；兼容性必须以 Limitations 为准。

## 补充建议

把 Monty worker 再放进低权限进程 / container，默认不给 mount、network 或通用 host function。为每个暴露函数做 schema、size、path、URL 与 tenant 校验；设置所有资源限制和宿主 watchdog，并在 limit / crash 后强制销毁 checkout。用 malicious corpus 测 escape、resource exhaustion、callback abuse、snapshot 与 CPython divergence。

## 参考资料

- [GitHub 仓库](https://github.com/pydantic/monty)
- [GitHub REST API](https://api.github.com/repos/pydantic/monty)
- [v1.0.0 Release](https://github.com/pydantic/monty/releases/tag/v1.0.0)
- [Security Model](https://github.com/pydantic/monty/blob/main/docs/security.md)
- [Resource Limits](https://github.com/pydantic/monty/blob/main/docs/resource-limits.md)
- [Limitations](https://github.com/pydantic/monty/blob/main/docs/limitations/index.md)
- [LICENSE](https://github.com/pydantic/monty/blob/main/LICENSE)
