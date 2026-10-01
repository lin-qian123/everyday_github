<!-- markdownlint-disable MD013 -->

# Cordis（cordiverse/cordis）

> 上游仓库：<https://github.com/cordiverse/cordis> · 归类：Agent 框架与技能生态 · 本页基于 2026-10-02 的 GitHub API、README、package manifests、测试树、论文仓库与发行信息静态整理，未运行 plugin lifecycle、HMR 或论文实验。

- 抓取快照：8,942 stars、559 forks、76 open issues。
- 热度信号：GitHub TypeScript Trending 抓取时约 +15 当日 stars。
- 版本与许可：MIT；latest Release / tag 和核心 `cordis` package 均为 `v4.0.0-rc.10`，根 workspace manifest 仍是私有 `0.0.0`。

## 定位

Cordis 是面向动态插件系统和 Agent harness 的 TypeScript 元框架，试图同时解决组件的“时间可组合性”与“空间可组合性”：插件移除时能撤销已登记副作用，依赖环境变化时能自动激活或停用组件。仓库提供 core、loader、include、HMR、group、timer 与 logging 等包。

## 用法

消费端核心包名为 `cordis`，loader 与 include 作为可选 peer packages；贡献者使用 Yarn 4 workspace 构建、测试。上游根 README 明确 API 尚不稳定，官方文档仍在建设，目前需要结合核心类型、测试、论文和 DeepSeek Harness 的 primer 理解 `Context`、service、event、fiber、plugin 与 dispose 语义。

## 原理

论文把每个组件产生的可撤销 context transformation 记为 revertible effect，把组件依赖声明及其随 context 变化的激活 / 停用记为 reactive coeffect；两者通过同一 context 中介。实现层以 fiber 追踪组件生命周期和 effect cleanup，以 service / registry 解析依赖，再由声明式 loader 做配置 reconcile 与 HMR。

## 价值

它把常见的“插件注册后留下监听器、定时器或服务引用”问题提升为运行时生命周期约束，也让依赖到位 / 消失与插件启停形成统一模型。对可热更新的 Agent harness、开发工具和长期运行服务，这比散落的初始化 / teardown 约定更容易测试和审计。

## 风险边界

- `v4.0.0-rc.10` 仍是 release candidate，README 明示 API 可无预告变化；根 manifest 与核心包版本也采用不同语义。
- “可撤销”只覆盖经 Cordis context 正确登记的副作用；任意 shell、网络、外部数据库写入、子进程或未注册全局状态不会自动回滚。
- HMR 和配置 reconcile 会重新加载应用代码，不等于事务、进程隔离或安全 sandbox；恶意 / 有缺陷插件仍继承宿主权限。
- 论文是正在修订的 arXiv preprint，本轮未核验形式化证明、运行时开销或与其他 DI / effect systems 的完整比较。
- 根 README 很短，官方文档尚未完成；当前 primer 托管在另一个 Harness 项目站点，文档与核心 package 可能发生版本漂移。
- 76 个 open issues 与 RC 阶段说明迁移、边界条件和生态兼容仍需按具体应用验证。

## 补充建议

固定 `v4.0.0-rc.10` 与完整 lockfile，在小型插件图中测试 service 到位 / 消失、异常初始化、重复 dispose、HMR、配置回滚和资源泄漏；对 socket、文件、子进程与数据库事务显式登记 cleanup 并增加故障注入。升级先读核心类型与 tests 的变更，不把 context lifecycle 当作 OS 权限或外部系统回滚保证。

## 参考资料

- [GitHub 仓库](https://github.com/cordiverse/cordis)
- [GitHub REST API](https://api.github.com/repos/cordiverse/cordis)
- [README](https://github.com/cordiverse/cordis/blob/main/README.md)
- [核心 package manifest](https://github.com/cordiverse/cordis/blob/main/packages/core/package.json)
- [核心测试目录](https://github.com/cordiverse/cordis/tree/main/packages/core/tests)
- [论文仓库与摘要](https://github.com/cordiverse/paper)
- [arXiv:2608.25512](https://arxiv.org/abs/2608.25512)
- [v4.0.0-rc.10 Release](https://github.com/cordiverse/cordis/releases/tag/v4.0.0-rc.10)
- [LICENSE](https://github.com/cordiverse/cordis/blob/main/LICENSE)
