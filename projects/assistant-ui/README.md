<!-- markdownlint-disable MD013 -->

# assistant-ui（assistant-ui/assistant-ui）

- GitHub：<https://github.com/assistant-ui/assistant-ui>
- 核查：2026-11-16（Asia/Shanghai）07 时段；13,236 stars / 1,342 forks / 81 open issues（含 PR）；仓库 ID `722184017`。
- 热度：官方 TypeScript daily +92；旧项目首次建档。
- 固定 main：`6029493d7b20f29f5f10f877de1d6e14c5b595c7`；React 包与 npm latest 均为 `0.15.36`，CLI 源清单 `0.0.135`；最近 Release `setup-agent@0.2.0`（UTC 11-13）只属于安装辅助包，不是整库版本。
- 许可与证据：MIT；可选 Assistant Cloud 为托管服务。静态核读文档、清单与 guide 相关源码，未安装、联云或运行 Agent。

## 定位

assistant-ui 是构建 AI 对话界面的 TypeScript / React 库，以可组合的线程、消息、输入框、工具卡与运行时接口接入现有后端。它提供流式交互、附件、消息分支及人机协作的前端基础；模型、业务权限和部署策略仍由应用选择。[固定 README](https://github.com/assistant-ui/assistant-ui/blob/6029493d7b20f29f5f10f877de1d6e14c5b595c7/README.md)

## 用法

新项目可使用上游 CLI `create`，既有项目可用 `init`；当前安装文档另推 `npx assistant-ui@latest setup`，让编码 Agent 与浏览器交互完成配置。后者会联网、安装依赖并改写项目，应在可回退 checkout 中检查实际 diff；本轮没有执行这些命令。[安装文档](https://github.com/assistant-ui/assistant-ui/blob/6029493d7b20f29f5f10f877de1d6e14c5b595c7/apps/docs/content/docs/(getting-started)/installation.mdx)

手工路径从 `@assistant-ui/react`、`@assistant-ui/ai-sdk` 与 `ai` 开始，用 `useChatRuntime` 接入 `AssistantRuntimeProvider` 和 Thread。React 包声明支持 React / React DOM 18 或 19。按实际适配器选择兼容包组并锁版本，不将不同包都设成同一 semver。[React 清单](https://github.com/assistant-ui/assistant-ui/blob/6029493d7b20f29f5f10f877de1d6e14c5b595c7/packages/react/package.json)、[CLI 清单](https://github.com/assistant-ui/assistant-ui/blob/6029493d7b20f29f5f10f877de1d6e14c5b595c7/packages/cli/package.json)

## 原理

运行时把后端流、线程状态、工具调用和消息片段映射到可组合 React primitives。AI SDK、LangGraph、AG-UI / A2A 或自定义流使用不同适配器，不能仅凭同名 UI 推断重试 / 恢复完全一致。

当前工具文档推荐 toolkit。`"use generative"` 模块经构建插件拆成服务器与客户端版本：普通 executor 留在服务端，带 `"use client"` 的 executor 在浏览器，`humanTool()` 通过 UI 提交结果，render-only 只显示外部执行的工具调用。旧 `makeAssistantTool` / `useAssistantTool` 已标 deprecated。[工具定义](https://github.com/assistant-ui/assistant-ui/blob/6029493d7b20f29f5f10f877de1d6e14c5b595c7/apps/docs/content/docs/tools/defining-tools.mdx)、[旧 API 状态](https://github.com/assistant-ui/assistant-ui/blob/6029493d7b20f29f5f10f877de1d6e14c5b595c7/apps/docs/content/docs/(reference)/api-reference/tools/component-tools.mdx)

## 价值

把聊天产品中重复的流式状态、滚动、工具反馈与组件结构抽出来，让团队集中验证业务行为。与昨天收录的 AG-UI 相比，它是具体前端库和适配生态；AG-UI 是其中一种连接协议，两者不是替代关系。

## 风险边界

- **安装引导不完全随本地版本冻结。** `setup-agent@0.2.0` 从 setup server 取 guide，缺网即失败；源码限制 256 KiB、拒绝重定向、清理控制字符，并只允许 print / print-status / announce-agent 步骤。这些限制不等于编码 Agent 不会按显示文本执行其他工作；需核对实际依赖与写入。[guide 源码](https://github.com/assistant-ui/assistant-ui/blob/6029493d7b20f29f5f10f877de1d6e14c5b595c7/packages/setup-agent/src/guide.ts)、[辅助包发行](https://github.com/assistant-ui/assistant-ui/releases/tag/setup-agent%400.2.0)
- 工具渲染、human result 和浏览器 executor 各有不同副作用；确认卡和 TypeScript schema 不能代替服务端身份、授权、参数验证及幂等。取消 UI 也需要底层 I/O 传播 abort signal。
- Assistant Cloud 文档以 workspace 拥有线程；API key 仅用于服务端，服务端传入的用户 / workspace 需来自可信身份。换用户或 workspace 时应重建 runtime client，或按文档使独立 client 的认证缓存失效。[Cloud 身份](https://github.com/assistant-ui/assistant-ui/blob/6029493d7b20f29f5f10f877de1d6e14c5b595c7/apps/docs/content/docs/cloud/(auth)/authorization.mdx)
- Cloud retention 删除线程及消息、清除相应 span 输入输出，但保留 runs、span 行、scores 和汇总；缩短窗口延迟 24 小时，之后按小时分批删除。不能把删除会话说成全部关联记录立即消失。[保留策略](https://github.com/assistant-ui/assistant-ui/blob/6029493d7b20f29f5f10f877de1d6e14c5b595c7/apps/docs/content/docs/cloud/(conversations)/retention.mdx)
- MIT 的组件、自建后端、模型服务与可选 Cloud 的数据 / 费用边界分开；支持本地 provider 不保证应用离线。

## 补充建议

先接已有后端和无敏感数据，验证断线、重试、消息去重、工具失败、人工结果与切换身份。接云前画清消息、附件、trace 的出口和保留范围。将工具显示、实际执行、服务端授权及最终业务结果分别验收；不要从演示视频或安装成功推出生产可用。

## 参考资料

- [仓库 API](https://api.github.com/repos/assistant-ui/assistant-ui)、[npm React latest](https://registry.npmjs.org/@assistant-ui%2Freact/latest)、[setup-agent 发行](https://github.com/assistant-ui/assistant-ui/releases/tag/setup-agent%400.2.0)。
- [固定 README](https://github.com/assistant-ui/assistant-ui/blob/6029493d7b20f29f5f10f877de1d6e14c5b595c7/README.md)、[MIT](https://github.com/assistant-ui/assistant-ui/blob/6029493d7b20f29f5f10f877de1d6e14c5b595c7/LICENSE)。
- 本文其余固定 SHA 文档、清单与源码见对应段落链接；仅核读相关内容，未审计整仓或验证 Cloud 服务实现。
