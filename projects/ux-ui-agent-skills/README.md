<!-- markdownlint-disable MD013 MD034 -->

# UX/UI Agent Skills：带可执行验证门槛的设计知识层

> 上游仓库：https://github.com/plugin87/ux-ui-agent-skills · 归类：前端、UI 与 Agent 交互层 · 本页基于 2026-09-15 的 README、package manifest、eval 记录、release、LICENSE 与 GitHub REST API 静态整理；未安装或运行其浏览器 gates。

## 定位

`ux-ui-agent-skills` 为 Claude Code 提供设计 token、组件规范、无障碍规则、设计系统映射、19 个 skills、5 个 commands 和一个 design critic。它将“给 agent 一些审美提示”扩展为 DTCG token、组件状态、WCAG 2.2、RTL、reduced motion、render gate 与冷启动 eval 组成的设计工程知识层。

2026-09-15 的 GitHub 官方 JavaScript Trending 抓取显示约 `+63 stars today`；REST API 快照为 `1,306 stars / 134 forks / 14 open issues`，MIT，最新 release 与根 `package.json` 均为 `v2.10.0`（2026-09-14）。仓库 description 仍写 38 gates，而 README 已写 41，说明宣传 metadata 与实现数字存在更新时差。

## 用法

可以作为 Claude Code plugin 安装，也可以用 npx 只复制需要的领域：

```text
/plugin marketplace add plugin87/ux-ui-agent-skills
/plugin install ux-ui-agent-skills@ux-ui-agent-skills
```

```sh
# 先看 demo，不安装全套规则
npx ux-ui-agent-skills demo

# 写入当前项目
npx ux-ui-agent-skills init
npx ux-ui-agent-skills add tokens taste design-systems
```

常用入口包括 `/design-component`、`/data-dashboard`、`/brandkit`、`/gate`、`/critique` 和 `/ship`。`--dry` 可预览 npx 写入；安装前应确认哪些文件会进入当前仓库以及是否覆盖既有 `CLAUDE.md` / rules。

## 原理

- 用 Primitive → Semantic → Component 三层 DTCG token 统一颜色、排版、间距、阴影、边框、断点和 motion。
- 用 Atomic Design 描述组件 anatomy、variant、state、token mapping 与 accessibility contract，并通过 adapter protocol 映射不同前端/原生框架。
- README 当前列出 41 个 objective gates；其中 31 个打开真实浏览器检查示例 HTML 的主题、交互、焦点、RTL、响应式、target size、reduced motion、overflow 等，其余读取 token 与源文件。
- `/critique` 负责主观设计判断：渲染不同 viewport / theme、点击控制并给出可回溯 findings，而不是把 gate 分数当审美分。
- 冷启动 eval 把简报和 scaffold 交给不带历史上下文的 agent，再用 14 个客观 gate 检查输出；原始输出保留在 `evals/out/`。

## 价值

- 将 token、一致性、无障碍和交互状态从 prompt 建议变成可失败的检查项，更适合进入 CI/验收链路。
- 文档主动区分“可测正确性”和“主观质量”，并保留冷启动输出与结果 provenance。
- plugin 与 npx 两条路径支持全量使用或按领域 vendoring，便于控制上下文与仓库改动范围。
- 框架适配和 design-system crosswalk 能作为团队统一设计语言的起点。

## 风险边界

- 41/41 主要覆盖仓库示例的 rendered HTML 与部分文件规则；README 明确承认生成的 `.tsx`、`.vue`、`.swift` 尚未全部通过相同 render gate。
- gate 通过不是可用性、品牌、审美或业务正确性证明。仓库自己的 blind output 即使 14/14，也曾被 `/critique` 判为 `rework`。
- “任意框架”“138 design systems”“50 components”等是知识覆盖清单，不证明每个组合都被真实实现、测试或持续维护。
- npx/init 与 plugin 会向项目写入规则、skills、commands、templates 和 token；`--force` 可能覆盖现有文件，需先 dry-run 和版本控制。
- 验证脚本涉及 Node、Python 与 Playwright；包描述中的“无 runtime 依赖”不能理解为完整验证流程没有工具链依赖。
- 本页没有运行 demo、41 个 gates、axe、冷启动 eval 或跨框架渲染，因此不能复述为本机验证结果。

## 补充建议

1. 固定 `v2.10.0`，先用 `demo` 和 `--dry` 观察写入面，再只引入 tokens、accessibility 或一个目标框架。
2. 把自己的真实组件编译并渲染到同一 gate，而不是只让仓库示例通过；同时保留视觉回归、屏幕阅读器和人工可用性测试。
3. 对所有“自动修复”保存前后截图、DOM、token diff 和交互记录，避免为满足规则而损伤信息层级或品牌意图。
4. 升级时核对 README gate 数、package version、eval corpus 与 changelog，防止指标口径随版本漂移。

## 参考资料

- 上游 README：https://github.com/plugin87/ux-ui-agent-skills
- 在线 demo：https://plugin87.github.io/ux-ui-agent-skills/
- 使用指南：https://github.com/plugin87/ux-ui-agent-skills/blob/main/docs/GUIDE.md
- Eval 记录：https://github.com/plugin87/ux-ui-agent-skills/blob/main/evals/RESULTS.md
- 根 package manifest：https://github.com/plugin87/ux-ui-agent-skills/blob/main/package.json
- `v2.10.0` release：https://github.com/plugin87/ux-ui-agent-skills/releases/tag/v2.10.0
- GitHub REST API：https://api.github.com/repos/plugin87/ux-ui-agent-skills
- LICENSE：https://github.com/plugin87/ux-ui-agent-skills/blob/main/LICENSE
