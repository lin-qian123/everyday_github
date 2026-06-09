# browserbase-skills（记录日期：2026-05-02）

- GitHub：<https://github.com/browserbase/skills>
- 趋势信号：GitHub Trending 当日出现（`browserbase/skills`）

## 1. 项目定位
`browserbase/skills` 是一组给 AI coding agent 用的浏览器自动化技能包。
它将 Browserbase 云浏览器能力、`bb` CLI 与 agent 技能系统打通，让代理可以稳定执行网页浏览、抓取、调试与 UI 测试任务。

## 2. 基础用法
1. 安装技能包：
   - `npx skills add browserbase/skills`
2. 在支持插件市场的代理里安装对应插件（README 给出 `/plugin` 流程）。
3. 通过自然语言或 CLI 指令触发操作，例如：
   - 让 agent 访问页面并提取结构化信息
   - 用 `bb` 列出项目与会话
   - 对本地站点做 UI 测试与回归检查
4. 需要复用本地登录态时，可按文档使用本地浏览环境连接参数。

## 3. 原理理解
- 技能封装层：把常见浏览器动作抽象成标准技能（browser/fetch/search/ui-test 等）。
- 运行时层：通过 Browserbase 会话提供更稳定的自动化执行环境，减少本地浏览器差异。
- 调试层：提供 trace/诊断技能，用于定位选择器失效、反爬、登录态等问题。
- CLI 协同层：`bb` CLI 负责会话、项目、函数等平台资源管理。

一句话：它让“AI 代理操作网页”从 ad-hoc 脚本变成可复用、可观测的工程能力。

## 4. 适用场景
- 智能体驱动的数据抓取和页面核查。
- 本地 Web 应用自动化冒烟测试。
- 需要代理执行跨站流程的运营/增长自动化。

## 5. 风险与注意点
- 自动化浏览涉及账号与会话，需严格隔离凭据与环境。
- 反爬策略变化会导致流程脆弱，必须保留人工兜底。
- 涉及真实交易/提交动作时应设置二次确认。

## 6. 补充材料
- 官方 README（技能列表与安装方法）：<https://github.com/browserbase/skills>
- Browserbase 文档：<https://www.browserbase.com/docs>
