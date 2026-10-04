<!-- markdownlint-disable MD013 -->

# e2e（tester-army/e2e）

> 上游仓库：<https://github.com/tester-army/e2e> · 归类：Agent 框架与技能生态 · 本页基于 2026-10-05 的 GitHub API、README、agent / security / telemetry 文档、Release、manifest 与 LICENSE 静态整理，未安装 npm 包、连接模型、运行浏览器 / 模拟器或复测测试稳定性。

- 抓取快照：3,032 stars、114 forks、42 open issues。
- 热度信号：GitHub 综合 / TypeScript Trending 抓取时约 +344 当日 stars。
- 版本与许可：Apache-2.0；主包 Release / manifest 为 `e2e@0.17.0` / `0.17.0`，web 与 mobile 包分别为 `0.12.0`、`0.9.2`；README 明确仍在走向 1.0。

## 定位

e2e 是面向 Web 与移动应用的 agentic 端到端测试框架。测试用自然语言描述目标，由 Agent 驱动界面；最终结果仍可用 locator 与 assertion 做确定性断言。它同时覆盖 Playwright 浏览器、iOS / Android 模拟器、GitHub PR reporter，以及可选的托管浏览器和移动设备执行器。

## 用法

运行 `npx e2e init`，选择 web / mobile engine 与模型 provider，工具会生成配置和示例测试。测试可以只用传统 locator，也可以调用 `agent.act()` 和 `agent.assert()`；Agent 成功动作会写入 replay cache，界面未变化时后续运行可不再调用模型。模型可用自带订阅、API key 或本地端点。

## 原理

runner 把测试代码、engine、模型 gateway 和报告层拆开：模型读取被标记为不可信的文本、accessibility tree 或像素观察，输出受 closed schema 约束的工具调用；runner 在 dispatch 前做授权，并由确定性断言给最终 verdict。成功动作可被录制为重放步骤，但 cache 一旦提交到仓库就属于 code-trust，会以测试代码的权限执行。

## 价值

它把“自然语言探索复杂 UI”与“可回归的断言 / 重放”放进同一个测试文件，适合难以只靠固定 selector 编写的流程。离线文档、provider 可替换、传统无模型测试和逐步缓存，让团队可以把模型成本限制在仍需语义判断的步骤。

## 风险边界

- SECURITY 明确测试文件、配置、自定义工具、engine、command / service 和 replay cache 都拥有当前 OS 权限，框架本身不是 sandbox；不可信 PR 必须在外部隔离环境运行。
- Web Agent 可访问任意 HTTP(S) URL，没有 origin allowlist；跳转、弹窗和第三方登录会扩大观察与动作范围，测试账户、支付和生产后台必须隔离。
- secret 机制会阻止值进入模型并重写 trace，但命令 / service stdout 不自动脱敏；应用本身、provider、浏览器下载和可选托管执行器仍有各自数据流。
- CLI telemetry 默认开启，虽然文档列出不发送测试内容、URL、路径和凭据，仍会发送命令、engine、provider / model id、计数、错误类别和随机机器 / hash 项目标识；可显式关闭。
- replay 降低模型调用不等于结果永远可靠：UI、权限、cache 内容或外部服务变化仍可能让重放产生错误副作用。
- 本轮未复测作者的 benchmark、页面 prompt injection 防护、secret trace 清理、移动设备一致性或托管 Kernel / EAS 边界。

## 补充建议

先固定 `e2e@0.17.0` 和 engine 版本，在无真实账号的测试环境中从只读流程开始；所有购买、删除、发信与权限变更另设后置断言和服务端 fixture。把 replay cache 当代码审查，CI 对 fork PR 禁用 secrets / write token，默认关闭 telemetry，并分别记录模型调用与确定性断言失败率。

## 参考资料

- [GitHub 仓库](https://github.com/tester-army/e2e)
- [GitHub REST API](https://api.github.com/repos/tester-army/e2e)
- [README 与 Quick start](https://github.com/tester-army/e2e/blob/main/README.md)
- [Agent steps](https://github.com/tester-army/e2e/blob/main/docs/agent-steps.mdx)
- [Security trust model](https://github.com/tester-army/e2e/blob/main/SECURITY.md)
- [Telemetry 字段](https://github.com/tester-army/e2e/blob/main/docs/telemetry.mdx)
- [e2e@0.17.0 Release](https://github.com/tester-army/e2e/releases/tag/e2e%400.17.0)
- [主包 manifest](https://github.com/tester-army/e2e/blob/main/packages/e2e/package.json)
- [LICENSE](https://github.com/tester-army/e2e/blob/main/LICENSE)
