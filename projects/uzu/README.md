<!-- markdownlint-disable MD013 -->

# uzu

> 更新：2026-10-22（Asia/Shanghai）。分类：模型、训练与推理基础设施。主上游 `trymirai/uzu`；默认分支快照 `c812cf9bae50`。官方资料与源码静态研究；热度、发行及社媒口径见[当日日报](../../daily/2026-10-22/ai-hotspots.md)。

## 定位

Mirai 的推理引擎，提供 Rust、Python、TypeScript 和 Swift 接口，利用 Apple 统一内存与 Metal 做端侧运行，也提供云模型和 HTTP server 示例。README 的“零延迟、完全隐私、无推理成本”是宣传口径，不能覆盖所有模式或实际设备开销。[README.md](https://github.com/trymirai/uzu/blob/c812cf9bae500f261b38de6e36beedf236ae9d6d/README.md) [Package.swift](https://github.com/trymirai/uzu/blob/c812cf9bae500f261b38de6e36beedf236ae9d6d/Package.swift)

## 用法

README 的 Python 入口固定 `uzu==0.6.11`，TypeScript 为 `@trymirai/uzu@0.6.11`；流程是创建 Engine、查模型、下载、建立 chat session 再 reply。Rust 示例依赖 main，不能与固定发行包默认视为相同接口。[README.md](https://github.com/trymirai/uzu/blob/c812cf9bae500f261b38de6e36beedf236ae9d6d/README.md)

当前 Swift manifest 的系统下限是 iOS / macOS / Mac Catalyst `26.4`，并下载带 checksum 的 `0.6.11` 二进制包。Swift tools 5.9 标签不表示可以在所有旧系统运行，选型须看实际 manifest。[Package.swift](https://github.com/trymirai/uzu/blob/c812cf9bae500f261b38de6e36beedf236ae9d6d/Package.swift)

## 原理

统一的 Engine / Model / Session 把下载、模型配置和回复封装为多语言接口，支持流式、结构化输出和工具调用。模型会占用统一内存，官方建议控制同时加载的 session 数量；HTTP server 默认监听 loopback，也可手动改到其他地址。[README.md](https://github.com/trymirai/uzu/blob/c812cf9bae500f261b38de6e36beedf236ae9d6d/README.md)

## 价值

工程判断：适合在 Apple 应用中验证小模型端侧体验，以及跨语言共享调用方式。收益应以首 token 延迟、生成速度、峰值内存、能耗与准确性共同衡量，不能把省掉网络等待理解为推理没有耗时。

## 风险边界

- 示例显式下载权重；首次运行并非离线。README 另有 cloud chat 和 API key 配置，选云模型会改变数据路径与账单；本地计算也有硬件、电力和内存成本。[README.md](https://github.com/trymirai/uzu/blob/c812cf9bae500f261b38de6e36beedf236ae9d6d/README.md)
- 工具调用由宿主注册并执行；推理引擎不自动限制工具副作用。HTTP server 改为 `0.0.0.0` 前还需设计认证和网络控制，不能照示例直接推断已有保护。[README.md](https://github.com/trymirai/uzu/blob/c812cf9bae500f261b38de6e36beedf236ae9d6d/README.md)
- 平台下限、预编译制品、量化格式与模型支持应按固定版本核验；MIT 代码许可不覆盖所有模型权重。[Package.swift](https://github.com/trymirai/uzu/blob/c812cf9bae500f261b38de6e36beedf236ae9d6d/Package.swift) [LICENSE](https://github.com/trymirai/uzu/blob/c812cf9bae500f261b38de6e36beedf236ae9d6d/LICENSE)
- 本页未复现性能、离线性或算子正确性，也未审计完整网络路径；可追踪计算的设计目标不等于所有模型数值已独立验证。[README.md](https://github.com/trymirai/uzu/blob/c812cf9bae500f261b38de6e36beedf236ae9d6d/README.md)

## 补充建议

先用公开小模型和短固定 prompt，对照参考实现检查输出、工具参数及内存；完成权重预取后断网验真实本地路径，再测冷 / 热启动。固定系统、芯片、包、权重哈希和采样参数。本轮未安装 uzu 或下载权重。

## 参考资料

- [README.md](https://github.com/trymirai/uzu/blob/c812cf9bae500f261b38de6e36beedf236ae9d6d/README.md)
- [LICENSE](https://github.com/trymirai/uzu/blob/c812cf9bae500f261b38de6e36beedf236ae9d6d/LICENSE)
- [Cargo.toml](https://github.com/trymirai/uzu/blob/c812cf9bae500f261b38de6e36beedf236ae9d6d/Cargo.toml)
- [Package.swift](https://github.com/trymirai/uzu/blob/c812cf9bae500f261b38de6e36beedf236ae9d6d/Package.swift)
- [docs/index.mdx](https://github.com/trymirai/uzu/blob/c812cf9bae500f261b38de6e36beedf236ae9d6d/docs/index.mdx)
- [仓库 API](https://api.github.com/repos/trymirai/uzu)
- [0.6.11 Release](https://github.com/trymirai/uzu/releases/tag/0.6.11)
