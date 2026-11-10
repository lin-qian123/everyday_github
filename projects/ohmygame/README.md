<!-- markdownlint-disable MD013 -->

# OhMyGame

> 更新：2026-11-11（Asia/Shanghai）。分类：办公、商业与行业应用。上游 `WhiteTowerAI/ohmygame`，仓库 ID `1330417082`；固定源码 `74d392fc72a16060099b9e31036cb1ca359ef196`。仅核官方资料与指定文件，未安装、生成素材、试玩或发布。

## 定位

OhMyGame 把游戏设计文档、素材画布、编码、预览、自动试玩和发布接在同一工作台。内置 Pi Agent，也可接 Claude Code、Codex、OpenCode 以及引擎插件；Web Game、交互故事和 General Game 是不同工作流。[项目说明](https://github.com/WhiteTowerAI/ohmygame/blob/74d392fc72a16060099b9e31036cb1ca359ef196/README.md)

TypeScript daily 为 +201 stars；API 为 2,033 stars / 257 forks / 25 open issues（含 PR）。最新列出的发行是 UTC 11-06 的 [v0.0.0-beta.5.5](https://github.com/WhiteTowerAI/ohmygame/releases/tag/v0.0.0-beta.5.5)，标为预发行；`releases/latest` 未返回稳定版，不能写成没有任何发行。清单版本同为 beta.5.5。[API](https://api.github.com/repos/WhiteTowerAI/ohmygame) / [清单](https://github.com/WhiteTowerAI/ohmygame/blob/74d392fc72a16060099b9e31036cb1ca359ef196/package.json)

## 用法

可选 macOS Apple silicon 或 Windows x64 安装包；先配置语言模型，再按需连接图像、视频、音频、3D provider。浏览器游戏从 Web Game 开始，已有原生引擎项目按插件说明准备对应编辑器。源码路径要求 Bun ≥1.4.2、Node.js ≥22.19：[运行说明](https://github.com/WhiteTowerAI/ohmygame/blob/74d392fc72a16060099b9e31036cb1ca359ef196/README.md)

```bash
git clone --branch main https://github.com/WhiteTowerAI/ohmygame.git
cd ohmygame
bun install --frozen-lockfile
bun run dev:desktop
```

建议首次只做一个场景和一条可玩的核心循环，先审查生成文件和操作权限。内置模型请求、外部 CLI 登录和媒体 provider 是分开的连接；发布还需要应用账号并上传静态构建。不要把拥有订阅理解为所有图像 / 视频 API 均已授权或免费。

## 原理

Pi Agent 通过工具串起文档、素材、代码与游戏操作。Markdown 设计稿、JSON 画布 / 故事节点和普通项目文件共用磁盘状态，GUI 与 Agent 读写同一资产；媒体生成与 `game_use` 试玩都是工具调用。README 注释明确试玩当前为“先规划一批输入，再看结果”的开环方式，不能据此声称实时反馈控制已完成。[架构与试玩说明](https://github.com/WhiteTowerAI/ohmygame/blob/74d392fc72a16060099b9e31036cb1ca359ef196/README.md)

插件 UI 在受限 frame 中，经 MessageChannel 和能力授权访问应用；原生插件则运行在每项目共享的 Node extension host。两者执行边界明显不同。[插件安全模型](https://github.com/WhiteTowerAI/ohmygame/blob/74d392fc72a16060099b9e31036cb1ca359ef196/docs/plugin-security.md)

## 价值

把“描述 → 素材 → 可玩版本 → 观察 → 修改”的迭代集中起来，适合小型原型、交互叙事和跨媒体资产试验。文件化产物方便离开工作台继续编辑；引擎插件与可见试玩能提供审查入口，但还需人工检查操控、节奏、性能和成片 / 成品质量。

## 风险边界

- **默认执行权限较宽**：当前文档列 Claude Code 默认 `bypassPermissions`、Codex 默认 Full Access、OpenCode 默认 Allow all；工作台不额外提供保护目录或 sandbox。这里描述的是本产品的接入配置，不是用户当前 CLI 的设置。[权限说明](https://github.com/WhiteTowerAI/ohmygame/blob/74d392fc72a16060099b9e31036cb1ca359ef196/docs/coding-agents.md)
- **原生插件完全受信任**：能访问当前用户的文件、网络和进程；manifest 中的 host / command 限制约束声明的 MCP，而不约束原生代码自行执行。插件 secrets 文件是 0600 明文，且同项目插件共享进程空间。[插件边界](https://github.com/WhiteTowerAI/ohmygame/blob/74d392fc72a16060099b9e31036cb1ca359ef196/docs/plugin-security.md)
- **供应链撤回不会自动停用已装版本**：市场有签名 / digest 检查，但已安装版本遭封锁后只警告，仍需用户卸载；市场之外来源的检查范围不同。[更新与撤回](https://github.com/WhiteTowerAI/ohmygame/blob/74d392fc72a16060099b9e31036cb1ca359ef196/docs/plugin-security.md)
- **本地工作台仍有网络出口**：提示词发给所选 provider；发行包检查更新并发送使用统计 / 崩溃报告，登录后使用数据关联账号，可在 About 关闭；README 称源码构建不发遥测，尚未做抓包验证。[隐私说明](https://github.com/WhiteTowerAI/ohmygame/blob/74d392fc72a16060099b9e31036cb1ca359ef196/README.md)
- **发布和商业成绩需独立验收**：生成、自动试玩和上传成功不能证明平台审核通过、玩家愿意付费或素材权利完整。代码 Apache-2.0 不涵盖名称 / Logo、模型服务及输入素材权利；Windows 包尚未签名。[许可与交付状态](https://github.com/WhiteTowerAI/ohmygame/blob/74d392fc72a16060099b9e31036cb1ca359ef196/README.md)

## 补充建议

给原型设素材与 API 预算，分开记录生成失败、重试、自动试玩和人工试玩。以专用工作目录起步，逐个审核原生插件与 CLI 权限；发布前检查资源归属、不同屏幕输入、帧率、存档、网络失败及最终构建。将本地验收与真实账号发布分别执行。

## 参考资料

1. [固定 SHA README](https://github.com/WhiteTowerAI/ohmygame/blob/74d392fc72a16060099b9e31036cb1ca359ef196/README.md)
2. [插件安全模型](https://github.com/WhiteTowerAI/ohmygame/blob/74d392fc72a16060099b9e31036cb1ca359ef196/docs/plugin-security.md)
3. [外部编码 Agent 与权限](https://github.com/WhiteTowerAI/ohmygame/blob/74d392fc72a16060099b9e31036cb1ca359ef196/docs/coding-agents.md)
4. [外部 MCP 入口](https://github.com/WhiteTowerAI/ohmygame/blob/74d392fc72a16060099b9e31036cb1ca359ef196/docs/external-agents.md)
5. [Apache-2.0](https://github.com/WhiteTowerAI/ohmygame/blob/74d392fc72a16060099b9e31036cb1ca359ef196/LICENSE) / [TypeScript Trending](https://github.com/trending/typescript?since=daily)
