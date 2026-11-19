<!-- markdownlint-disable MD013 -->

# splash

## 定位

Splash 是为 Apple silicon 设计的本地 LLM 推理引擎，通过 Metal 内核、DFlash 2 推测解码、前缀缓存和并发调度，向编码 Agent 及 OpenAI / Anthropic 兼容应用提供服务。模型推理和 Agent 执行工具的权限属于不同层。

- 上游：[incoai/splash](https://github.com/incoai/splash)，仓库 ID `1376380844`。
- 2026-11-20 07 时段：官方 C++ daily **+61**；API stars / forks / open issues（含 PR）为 **2,476 / 243 / 167**。[API](https://api.github.com/repos/incoai/splash)
- 最新核到的非预发行版：[1.7.0](https://github.com/incoai/splash/releases/tag/1.7.0)，UTC 11-17；main 固定快照 `61f6d51643a2cf8b3ed868dcb4bcda176ae578ec`。本页没有运行设备测试。
- 分类：`模型、训练与推理基础设施`。首次建档；官网首发博客日期为 09-17，不是今天发布。

## 用法

当前 README 要求 **Apple M3 或更新芯片、macOS 26.4+**；命令行使用 Homebrew，示例如下，本轮未执行：

```bash
brew install incoai/tap/splash
splash serve --model unsloth/Qwen3.8-27B-GGUF:UD-Q4_K_M
```

首次运行会准备依赖并下载目标模型及匹配的 draft，随后监听 `127.0.0.1:8000`；等待 `Ready` 后使用网页、API 或已安装的编码 Agent。`splash codex` 等命令接入已有 Agent，并不等于提供其订阅、全部协议能力或主机执行隔离。使用本地模型文件和兼容 draft 的方式见固定文档，不要将首次启动描述为完全离线。[README](https://github.com/incoai/splash/blob/61f6d51643a2cf8b3ed868dcb4bcda176ae578ec/README.md)、[服务配置](https://github.com/incoai/splash/blob/61f6d51643a2cf8b3ed868dcb4bcda176ae578ec/docs/server.md)

## 原理

1. **提议与验证**：小 draft 生成候选，目标模型一次验证候选树；1.7.0 同时使用 prompt lookup，把历史文本能提出的续写放入验证链。
2. **按成本选工作量**：启动校准后按设备、模型和运行时成本选择每轮验证行数，减少调度与重复计算；并非固定每轮接受同样多 token。
3. **缓存与内存调度**：复用前缀、保存 recurrent state，并按内存压力安排并发和 SSD cache / KV spill；减少重复 prefill，但会改变内存、磁盘与延迟分布。
4. **协议层**：提供 Chat Completions、Responses、Completions 与 Messages 接口及工具调用表示；兼容性仍需按具体客户端、模型模板和版本验证。

来源：[1.7.0 固定发行笔记](https://github.com/incoai/splash/blob/61f6d51643a2cf8b3ed868dcb4bcda176ae578ec/docs/release-notes/1.7.0.md)、[README](https://github.com/incoai/splash/blob/61f6d51643a2cf8b3ed868dcb4bcda176ae578ec/README.md)。

## 价值

- 为单台 Mac 上的本地模型、多个 Agent 请求与长会话提供统一服务和状态观察入口。
- 将解码、prefill、缓存和队列等待放在同一服务内优化，适合评估真实多轮调用而不只测裸 token 速率。
- 1.7.0 作者测试中，64GB M5 Pro、Qwen3.8-27B 的 62 个录制 pi / Codex 请求回放，解码中位提速 **1.46×**，请求耗时对应速度 **1.23×**，相对的是 **1.6.2 开发版本**。这是限定配置的作者回放结果，不是本轮复现或任意 Agent 任务成功率提升。

## 风险边界

- **提速并不均匀。** 固定发行笔记披露三个测量格的 decode 回退，最低约 0.973×；四会话回放中，首 token 耗时总和由 218 秒升至 259 秒，尽管请求中位速度改善。不能只引用 1.46×，也不能把比值换成任务质量结论。[详细基准](https://github.com/incoai/splash/blob/61f6d51643a2cf8b3ed868dcb4bcda176ae578ec/docs/release-notes/1.7.0.md)
- **默认数值与调度影响复现。** 缓存 recurrent state 默认 int8，恢复后的近似数值可能影响接近并列的候选；`--verify-rows auto` 也会令 greedy / seeded 输出随运行条件变化。文档给出 `--cached-states exact` 与 `--verify-rows all` 等控制项，重复条件还包括单请求和相同缓存前缀，不能只保存 seed。[配置说明](https://github.com/incoai/splash/blob/61f6d51643a2cf8b3ed868dcb4bcda176ae578ec/docs/server.md)
- **监听地址、Host 和认证是三回事。** 默认 loopback、认证关闭；扩大监听应配置 `SPLASH_API_KEY` 或 `--api-key`。`--allowed-host` 控制 HTTP Host，不是客户端 IP 白名单；`--allowed-origin '*'` 放宽浏览器来源，需要同时配置密钥。本轮未做网络攻击或鉴权测试。[安全文档](https://github.com/incoai/splash/blob/61f6d51643a2cf8b3ed868dcb4bcda176ae578ec/SECURITY.md)
- **本地推理仍有下载和留存。** 模型 / draft、持久缓存和可选 crash trace 分别管理；`SPLASH_CRASH_TRACE=1` 的记录可能包含会话内容。1.7.0 会令旧 1.6.x 持久缓存冷启动；SSD 写入与首启校准成本应计入验收。[服务文档](https://github.com/incoai/splash/blob/61f6d51643a2cf8b3ed868dcb4bcda176ae578ec/docs/server.md)、[发行说明](https://github.com/incoai/splash/releases/tag/1.7.0)
- **引擎许可不覆盖所有模型。** 根代码为 Apache-2.0，目标权重和 draft 的许可、格式与兼容关系须另外核验。[LICENSE](https://github.com/incoai/splash/blob/61f6d51643a2cf8b3ed868dcb4bcda176ae578ec/LICENSE)

## 补充建议

在自己的 Mac 上固定目标 / draft 权重版本、量化、上下文、缓存状态、系统负载和并发数，交替运行对照，分别记录 TTFT、decode tok/s、请求全程耗时、SSD 写入和任务正确率。保留慢样本与失败分母，再决定是否接入实际 Agent；本轮只读资料，没有下载模型、运行回放或验证主机权限隔离。

## 参考资料

- [官网首发说明，2026-09-17](https://inco.ai/blog/splash/)
- [发行列表](https://github.com/incoai/splash/releases)；本文以固定 1.7.0 笔记解释当前版本，不将 README 的 1.0 首发对比表当作最新基准。
