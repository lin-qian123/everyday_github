<!-- markdownlint-disable MD013 -->

# bend

## 定位

Bend 2 是把依赖类型、形式化定律和 CPU / GPU 并行编译结合的语言。面向 AI 编程时，思路是让人维护 `LAWS.bend` 中的性质，由 Agent 编写实现和证明，再由检查器验证性质是否成立。它是一门新语言及工具链，并不是给任意现有 Python / JavaScript 项目加一条提示就能消除错误。

- 上游：[bendlang/bend](https://github.com/bendlang/bend)，仓库 ID `684776900`。
- 2026-11-21（Asia/Shanghai）07 时段：官方 TypeScript daily **+95**；API stars / forks / open issues（含 PR）为 **25,694 / 820 / 161**。[API](https://api.github.com/repos/bendlang/bend)
- 最新核到非预发行版 [v2.0.40](https://github.com/bendlang/bend/releases/tag/v2.0.40)，UTC 11-06；本页 main 固定快照 `0e2f38f759cc830849e489307f3d256a7d148288`。首次建档不代表今天发布，main 功能不能自动归入发行包。
- 分类：`模型、训练与推理基础设施`，按 AI 生成代码的验证与执行工具链收录；本轮未安装编译器、运行证明或测试性能。

## 用法

上游主要支持 Linux / macOS 后端开发，Windows 走 WSL。安装入口见[固定 README](https://github.com/bendlang/bend/blob/0e2f38f759cc830849e489307f3d256a7d148288/README.md)；检查下载脚本与对应版本后再自行安装。本轮没有执行远程安装器。

已安装 Bend 后，可先读 guide，再从一个明确性质开始：

```text
bend guide
bend PROOF.bend
bend PROOF.bend --verdict
```

按[指南](https://github.com/bendlang/bend/blob/0e2f38f759cc830849e489307f3d256a7d148288/guide/GUIDE.md)的约定，`LAWS.bend` 导入实现并声明性质；`PROOF.bend` 导入 laws，给每条 law 写同名定义作为证明。人应保护 laws，避免 Agent 为通过检查而削弱目标。普通检查与 `--verdict` 的双重检查是不同路径，要保存实际输出和版本。

上游还提醒：发行的 `bend` 忽略项目 `bunfig.toml` 和 `.env`，从 checkout 直接跑 `bun bend2/main.ts` 会读取它们。此差异不是运行任意不可信程序的沙箱承诺。

## 原理

- **性质即类型。** 定律表达为命题类型，证明是该类型的定义；依赖类型使结果约束能包含输入值。模式匹配、结构递归与改写构造证明，并没有自动 tactics / proof search。
- **仿射资源与终止。** 值默认最多使用一次，可复制数据有额外标记；常规递归必须通过终止检查。`@unsafe` / 不受检查的递归与 foreign 路径会改变可证明范围，不能混入“所有代码都已证明”的结论。
- **并行调用。** 纯函数和仿射约束支持独立调用的二叉 fork-join；工作量均衡由程序组织保证。`!` 用于 GPU 路径，具体执行还受调用位置和设备条件影响；没有 GPU 时可回落 CPU，JavaScript target 为单核。
- **第二检查器。** `--verdict` 把翻译出的项交给有 Lean 证明的 BendTT kernel，再次检查。上游明确 parser 和翻译过程尚未被证明，默认 checker 也没有自身正确性证明；内核证明不等于整个编译器、运行时和所有后端已形式化验证。[指南](https://github.com/bendlang/bend/blob/0e2f38f759cc830849e489307f3d256a7d148288/guide/GUIDE.md)

## 价值

对离散状态机、容器性质、排序不变量等定义清楚的任务，Bend 提供把自然语言意图转换为可机械检查命题的实验路径。它有助于把“看起来能运行”与“针对指定语义证明了什么”分开；证明仍只能覆盖写入 laws 的性质。

上游展示与 C、GPU 和其他证明工具的速度比较，本轮只读文本与方法入口，未核动画中的完整数据、基准公平性或硬件条件，不复述为独立性能结论。v2.0.40 修复相等 share cell 导致的检查挂起，也说明工具链自身仍在修正。[发行说明](https://github.com/bendlang/bend/releases/tag/v2.0.40)

## 风险边界

- **规格可能写错。** 检查通过不证明 laws 完整表达人的需求；弱性质、错误前提或遗漏外部状态都可能放过业务错误。需要审阅 laws 及其与实现的连接。
- **语义与后端不同层。** [README 限制](https://github.com/bendlang/bend/blob/0e2f38f759cc830849e489307f3d256a7d148288/README.md)明确：性质针对 Bend 语义，后端仍可能有差异；编译器尚未全面审计。`--verdict` 的信任边界还包含未证明的解析和翻译。
- **浮点和硬件能力有限。** 当前文档仅列 Nat、U32、F32，没有 F64；F32 运算仍为公理，不能据此宣称浮点数值正确性已证明。[WONTFIX](https://github.com/bendlang/bend/blob/0e2f38f759cc830849e489307f3d256a7d148288/WONTFIX.txt)还记录 JS / C 的 NaN payload 差异、运行时容量上限以及部分理论允许但后端会 fail-stop 的值。
- **并行不是普适提速。** 当前需均衡调用，单程序单 GPU、无多机执行；某些 GPU 条件不满足会运行在 CPU。数值 HPC、PIC 或任意动态图不能只凭语言口号迁移。
- **生态与迁移。** Bend 1 程序和 HVM 不直接延续到 Bend 2；基础库较小，缺少许多通用语言设施，原生编译也有工具链要求。正式工程需核对依赖、FFI 和可维护性。
- **许可。** 根代码为 Apache-2.0；第三方库、安装制品和另接模型服务需另核。本文不是全仓安全或许可证适用性审计。[LICENSE](https://github.com/bendlang/bend/blob/0e2f38f759cc830849e489307f3d256a7d148288/LICENSE)

## 补充建议

先选一个不用浮点、外部 IO 或 unsafe 的小状态机，人工写 laws，分别制造正常实现、破坏性质的实现和弱化 laws 的实现，检查默认路径与 `--verdict` 是否符合预期。再对比解释 / C / JS / GPU 的输出与资源使用，保存输入、编译参数、版本和失败样本。

对科研代码，本页最值得借鉴的是“明确不变量、保护规格、保存证明边界”的工作方式。当前资料不足以建议用它替换现有双精度数值计算或多节点 HPC 工具链。

## 参考资料

- [固定 README：定位与限制](https://github.com/bendlang/bend/blob/0e2f38f759cc830849e489307f3d256a7d148288/README.md)。
- [固定 GUIDE：laws、kernel、并行与 unsafe](https://github.com/bendlang/bend/blob/0e2f38f759cc830849e489307f3d256a7d148288/guide/GUIDE.md)。
- [固定 WONTFIX：设计与后端限制](https://github.com/bendlang/bend/blob/0e2f38f759cc830849e489307f3d256a7d148288/WONTFIX.txt)、[Apache-2.0](https://github.com/bendlang/bend/blob/0e2f38f759cc830849e489307f3d256a7d148288/LICENSE)。
- [v2.0.40 发行说明](https://github.com/bendlang/bend/releases/tag/v2.0.40)。README 所链论文与 Lean 形式化为后续深读入口，本轮未阅读全文或重跑形式化证明。
