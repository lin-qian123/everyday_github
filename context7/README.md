# context7（upstash/context7）

- GitHub: https://github.com/upstash/context7
- 记录日期: 2026-04-24 (Asia/Shanghai)

## 这是什么

`context7` 是一个面向 AI 编码助手的“实时文档注入层”。核心目标是把库/框架的最新官方文档和版本化示例，在提问时直接注入到模型上下文，减少“用旧 API 写新代码”与幻觉接口问题。

## 热度信号

1. GitHub 页面显示约 `53.6k stars`、`2.5k forks`，属于近期高关注的 AI 开发基础设施项目。
2. OSSInsight AI Trending（2026-04-24 快照）将其列在 Top Movers 与 Top 50 的前列，说明不是一次性爆红，而是仍在持续扩散。

## 怎么用（最短路径）

### 1) 一键安装

```bash
npx ctx7 setup
```

该命令会完成认证与基础配置，可按提示选择 CLI+Skills 或 MCP 方式。

### 2) 在提示词里显式触发

```text
Create Next.js middleware for JWT cookies. use context7
```

如果知道库 ID，可指定：

```text
Implement auth with Supabase. use library /supabase/supabase
```

### 3) MCP 手工接入（按需）

- Server URL: `https://mcp.context7.com/mcp`
- 通过 `CONTEXT7_API_KEY` 传递凭据。

## 核心原理

1. 运行时检索：在推理前拉取目标库当前文档，而不是只依赖模型训练记忆。
2. 版本对齐：按库名/版本匹配上下文，避免旧参数或废弃接口。
3. 低摩擦触发：通过规则（Rules/Skills）自动在“文档类问题”调用，减少人工切换。

## 适用场景

1. 框架快速迭代（Next.js、Supabase、Cloudflare 等）导致 API 变化频繁的项目。
2. 团队中多个代理/IDE 并行协作，需要统一“文档事实来源”。
3. 对代码正确性要求高，且不希望人工频繁查文档切页的工作流。

## 价值与风险

价值：
- 显著降低过期 API 与幻觉调用。
- 把文档检索嵌入编码闭环，提升首版代码可运行率。

风险：
- 检索质量受库匹配与提示词清晰度影响。
- 若盲目信任自动注入，仍可能出现“上下文噪声过多”或误匹配。

## 我认为有价值的补充材料

1. 在团队规范中增加“文档敏感任务默认启用 Context7”规则。
2. 对关键库固定 `library id + version`，减少跨版本漂移。
3. 在 CI 里增加最小烟测，验证模型输出确实与目标版本兼容。

## 参考来源

- https://github.com/upstash/context7
- https://ossinsight.io/trending/ai
- https://context7.com/
