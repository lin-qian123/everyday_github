<!-- markdownlint-disable MD013 MD034 -->

# json-render：用受约束 JSON 生成跨平台界面的 Generative UI 框架

> 上游仓库：https://github.com/vercel-labs/json-render · 归类：前端、UI 与 Agent 交互层 · 本页基于 2026-09-20 的 README、package manifest、release、LICENSE 与 REST API 静态整理；未接入模型或运行示例应用。

## 定位

Vercel Labs 的 `json-render` 让模型只在开发者定义的 component catalog 和 action 名单内生成 JSON spec，再由 React、Vue、Svelte、Solid、React Native、Next.js、Remotion、PDF、Email、Ink 或 3D renderer 转成界面。它试图把“模型直接写任意 UI 代码”变成“模型填写受约束结构”，但不是完整的应用安全边界。

2026-09-20 的 GitHub 官方 TypeScript Trending 抓取显示约 `+468 stars today`；REST API 快照为 `16,843 stars / 901 forks / 103 open issues`，Apache-2.0，最新 release 为 `v0.21.0`（9 月 18 日）。

## 用法

React 最小安装如下：

```sh
npm install @json-render/core @json-render/react
```

开发者先用 Zod 定义 component props 与可用 action，再把实现注册到 renderer：

```ts
const catalog = defineCatalog(schema, {
  components: { Card: { props: z.object({ title: z.string() }) } },
  actions: { refresh_data: { description: "Refresh metrics" } },
});
```

模型只输出 spec，前端用 `<Renderer spec={spec} registry={registry} />` 渲染。仓库主干要求 Node `>=24` 与 pnpm `>=11`；实际应用应按 release 的包版本安装。

## 原理

- catalog 将允许的 component、props schema、event 与 action 名称转换为模型提示和运行时校验合同。
- model 输出扁平 elements map 与 root，stream utilities 可在 spec 生成过程中增量渲染。
- registry 把已验证的 type 映射到真实组件；模型不直接提供任意 React / Vue 代码。
- state store、dynamic props、directives 与 action handler 负责数据绑定和交互副作用。
- 同一 catalog 可复用到 Web、移动、视频、PDF、Email、TUI、3D 和 MCP Apps；各 renderer 的能力与安全模型并不完全相同。

## 价值

- 把可生成 UI 的自由度限制在团队已有设计系统内，提升一致性、可回放和审查性。
- JSON spec 可记录、diff、测试和流式传输，比一次性代码生成更容易建立回归集。
- 多 renderer 共享 catalog，有利于把同一业务结构投影到不同交付媒介。
- 预制 shadcn 组件、AI SDK transform、MCP、devtools 和状态适配器降低试验门槛。

## 风险边界

- component allowlist 只限制“能渲染什么”；action handler 仍可能付款、写数据库、发邮件或调用工具，必须独立做授权、确认和幂等。
- schema 合法不代表语义正确、无欺骗或符合业务规则；模型仍可选择错误数据、误导布局或高风险 action 参数。
- 动态 HTML、链接、图片、Email、PDF、3D asset 和 MCP 输入需要各自的转义、来源 allowlist 与内容安全策略。
- 流式 UI 会出现中间态；表单提交、action 可用性和焦点管理不能依赖尚未完成的结构。
- 跨框架“同一 catalog”不保证可访问性、视觉一致、SSR、移动手势或打印结果等价。
- 本页未验证 `v0.21.0` 的 schema 覆盖、stream recovery、XSS、防提示注入、action 授权或无障碍。

## 补充建议

1. 将查询类与写入类 action 分开，所有外部副作用在服务端重新鉴权、校验参数并保留人工确认。
2. 对生成 spec 建 golden fixtures、schema fuzz、未知 component、超深树和流中断测试。
3. 只让模型看到必要 catalog 与脱敏数据，renderer 不加载模型给出的任意代码、URL 或组件包。
4. 每个目标 renderer 单独做可访问性、错误态、打印 / 导出和视觉回归，不能只验 React demo。

## 参考资料

- 上游 README：https://github.com/vercel-labs/json-render
- `v0.21.0` release：https://github.com/vercel-labs/json-render/releases/tag/v0.21.0
- Core package source：https://github.com/vercel-labs/json-render/tree/main/packages/core
- GitHub REST API：https://api.github.com/repos/vercel-labs/json-render
- LICENSE：https://github.com/vercel-labs/json-render/blob/main/LICENSE
