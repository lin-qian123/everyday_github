<!-- markdownlint-disable MD013 -->

# Modern Web Guidance：把现代 Web 平台知识送入 Coding Agent

- 上游：[`GoogleChrome/modern-web-guidance-src`](https://github.com/GoogleChrome/modern-web-guidance-src)；仓库 ID：`1143633223`。
- 核读：2026-11-12（Asia/Shanghai）；主线固定于 [`9636f4b1a43b`](https://github.com/GoogleChrome/modern-web-guidance-src/tree/9636f4b1a43b71e0cc9fdf34cf60f477c01d0087)。
- 热度快照：1,704 stars / 138 forks / 366 open issues（含 PR）；来自 [GitHub API](https://api.github.com/repos/GoogleChrome/modern-web-guidance-src)，不代表采用量或质量。

## 定位

Chrome、Edge、Firefox 和 MDN 团队及社区共同维护的 Web 开发指导体系，帮助 Coding Agent 使用浏览器原生 API、兼容策略和可验证的 UI 模式。本页跟踪**源仓库**：编写、校准、构建和评测逻辑在这里；面向宿主安装的分发仓库是 `GoogleChrome/modern-web-guidance`，两者不要混淆。

今天官方综合 / TypeScript daily +133。[npm `modern-web-guidance`](https://registry.npmjs.org/modern-web-guidance/latest) 当前为 1.0.0；源仓库唯一可见发行 `audit-data` 是 10-14 的预发行审计快照，不是 CLI 稳定版号。[官方文档](https://developer.chrome.com/docs/modern-web-guidance)提供安装与演示回链。代码 Apache-2.0；`guides/` 指南内容按 README 为 CC-BY 4.0，不能只沿用 API 的单一 SPDX。

## 用法

以下按上游命令改为固定当前 npm 版本，并明确关闭默认遥测；本轮未安装或执行：

```bash
DISABLE_TELEMETRY=1 npx modern-web-guidance@1.0.0 search "light dismiss dialog"
DISABLE_TELEMETRY=1 npx modern-web-guidance@1.0.0 retrieve "animate-to-from-top-layer"
DISABLE_TELEMETRY=1 npx modern-web-guidance@1.0.0 install
```

先用单一、简短的英文能力描述搜索，再按返回 ID 取指南，不要把示例 ID 当成任何任务的答案。上游 `install` 会调用 skills 安装器，从分发仓库写入宿主技能；固定 CLI 版本并不自动固定分发内容。接入前检查将写入的目录和版本。

npm 元数据要求 Node >=22.0.0；源仓库开发 `package.json` 要求 >=22.18.0、pnpm 10.30.3，不能把贡献环境与已发布 CLI 的最低版本混写。广泛旧代码迁移可用 `legacy-scan`；普通单功能实现先 search / retrieve 即可。

## 原理

以本地语义检索和 BM25 找到相关 guide，再将模式、易错点和 fallback 送入模型上下文。源仓库的指南、示例、expectations 和 Playwright grader 构成校准流程，比较有 / 无指导时在同类任务上的通过率。

兼容策略默认按 Baseline Widely available；不是该状态的特性仍需按指南处理回退。Origin Trial 与 volatile 特性需显式 opt-in，可通过项目级 `.mwgrc` 配置；搜索可见不等于直接可采用。`legacy-scan` 文档标明只覆盖约 20% 的指南库中有确定规则的部分。

## 价值

把 Web 平台更新、浏览器兼容与可执行检查放到写代码前，适合改进 dialog、popover、布局、性能和无障碍实现。可把“模型说能用”转化为具体 guide、目标浏览器和可复核行为。

README 的 11-08 作者评测示例为 215 项 Codex 任务、1,795 条 assertions，通过率 54% → 82%（+28 个百分点）；这是指定模型、任务和 grader 的作者结果，未在本轮复跑，也不是线上缺陷率或所有浏览器的保证。

## 风险边界

- **本地检索与全程无网络不同**：README 声明搜索引擎本地，但 CLI 默认启用遥测。核读 logger 中 `DISABLE_TELEMETRY=1/true` 关闭，普通环境默认开启，payload 含搜索 query、guide IDs、agent、版本和耗时等；原始用户 prompt 不在作者声明的收集项里，但生成的 query 仍可能带敏感语义。
- `npx` 初次取包、更新与技能安装需要网络。关闭遥测不替代断网实验，也不证明包或 Agent 其他组件无出口。
- “原生 API 更简洁”不保证满足目标浏览器、嵌入式 WebView、输入设备或无障碍要求；需要实际测试 fallback、键盘与屏幕阅读器。
- grader 通过只覆盖定义的断言。不要据此认定完整安全审计、业务正确性或真实 Core Web Vitals 提升。
- 指南引用与二次分发应保留 CC-BY 所需署名；代码和内容许可分别处理。

## 补充建议

在项目约定目标浏览器和允许的 fallback，再选一个有 / 无指导的同任务对照；保存 CLI、分发技能与 guide 版本、模型配置、输出 diff 和人工评审。敏感项目先关闭遥测并检查实际出口；不要仅凭 README 中“offline/private”措辞下结论。

本轮只核文件、注册表、官方文档与公开发布元数据，未执行 CLI、安装、浏览器评测或网络抓包。

## 参考资料

- [源仓库说明与评测、隐私、许可](https://github.com/GoogleChrome/modern-web-guidance-src/blob/9636f4b1a43b71e0cc9fdf34cf60f477c01d0087/README.md)。
- [技能检索与兼容规则](https://github.com/GoogleChrome/modern-web-guidance-src/blob/9636f4b1a43b71e0cc9fdf34cf60f477c01d0087/guides/modern-web-guidance/SKILL.md)。
- [源仓库开发环境](https://github.com/GoogleChrome/modern-web-guidance-src/blob/9636f4b1a43b71e0cc9fdf34cf60f477c01d0087/package.json)。
- [CLI 与安装调用](https://github.com/GoogleChrome/modern-web-guidance-src/blob/9636f4b1a43b71e0cc9fdf34cf60f477c01d0087/src/cli/modern-web.ts)。
- [默认遥测及 payload](https://github.com/GoogleChrome/modern-web-guidance-src/blob/9636f4b1a43b71e0cc9fdf34cf60f477c01d0087/src/cli/telemetry/clearcut-logger.ts)。
- [Apache-2.0 代码许可](https://github.com/GoogleChrome/modern-web-guidance-src/blob/9636f4b1a43b71e0cc9fdf34cf60f477c01d0087/LICENSE)。
