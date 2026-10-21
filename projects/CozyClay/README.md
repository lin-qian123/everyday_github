<!-- markdownlint-disable MD013 -->

# CozyClay

> 更新：2026-10-22（Asia/Shanghai）。分类：语音、视频与多模态。主上游 `NomaDamas/CozyClay`；默认分支快照 `567c9d447f08`。官方资料与源码静态研究；热度、发行及社媒口径见[当日日报](../../daily/2026-10-22/ai-hotspots.md)。

## 定位

浏览器中的 3D 预演工具：先摆人物与场景、编动作、切镜头，再把首尾帧、灰模参考视频和提示词交给 AI 视频模型。包含 storyboard、景深 / 法线等导出与 Agent 控制面，不能把预演约束等同于下游视频必然服从。[README.md](https://github.com/NomaDamas/CozyClay/blob/567c9d447f08f169663a3b47a3880894be23facb/README.md)

## 用法

官方入口 `npx cozyclay`，要求 Node.js `>=22.19.0` 与 Chromium，工作室默认 `http://127.0.0.1:5180/app/`。先手动建立一个场景并导出，再接 Agent；MCP 入口为 `npx -y cozyclay mcp`。[README.md](https://github.com/NomaDamas/CozyClay/blob/567c9d447f08f169663a3b47a3880894be23facb/README.md) [package.json](https://github.com/NomaDamas/CozyClay/blob/567c9d447f08f169663a3b47a3880894be23facb/package.json)

本地建分镜不要求下载大模型；内置聊天可登录 ChatGPT 或配置模型服务，视频生成和相关素材生成另有后端与费用。不要把“打开本地页面”写成所有 AI 步骤都离线。[README.md](https://github.com/NomaDamas/CozyClay/blob/567c9d447f08f169663a3b47a3880894be23facb/README.md)

## 原理

场景、角色和镜头形成可编辑状态；Agent 写运动规格，浏览器中的确定性编译器烘焙帧并做碰撞、滑步、接触等 QA。MCP / CLI / 面板操作同一 live studio；导出给视频模型的是参考条件，而不是经过验证的最终运动学或物理仿真。[README.md](https://github.com/NomaDamas/CozyClay/blob/567c9d447f08f169663a3b47a3880894be23facb/README.md) [mcp/README.md](https://github.com/NomaDamas/CozyClay/blob/567c9d447f08f169663a3b47a3880894be23facb/mcp/README.md)

## 价值

工程判断：把昂贵的视频重抽样前移为便宜的构图、时序和镜头修改，适合比较多个分镜方案。是否减少总生成成本应按固定镜头、模型和重试次数评估，本轮没有成本实验。

## 风险边界

- 官网与官方 npm 制品默认有用量遥测；隐私文档列出 PostHog US Cloud、随机标识、功能与设备分桶等。源码 checkout / fork / CI 等按文档不发送；分发来源决定默认行为，不能简单归为“本地无网络”。[docs/privacy.md](https://github.com/NomaDamas/CozyClay/blob/567c9d447f08f169663a3b47a3880894be23facb/docs/privacy.md)
- `cclay telemetry off` 可关闭；启动前可设 `COZYCLAY_TELEMETRY=0` 或 `DO_NOT_TRACK=1`。状态默认 `telemetryEnabled: true`；环境变量暂停与删除持久标识的行为不同。文档称不采 prompt / 项目内容，本轮核了配置，未抓包证明全路径。[bin/telemetry-state.mjs](https://github.com/NomaDamas/CozyClay/blob/567c9d447f08f169663a3b47a3880894be23facb/bin/telemetry-state.mjs) [docs/privacy.md](https://github.com/NomaDamas/CozyClay/blob/567c9d447f08f169663a3b47a3880894be23facb/docs/privacy.md)
- Agent 和生成后端有自己的数据出口、密钥与权限，关闭 analytics 不会自动关闭模型调用。人物、参考图片、字体和权重需各自核权利。[README.md](https://github.com/NomaDamas/CozyClay/blob/567c9d447f08f169663a3b47a3880894be23facb/README.md) [LICENSING.md](https://github.com/NomaDamas/CozyClay/blob/567c9d447f08f169663a3b47a3880894be23facb/LICENSING.md)
- 当前组合程序 AGPL-3.0-or-later；许可说明要求修改版网络服务提供对应源码，并通过 `VITE_SOURCE_CODE_URL` 设置来源入口。第三方材料仍有独立条款。[LICENSING.md](https://github.com/NomaDamas/CozyClay/blob/567c9d447f08f169663a3b47a3880894be23facb/LICENSING.md)

## 补充建议

用自制角色和三镜头短场景先测保存、重开、undo 和导出；把 QA 指标与人工观感分开记录，再对比有 / 无预演的成功率、重试和总费用。固定 npm 版本与遥测状态，MCP 先在测试场景中用。本轮未运行工作室或生成视频。

## 参考资料

- [README.md](https://github.com/NomaDamas/CozyClay/blob/567c9d447f08f169663a3b47a3880894be23facb/README.md)
- [package.json](https://github.com/NomaDamas/CozyClay/blob/567c9d447f08f169663a3b47a3880894be23facb/package.json)
- [LICENSE](https://github.com/NomaDamas/CozyClay/blob/567c9d447f08f169663a3b47a3880894be23facb/LICENSE)
- [LICENSING.md](https://github.com/NomaDamas/CozyClay/blob/567c9d447f08f169663a3b47a3880894be23facb/LICENSING.md)
- [docs/privacy.md](https://github.com/NomaDamas/CozyClay/blob/567c9d447f08f169663a3b47a3880894be23facb/docs/privacy.md)
- [bin/telemetry-state.mjs](https://github.com/NomaDamas/CozyClay/blob/567c9d447f08f169663a3b47a3880894be23facb/bin/telemetry-state.mjs)
- [mcp/README.md](https://github.com/NomaDamas/CozyClay/blob/567c9d447f08f169663a3b47a3880894be23facb/mcp/README.md)
- [仓库 API](https://api.github.com/repos/NomaDamas/CozyClay)
- [v3.0.3 Release](https://github.com/NomaDamas/CozyClay/releases/tag/v3.0.3)
