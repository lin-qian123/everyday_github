# chatbot-template

## 定位

shadcn-ui 的最小聊天应用模板，以 Next.js、Vercel AI SDK、shadcn/ui 和 Vercel AI Gateway 组合流式聊天、工具调用、网页搜索与人工问卷；它是应用起点，不是可直接公网部署的完整产品。

## 用法

```bash
git clone https://github.com/shadcn-ui/chatbot-template.git
cd chatbot-template && pnpm install
cp .env.example .env.local # 填入 AI_GATEWAY_API_KEY
pnpm dev
```

在 Vercel 可用 OIDC 连接 Gateway；本地可先 `vercel link && vercel env pull`。模型清单在 `lib/models.ts`，新增工具还需注册对应服务端定义和 UI message part。

## 原理

`/api/chat` 使用 `streamText`，客户端以 `useChat` 渲染；GitHub 查询、provider 原生网页搜索和人工问卷被组织为类型化 message parts，并按流式输入、执行、输出和错误状态显示。

## 价值

提供可读的 agent chat UI 骨架，以及工具状态、来源与人工澄清的完整交互路径；工具定义到界面的类型关联也有助于在构建期发现字段漂移。

## 风险边界

上游明确 `/api/chat` 默认公开且未认证，直接上线可能耗尽 AI Gateway credits。外部工具/网页内容也会带来权限、隐私和提示注入风险；OIDC 便利不等于成本、输出或合规已被保证。

## 补充建议

先加入认证、每用户/IP 限流、支出上限和监控；将模型与工具限制在代码清单，对工具输出做结构校验和最小权限设计。

## 参考资料

- [GitHub 仓库](https://github.com/shadcn-ui/chatbot-template)
- [README：部署、安全与工具机制](https://github.com/shadcn-ui/chatbot-template/blob/main/README.md)
- [GitHub API 元数据](https://api.github.com/repos/shadcn-ui/chatbot-template)
