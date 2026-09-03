<!-- markdownlint-disable MD013 MD034 -->

# UI Skills：面向 Design Engineers 与 Coding Agents 的设计技能注册表

## 项目概览

- 上游仓库：https://github.com/ibelick/ui-skills
- GitHub API 快照（2026-09-04）：8,052 stars、363 forks、13 个开放 issue
- 当前 release：`v0.2.3`
- 主要技术：TypeScript CLI、远程 MCP、skills registry、UI design playbook
- 许可证：MIT

## 定位

UI Skills 把设计工程中的界面、动效和实现经验组织为可查询的 skills，并同时提供网页、CLI 和 MCP 入口。Design Engineer 可以浏览规则，coding agent 可以列出并读取某项 skill 后用于界面任务。

它是设计知识与指令分发层，不是 Figma 文件、组件库、自动视觉验收或无障碍测试器。

## 用法

CLI 可浏览分类、列出或拉取某项 skill：

```bash
npx ui-skills categories
npx ui-skills list --category motion
npx ui-skills get baseline-ui
```

需要 agent 动态查询时，可接入 `https://www.ui-skills.com/mcp`，使用 `list_skills` 和 `get_skill`。生产仓库宜先把选定 skill 固定到项目内并审查内容，而不是每次都依赖远程最新版本。

## 原理

项目维护一个技能注册表和 playbook；CLI 负责查询与获取，MCP server 把相同能力暴露为 agent tools。模型读取规则后仍通过自身推理生成或修改 UI 代码。

规则能改善提示上下文，但不会确定性执行视觉测量，也无法自动证明生成页面符合品牌、交互、性能、响应式或 WCAG 要求。

## 价值

- 让设计 judgment 以可版本化文本进入 coding-agent 上下文。
- CLI、Web 与 MCP 三种入口适合人工浏览、项目固化和动态发现。
- `list/get` 的小工具面比开放式远程执行更容易审计。
- 可作为设计评审 checklist 的起点，而不只是一组样式模板。

## 风险边界

- 远程 MCP 与注册表内容会变化，必须明确信任源、版本、网络和可用性边界。
- skill 中的审美与最佳实践是建议，不保证符合具体品牌、用户研究或业务指标。
- agent 生成的 UI 仍可能有无障碍、性能、响应式、浏览器兼容和设计 token 漂移。
- 从远程加载的自然语言内容属于不可信输入，需防提示注入和越权工具调用。
- 高星与 Trending 日增星不是设计质量、转化率或可维护性证据。
- 本页只核验 README、站点入口、release 与 API，未连接 MCP 或运行视觉回归。

## 补充建议

1. 把采用的 skill 内容和上游 commit 固定进项目，升级时做文本 diff。
2. 将规则转成可执行 gate：axe、Lighthouse、截图 diff、键盘导航和多 viewport 检查。
3. 用现有设计系统、token 和真实组件约束 agent，不让通用 playbook 覆盖品牌规范。
4. 给远程 MCP 配置只读工具范围、超时和审计日志，不允许其直接触发部署或外部写操作。
5. 用设计师和用户测试评价结果，不用“已使用 skill”替代产品验证。

## 参考资料

- 仓库与 README：https://github.com/ibelick/ui-skills
- Releases：https://github.com/ibelick/ui-skills/releases
- 官方站点：https://www.ui-skills.com/
- Playbook：https://www.ui-skills.com/playbook
- MCP 入口：https://www.ui-skills.com/mcp
