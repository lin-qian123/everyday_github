<!-- markdownlint-disable MD013 -->

# Sandcastle：用 TypeScript 编排 coding agents 与 sandbox

- 上游：[mattpocock/sandcastle](https://github.com/mattpocock/sandcastle)；分类：Agent 框架与技能生态。
- 更新：2026-11-04（Asia/Shanghai）；固定 main SHA：`8c2c5689a836a626232ff09b4c62cfdf72ad7684`。
- 热度：TypeScript daily +28；API 8,815 stars / 943 forks / 143 open issues（含 PR）。最新 v0.14.0，UTC 2026-11-02；主线 package 同为 0.14.0。
- 证据范围：官方榜单、API、发行与固定文档 / 源码；未安装、运行 Agent、创建 sandbox 或调用云服务。

## 定位

以 `run()`、sandbox provider、Agent provider 和 Git 分支策略组合自动编码流程的 TypeScript 库。原生 Bubblewrap / Seatbelt、容器和云执行环境承担不同隔离边界；框架负责启动、会话、提交同步和分支处理。它适合审查流水线、并行任务和多步自动化，实际权限取决于所选 provider。

## 用法

上游 quick start 的初始化路径如下，先在可丢弃测试仓库操作：

```sh
npm install --save-dev @ai-hero/sandcastle@0.14.0
npx @ai-hero/sandcastle@0.14.0 init
```

init 生成 .sandcastle 配置并检查 provider：macOS 14+ 可选 Seatbelt，Linux / WSL2 需 Bubblewrap；原生环境使用宿主工具链。按生成的 .env.example 填写专用模型凭据后再执行生成入口。这里的命令仅说明用法，本轮没有初始化或消费模型额度。

`branchStrategy: { type: "branch", branch: "agent/test" }` 可让提交保留在明确分支。先检查生成脚本的 provider、分支策略、模型、预算和测试门槛；不要从名称推断默认会创建独立分支。

## 原理

- Agent provider 封装 Claude Code、Codex 等工具；sandbox provider 定义进程、文件、环境变量和同步方式。
- bind-mount provider 默认 head，直接写宿主工作目录；isolated provider 默认 merge-to-head，复制仓库后同步提交并合回；branch 策略保留指定分支。
- 原生 provider 隐藏普通 home、使用临时 home，仅传入指定变量，读取宿主工具链并开放仓库写入；不可用时抛错，不自动退回无隔离执行。
- 当前分支文档说明 Git 控制文件只读、宿主 Git 操作忽略仓库可执行配置；这些保护只覆盖框架控制的 Git 路径。

## 价值

把模型调用、执行环境与提交归属拆成显式参数，便于更换本地 / 云后端并追踪任务产物。与只创建 worktree 相比，它还组织执行边界；是否能长期无人值守仍需任务级验收、错误恢复和成本控制。

## 风险边界

- 原生 sandbox **网络开放，包括宿主 localhost**；Seatbelt 文档不保证隔离 macOS Keychain，进程组逃逸也有清理限制。文件约束不能替代网络与凭据策略。
- 文档明确 Agent 在框架内跳过自身权限检查，隔离依赖外层 provider；`noSandbox()` 完全在宿主执行，`wt.interactive()` 未给 provider 时默认走此路径。
- mount 可扩大读取 / 写入范围；.sandcastle/.env 中声明的变量会进入 sandbox，云 provider 的控制面 key 不应误当作 Agent 所需变量下发。
- head 会直接改当前目录，merge-to-head 会自动合回；一次 run 结束并不代表 diff、测试或业务结果已经验收。后续用户自行执行的 Git 命令也超出框架保护范围。
- v0.13 改变 native 默认与部分 Git / sync 行为；v0.14 新增 E2B、Modal、Sprites，SDK、Node 要求、网络与收费规则各异。根许可 MIT，依赖和云服务分别核对。

## 补充建议

1. 对每个 provider 独立检查可见文件、环境变量、网络和 localhost；先用无敏感数据的测试仓库。
2. 初次采用明确 branch 策略，验收 diff / 测试后再合并；记录失败、冲突和清理后的残留状态。
3. 分开保存模型 key 与云控制面 key，设置预算、超时和允许访问的服务；升级时重测分支默认值。

## 参考资料

- [README](https://github.com/mattpocock/sandcastle/blob/8c2c5689a836a626232ff09b4c62cfdf72ad7684/README.md)、[Getting started](https://github.com/mattpocock/sandcastle/blob/8c2c5689a836a626232ff09b4c62cfdf72ad7684/docs/guide/getting-started.md)。
- [Sandbox providers](https://github.com/mattpocock/sandcastle/blob/8c2c5689a836a626232ff09b4c62cfdf72ad7684/docs/guide/sandbox-providers.md)、[分支策略](https://github.com/mattpocock/sandcastle/blob/8c2c5689a836a626232ff09b4c62cfdf72ad7684/docs/guide/branch-strategies.md)、[Seatbelt 实现](https://github.com/mattpocock/sandcastle/blob/8c2c5689a836a626232ff09b4c62cfdf72ad7684/src/sandboxes/seatbelt.ts)。
- [package.json](https://github.com/mattpocock/sandcastle/blob/8c2c5689a836a626232ff09b4c62cfdf72ad7684/package.json)、[LICENSE](https://github.com/mattpocock/sandcastle/blob/8c2c5689a836a626232ff09b4c62cfdf72ad7684/LICENSE)、[API](https://api.github.com/repos/mattpocock/sandcastle)。
- [v0.14.0](https://github.com/mattpocock/sandcastle/releases/tag/v0.14.0)、[v0.13.0 行为变更](https://github.com/mattpocock/sandcastle/releases/tag/v0.13.0)。
