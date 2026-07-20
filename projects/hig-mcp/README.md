<!-- markdownlint-disable MD013 -->

# hig-mcp

## 定位

`hig-mcp` 是一个把 Apple Human Interface Guidelines 转成结构化 design tokens 的 MCP server，面向 Claude Code、Cursor 等 AI coding agent。它关注 iOS / macOS 设计实现中常被 agent 误读的系统颜色、字号、布局、Liquid Glass 约束和 SwiftUI 映射。

## 用法

```bash
pipx install hig-mcp
claude mcp add hig -- hig-mcp
```

其他 MCP client 可按 stdio server 配置 `hig-mcp`。主要工具包括 `hig_get_tokens`、`hig_check_liquid_glass`、`hig_swiftui` 和 `hig_fetch`。

## 原理

项目把 HIG 中适合机器读取的部分整理为本地 JSON token，例如颜色、typography、material、layout、SwiftUI 和 SF Symbols 映射；需要最新 prose 时再通过 `sosumi.ai` 获取 Markdown。每个 token 带 provenance 标记，区分 Apple-published facts、WCAG 规则、社区最佳实践和 beta 阶段需验证项。

## 价值

- 解决 agent 生成 Apple UI 时常见的“训练数据过期、颜色硬编码、Liquid Glass 规则缺失”问题。
- 适合 iOS/macOS 项目把设计规范作为工具调用结果，而不是让模型凭记忆生成。
- 与 `design-md`、`stitch-mcp`、`openpencil` 等“设计上下文进入 coding agent”的趋势一致。

## 风险边界

- Apple HIG 和平台 API 会持续变化，token 需要跟随验证。
- 项目不隶属于 Apple，生产发布前仍应以官方 HIG 和 Xcode SDK 为准。
- `hig_fetch` 依赖外部服务，离线环境只能使用本地 token。
- 对视觉质量的保障仍需要截图验证、辅助功能检查和人工设计审查。

## 补充建议

- 适合放入 Apple 平台应用的开发环境，作为 coding agent 的 HIG 查询入口。
- 可把 Reduce Transparency、contrast after blur、hit target 等约束写进项目验收 checklist。
- 对跨平台 UI 项目，应避免把 Apple token 误用于 Web 或 Android 设计系统。

## 参考资料

- GitHub：<https://github.com/aka-kika/hig-mcp>
- Apple Human Interface Guidelines：<https://developer.apple.com/design/human-interface-guidelines/>
- sosumi.ai：<https://sosumi.ai>
