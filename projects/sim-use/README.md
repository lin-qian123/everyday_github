# sim-use

<!-- markdownlint-disable MD013 MD012 -->

## 定位

`sim-use` 是 LINE Yahoo Japan 开源的移动端 agent 操作 CLI，让 AI agent 能观察并操作 iOS Simulator 与 Android emulator/device。它把屏幕 UI 压缩成 LLM 易读的元素 outline，并通过 alias、accessibility id、label 或坐标执行点击、滑动、输入和截图。

截至 2026-07-10 抓取时，GitHub 仓库约 `742` stars、`41` forks，主语言为 Swift，许可证为 Apache-2.0。

## 用法

- macOS 上推荐通过 Homebrew 安装：`brew tap lycorp-jp/tap && brew install lycorp-jp/tap/sim-use`。
- agent loop 常用流程是 `sim-use ui` 读取屏幕、`sim-use tap @9` 操作元素、再用 `sim-use ui` 验证结果。
- iOS 通过 Simulator HID 与 Accessibility API 操作；Android 通过一次性安装 bridge APK 后使用 AccessibilityService。
- 可用 `sim-use init --client claude` 安装 agent skill，让 Claude Code 等客户端理解命令面。

## 原理

项目把真实移动设备/模拟器的 accessibility tree 转成紧凑 outline，并给元素缓存 `@N` alias。agent 不需要处理完整 JSON 树或猜坐标，而是用结构化 UI 文本推理，再调用统一命令面执行动作。后台 daemon 摊销初始化成本，使 observe-act 循环保持低延迟。

## 价值

- 补上 mobile app agent 开发中“写完代码但无法亲自点模拟器验证”的缺口。
- outline 表示比原始 accessibility JSON 更省 token，适合长任务回路。
- iOS 与 Android 使用同一命令风格，便于写跨平台验证脚本。
- 对移动端自动化测试、agent 自验收、demo 录制和 UI 回归检查都有直接价值。

## 风险边界

- 依赖 accessibility 暴露质量；自绘 UI、游戏画面或未标注控件可能退化到截图/坐标。
- iOS 构建依赖 Xcode 和 macOS 版本，Android 侧需要设备权限与 bridge APK。
- agent 自动点击真实设备存在误操作风险，应优先在模拟器、测试账号和沙箱后端中使用。
- 它解决的是观察和操作层，不替代 Playwright/Appium 等断言体系。

## 补充建议

- 与 `Agent-S`、`GUI-Agents-Paper-List` 和 browser-use 系列一起观察，判断 GUI agent 能否从网页扩展到移动端。
- 在实际项目中把 `sim-use ui` 输出、操作命令和截图作为验收证据归档。
- 若用于 CI，应先固定模拟器版本、屏幕尺寸、语言和系统设置。

## 参考资料

- GitHub 仓库：<https://github.com/lycorp-jp/sim-use>
- Meta idb：<https://github.com/facebook/idb>
- X 讨论入口：<https://x.com/QingQ77/status/2072704599962890742>
