<!-- markdownlint-disable MD013 -->

# Doop：人与 Agent 共享的 HTML 设计画布

- 上游：[kgoedecke/doop](https://github.com/kgoedecke/doop)；分类：前端、UI 与 Agent 交互层。
- 更新：2026-11-03（Asia/Shanghai）；固定主线 SHA：`a3749d99817c32498ec36b7130db24023a2af901`。
- 热度快照：TypeScript daily +162；API 1,556 stars / 185 forks / 71 open issues（含 PR）。最新发行首项 desktop-v0.11.0，UTC 2026-11-01；这是桌面组件标签。
- 证据：官方 Trending / API 与固定源码静态核读；下文用法供复核，不表示本轮已运行。

## 定位

Doop 把画布、HTML frame、多人光标、评论、设计记忆和 MCP 放在同一工作台。浏览器用户与 Claude Code、Codex 等 MCP 客户端编辑相同设计；内置 Doop Agent 是另一条需要模型账户的执行路径。项目自称 Paper.design 的开源替代品，本页未验证功能等价。

## 用法

上游开发入口需要 Bun 和 Node；安装前固定提交并检查依赖：

```sh
git clone https://github.com/kgoedecke/doop
cd doop
bun install
bun run dev
```

Web 默认为 localhost:4300，API / WebSocket / MCP 为 localhost:4400，开发模式用 data/pg 内嵌 PGlite。先注册测试账户，在顶栏 Connect AI 选择客户端并完成 OAuth；CI 等无浏览器场景可创建 agent key。内置 Agent 使用用户连接的模型账户；服务端免费任务配额 RESIDENT_TASK_LIMIT 默认 0。首次欢迎演出是脚本，不能据此判断模型效果。

## 原理

- React 画布通过 WebSocket 房间同步状态；REST 与 MCP 写入复用 actions，再落到 Postgres / PGlite。
- Frame HTML 在带 allow-scripts 的 sandbox iframe 渲染，没有 allow-same-origin；DOM 原位更新承接流式设计。
- MCP OAuth 和 agent key 解析到用户身份，继承该用户的画布权限。源码中 key 只创建时返回明文，服务端存 SHA-256；它是账户级凭据。
- 设计批准关联 frame revision；HTML 或尺寸变更后回到 needs_review。批准可以触发自动化，但没有启用 workflow 时只改变设计状态。

## 价值

适合把视觉迭代、评论与后续开发连接起来，保留人和 Agent 的编辑上下文。直接操作 HTML 也便于把设计同实际 Web 组件比较；是否能保持字体、响应式行为和可维护代码，需要真实导出验收。

## 风险边界

- 自托管代码为 AGPL-3.0；名称与 logo 另有商标约束。Figma、Canva、PSD 的部分导入导出仅在 Cloud 提供，不能从截图推断开源版具有同样能力。
- iframe 限制页面脚本访问宿主，不能替代账户权限、模型数据出口或第三方资源访问治理。连接模型、图片服务、Slack / Linear 后要分别审查内容与凭据。
- .env.example 标明 PostHog 分析和 session replay 默认关闭，但构建时设置 VITE_POSTHOG_KEY 会开启，运行时删变量不能改变已有 bundle。
- 未配置 SMTP 时注册保持开放，认证邮件链接进入服务端日志；生产应设置认证 origin / secret、邮箱验证及注册域限制，限制日志访问。
- 账户级 agent key、自动化发布和外部系统写入权限需分别收窄。本轮只核静态实现，未启动服务、接 MCP 或验证租户隔离。

## 补充建议

1. 用两名测试用户和一个受限 Agent 验证 view / comment / edit、撤销 key 与并发修改。
2. 先选一张真实页面，比较导入、编辑、导出后的 DOM、字体、尺寸和交互。
3. 固定模型、预算与画布 revision，批准前检查事实、素材许可和导出可用性。

## 参考资料

- [README.md](https://github.com/kgoedecke/doop/blob/a3749d99817c32498ec36b7130db24023a2af901/README.md)。
- [.env.example](https://github.com/kgoedecke/doop/blob/a3749d99817c32498ec36b7130db24023a2af901/.env.example)。
- [server/agentKeys.ts](https://github.com/kgoedecke/doop/blob/a3749d99817c32498ec36b7130db24023a2af901/server/agentKeys.ts)。
- [server/auth.ts](https://github.com/kgoedecke/doop/blob/a3749d99817c32498ec36b7130db24023a2af901/server/auth.ts)。
- [LICENSE](https://github.com/kgoedecke/doop/blob/a3749d99817c32498ec36b7130db24023a2af901/LICENSE)。
- [仓库 API](https://api.github.com/repos/kgoedecke/doop)；[发行记录](https://github.com/kgoedecke/doop/releases/tag/desktop-v0.11.0)。
