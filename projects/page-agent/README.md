# Page Agent 项目速览与上手指南

> 更新日期：2026-03-12（Asia/Shanghai）
> 项目地址：https://github.com/alibaba/page-agent

## 这是什么
`alibaba/page-agent` 是一个“运行在网页内”的 GUI Agent：直接在当前页面注入脚本后，用自然语言控制页面中的按钮、表单、导航等交互。它不是传统浏览器自动化（如外部驱动+截图识别）路线，而是偏“前端内嵌 Copilot”路线。

## 为什么今天值得关注
- GitHub Trending Today 快照显示：`page-agent` 位于当日热门列表，约 `4,668 stars`、`1,206 forks`、`368 stars today`。
- GitHub 仓库页（2026-03-12 抓取）显示约 `4.6k stars`、`364 forks`，最近版本 `v1.5.6` 发布于 `2026-03-11`。
- 这类 in-page agent 形态对 SaaS 产品团队很实用：能快速给已有系统加“自然语言操作层”，无需先重写后端架构。

## 快速上手

## 1) 一行脚本接入（Demo）
适合先验证交互效果：

```html
<script src="https://cdn.jsdelivr.net/npm/page-agent@1.5.6/dist/iife/page-agent.demo.js" crossorigin="true"></script>
```

说明：官方标注该 demo LLM 仅适合技术评估，存在速率/配额限制。

## 2) NPM 安装（推荐正式接入）

```bash
npm install page-agent
```

```ts
import { PageAgent } from 'page-agent'

const agent = new PageAgent({
  model: 'qwen3.5-plus',
  baseURL: 'https://dashscope.aliyuncs.com/compatible-mode/v1',
  apiKey: 'YOUR_API_KEY',
  language: 'zh-CN',
})

await agent.execute('点击登录按钮，然后填写账号和密码')
```

## 原理（工程视角）

## 1) DOM 优先，而非截图优先
核心能力是从页面 DOM 结构抽取可操作语义，再由 LLM 规划动作序列。
- 优点：无需多模态截图推理，延迟和成本更可控。
- 限制：对复杂 Canvas、自定义渲染控件的可解释性弱于视觉方案。

## 2) Agent 循环 + 工具执行
执行链路通常是：
1. 读取当前页面状态（元素、可见性、层级关系）；
2. LLM 将自然语言意图拆成动作计划；
3. 执行动作（点击、输入、滚动、导航）；
4. 校验结果并继续下一步，必要时进入 human-in-the-loop。

## 3) BYO LLM（自带模型）
项目支持接入自有模型/网关（示例里是兼容 OpenAI 风格的接口参数），便于企业在“模型可替换、审计可追踪”的前提下部署。

## 4) 可扩展到多页任务
官方提供可选浏览器扩展能力，支持跨 tab/多页面任务，从“单页助手”扩展为“轻量工作流代理”。

## 适用场景
- SaaS 内置 AI Copilot（如 CRM/ERP 操作辅助）
- 长流程表单自动化填写
- 面向无障碍场景的自然语言控制
- 低代码后台的“操作语义层”快速加装

## 风险与边界
- 权限风险：若直接给高权限页面启用自动执行，可能扩大误操作半径。
- 稳定性风险：动态 DOM 频繁变更会导致元素定位波动。
- 合规风险：若接入第三方模型，需核对敏感字段与日志策略。

建议：先在低风险页面灰度，开启关键动作二次确认，逐步扩白名单。

## 对你仓库可复用的实践建议
1. 先写一份“页面操作意图模板”（例如登录、检索、导出）。
2. 给每个意图补充失败回退动作（找不到元素时如何处理）。
3. 把模型参数与 API Key 放到环境层，不写死在前端代码。

## 参考来源
- GitHub 仓库：https://github.com/alibaba/page-agent
- 官方文档：https://alibaba.github.io/page-agent/
- GitHub Trending Today：https://github-trending.today/
