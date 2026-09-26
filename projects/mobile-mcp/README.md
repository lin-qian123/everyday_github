<!-- markdownlint-disable MD013 -->

# Mobile MCP（mobile-next/mobile-mcp）

> 上游仓库：<https://github.com/mobile-next/mobile-mcp> · 归类：Agent 框架与技能生态 · 本页基于 2026-09-27 的 GitHub API、README、Security Policy、Release、tag 与 manifest 静态整理，未连接模拟器、真机或 Mobile Next Cloud。

- 抓取快照：7,318 stars、640 forks、43 open issues。
- 热度信号：GitHub TypeScript Trending 抓取时约 +143 当日 stars。
- 版本与许可：Apache-2.0；latest Release 为 `1.0.4`，最新 tag 为 `1.0.5`，根 `package.json` 仍写 `0.0.1`。

## 定位

Mobile MCP 是面向 iOS 与 Android 的 MCP 自动化服务器，让 Codex、Claude Code、Copilot 等 Agent 用统一工具控制模拟器、仿真器和真机。它优先读取原生 Accessibility tree，必要时再用截图与坐标操作，覆盖测试、数据录入、用户旅程和移动端开发调试。

## 用法

本地模式需要 Node.js 20+、Xcode command line tools 或 Android Platform Tools，并先启动 / 授权测试设备。MCP 客户端可用 `npx -y @mobilenext/mobile-mcp@latest` 启动，Codex 也可执行 `codex mcp add mobile-mcp npx "@mobilenext/mobile-mcp@latest"`。首次使用应固定版本并只连接专用测试设备，不直接接入个人手机、生产账号或真实支付环境。

## 原理

服务把 device discovery、app 安装 / 启停、屏幕元素、手势、键盘、剪贴板、GPS、日志、崩溃报告和录屏封装为 MCP tools。结构化 accessibility snapshot 降低视觉 token 与坐标漂移；缺少语义节点时再回退截图坐标。远程路径还可登录 Mobile Next Cloud、分配物理设备并在同一工具面释放资源。

## 价值

它把 XCUITest、`simctl`、ADB 与设备差异收敛到一套 Agent 接口，便于跨平台生成可复用的移动测试流程。结构化元素和 batch command 比纯截图点击更容易调试，也适合把 crash log、screen recording 与自动化步骤放进同一证据链。

## 风险边界

- 上游 Security Policy 明确 Agent 可在设备安全范围内操作，建议使用专用设备；MCP server 不是移动应用 sandbox。
- 工具可读写剪贴板、日志、截图和屏幕元素，也可安装 / 卸载应用、修改位置、打开 URL 和输入文字；错误授权可能暴露验证码、通知、账号与本地文件。
- Accessibility tree 可能缺失 canvas、游戏、WebView 或自定义控件；坐标回退会受分辨率、方向、动画、弹窗和区域设置影响。
- Cloud 模式引入登录、远程真机、租期和外部数据流；“同一套 tools”不代表本地与云端的隐私、留存和网络边界相同。
- Release、tag 与根 manifest 版本不一致；使用 `@latest` 还会把供应链和行为变化带入不可复现流程。

## 补充建议

固定 npm 版本与 commit，在无真实账号的专用模拟器和测试真机上建立 accessibility / coordinate 双路径 fixture。对安装、剪贴板、GPS、URL、日志和 cloud allocation 单独设审批；记录设备型号、OS、locale、orientation 与 app build，并用独立断言验证动作结果，而不是把 Agent 文本当作测试通过。

## 参考资料

- [GitHub 仓库](https://github.com/mobile-next/mobile-mcp)
- [GitHub REST API](https://api.github.com/repos/mobile-next/mobile-mcp)
- [1.0.4 Release](https://github.com/mobile-next/mobile-mcp/releases/tag/1.0.4)
- [Security Policy](https://github.com/mobile-next/mobile-mcp/blob/main/SECURITY.md)
- [根 package.json](https://github.com/mobile-next/mobile-mcp/blob/main/package.json)
- [LICENSE](https://github.com/mobile-next/mobile-mcp/blob/main/LICENSE)
- [官方 Wiki](https://github.com/mobile-next/mobile-mcp/wiki)
