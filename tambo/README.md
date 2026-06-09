# Tambo

Tambo 是一个面向 React 的 **Generative UI（生成式界面）** SDK：你注册已有的 React 组件，AI 在对话中决定该渲染哪个组件、生成哪些 props，并把组件直接插入对话或页面中。它内置 agent、支持流式输出、工具调用与 MCP（Model Context Protocol）集成，适合做“会对话、会动手”的产品界面。

## 适用场景
- 把聊天从“纯文本”升级为“可交互的界面元素”（图表、表单、卡片、面板）。
- 在业务系统里让用户用自然语言驱动 UI（比如“给我上周销售图表”“把订单过滤为华东地区”）。
- 让 AI 通过工具调用/外部系统完成动作（查库、调用 API、生成报告）。

## 核心能力
- **Generative Components**：AI 按需创建并渲染新组件实例。
- **Interactable Components**：你预先放置组件，AI 通过对话更新其 props。
- **工具调用（Tools）**：把你的函数注册为工具，AI 可调用获取数据或执行操作。
- **MCP 原生**：通过 MCP 连接外部系统（数据库、API、第三方服务）。
- **流式与状态**：props 可流式更新，消息线程与状态管理开箱即用。

## 原理概述（简化版）
1. **注册组件/工具**：在 `TamboProvider` 中注册组件与工具，并用 Zod 定义 props/输入输出结构。
2. **意图解析与匹配**：用户发起自然语言请求后，Tambo 结合组件描述、对话上下文进行匹配。
3. **生成 props 并渲染**：若匹配到组件，AI 生成 props 并将组件渲染进对话；若需要数据，则先调用工具。
4. **持续对话更新**：对话中已有组件可被再次更新（Interactable），形成“可对话的 UI”。

## 快速开始
### 1) 创建项目
```bash
npm create tambo-app@latest my-tambo-app
```
该命令会拉起模板、安装依赖并引导生成 API Key，写入 `.env.local`。

### 2) 运行
```bash
npm run dev
```
打开 `http://localhost:3000` 开始体验。

### 3) 注册组件（示意）
```tsx
import { TamboProvider } from "@tambo-ai/react";
import { z } from "zod";

const components = [
  {
    name: "RecipeCard",
    description: "Render a recipe card",
    component: RecipeCard,
    propsSchema: z.object({
      title: z.string(),
      ingredients: z.array(z.object({ name: z.string(), amount: z.number() })),
    }),
  },
];

export default function App() {
  return (
    <TamboProvider components={components} tools={tools} apiKey={process.env.TAMBO_API_KEY}>
      <MyAiApp />
    </TamboProvider>
  );
}
```

## 组件模式：Generative vs. Interactable
- **Generative**：根据用户请求即时创建新组件实例，适合“单次展示型”内容（图表、摘要）。
- **Interactable**：组件预先放在页面中，AI 可以根据对话更新其 props，适合“长期存在的状态组件”（购物车、表单）。

## 工具调用与 MCP
- **本地工具**：你提供 JS/TS 函数，Tambo 根据需要调用，产出数据再渲染组件。
- **MCP 工具**：连接外部 MCP Server，实现“无需手写集成”的第三方能力接入。
- **MCP 连接方式**：支持服务端连接（推荐，性能好）与客户端连接（便于本地/私有环境）。

## 关键优势
- **开发门槛低**：会写 React 即可上手，复用现有组件。
- **UI 更“主动”**：用户只说需求，界面自动生成与更新。
- **体系化扩展**：通过 Tools + MCP 把 AI 变成“能做事”的产品助手。

## 资源
- GitHub: https://github.com/tambo-ai/tambo
- Docs: https://docs.tambo.co/
- Quickstart: https://docs.tambo.co/getting-started/quickstart
- Tools 概念: https://docs.tambo.co/concepts/tools
- MCP 概念: https://docs.tambo.co/concepts/model-context-protocol
