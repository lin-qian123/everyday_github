<!-- markdownlint-disable MD013 -->

# remote-mic-app / SayAll：蓝牙遥控器语音入口与可选只读历史 MCP

- 上游：[HD838A/remote-mic-app](https://github.com/HD838A/remote-mic-app)；repository ID `1308856749`；产品名“无线麦 SayAll”。
- 更新：2026-11-05（Asia/Shanghai）；分类：语音、视频与多模态。
- 固定 main SHA：`fe09cb090b7aa3e9ddbfcc58a93955cc907f71a8`；API 2,435 stars / 256 forks / 110 open issues（含 PR）；Swift daily +78。
- 发行列表首项 v1.9.21（UTC 2026-09-03）；主线候选能力与稳定安装包分开看。代码 GPL-3.0-only，Logo / App Icon 单独授权。
- 范围：固定 README、AI 配置、授权 / 存储实现与官网回链静态核读；未安装驱动、授权、配对遥控器、录音、连接 MCP 或试听。

## 定位

让兼容蓝牙语音遥控器成为 Mac 的麦克风和按键入口，再配合豆包、微信、Typeless 等语音工具完成输入。它不是独立语音模型；识别质量与数据出口还取决于实际使用的第三方工具。主线另有可选“回眸”文字历史和本机只读 MCP。

## 用法

macOS 路径要求 Apple Silicon / macOS 14+，或 Intel / macOS 13+。按芯片选择 Installer PKG：官网稳定入口当前仅 Apple Silicon；Intel 与 Apple Silicon 的预览包从 Releases 区分下载。

安装器包含应用与按需安装 / 更新的 MiRemoteV 2ch 驱动；已有兼容回环设备的高级用户可选择 App-only ZIP。核对资产摘要、签名、系统版本和目标语音工具，再按引导配置蓝牙、音频与语音键。上游说明签名 / 公证是发布流程声明，本轮没有下载验证安装包。

先做短句输入测试，再决定是否开启回眸或 Agent 访问。MCP 通过随 App 的 Swift Helper 以 `stdio` 启动，不需要为此安装 Node.js。快速连接会修改客户端配置并创建私有备份，应先核目的客户端与配置位置。

## 原理

- 遥控器的蓝牙音频经兼容回环设备送给目标语音工具，按键生命周期触发开始 / 停止；不会仅因连接而证明音频链路正常。
- 普通按键可映射本机动作；语音键的 Fn 点按兼容模式默认关闭，与遥控器“按住采音、松开结束”仍是两层行为。
- 主动开启回眸后，只归档通过 SayAll 输入并最终稳定出现的文字，按 App 与日期组织；文档说明不保存音频、不读取完整聊天和输入框上下文。
- Agent 访问默认关闭，授权按客户端创建并可撤销；当前实现的 scope 为 `transcripts.read.all`，即授权边界内的历史读取，而不是每条记录逐次授权。
- 授权存储使用 token / Helper 路径哈希；客户端配置仍必须保存实际 token 和 Helper 路径。`stdio` 不监听 HTTP / TCP，也不改变模型 provider 的网络行为。

## 价值

可让语音输入有更明确的物理按键，并把本人主动保留的表达作为 Agent 查询材料。适合先验证硬件舒适性、目标工具兼容和输入稳定性，再评价是否减少工作中切换成本。

## 风险边界

- 蓝牙、输入监控、辅助功能各有用途；修饰键触发、App 自动匹配、复合动作与第三方语音工具要分别实测，避免错误聚焦、按键未释放或误输入。
- 回眸、按 App 切换和组合动作在 README 中分别标记为候选 / 新增、真实环境验证中；源码存在和界面可见不等于稳定包已包含或完整真实语音验收通过。
- 回眸和本地 Agent 访问默认关闭，启用前确定保留内容与读取范围；第三方客户端可能将读到的历史发往云模型，不能从“本地 stdio”推断全流程不外发。
- 客户端配置中的实际 token 是敏感凭据，勿公开或同步到公共仓库；关闭总开关会阻止访问但不删除历史，撤销授权与删除数据是不同操作。
- 本地统计与回眸存储不代表应用完全不联网：文档有每日更新检查，用户确认后安装；Sparkle 只更新 App，驱动仍由 Installer PKG 管理。
- iOS 现为独立私有仓库，不能把 macOS GPL 源码的可复核范围扩展到 iOS / Watch 或其他客户端；品牌资产另有权利条件。

## 补充建议

先用无敏感内容的固定短句，核对按下、松开、断连、唤醒、目标 App 切换和输入结果。若启用 MCP，使用小 limit 查询自建测试记录，再验证关闭总开关和撤销客户端后的拒绝行为，同时检查第三方模型出口。

## 参考资料

- [README、候选能力与隐私](https://github.com/HD838A/remote-mic-app/blob/fe09cb090b7aa3e9ddbfcc58a93955cc907f71a8/README.md)、[AI / MCP 配置](https://github.com/HD838A/remote-mic-app/blob/fe09cb090b7aa3e9ddbfcc58a93955cc907f71a8/AI_SETUP.md)。
- [授权存储与 scope](https://github.com/HD838A/remote-mic-app/blob/fe09cb090b7aa3e9ddbfcc58a93955cc907f71a8/Sources/SayAllMCPKit/SayAllMCPAuthorizationStore.swift)、[历史归档](https://github.com/HD838A/remote-mic-app/blob/fe09cb090b7aa3e9ddbfcc58a93955cc907f71a8/Sources/RemoteMic/TranscriptArchiveStore.swift)。
- [软件许可](https://github.com/HD838A/remote-mic-app/blob/fe09cb090b7aa3e9ddbfcc58a93955cc907f71a8/LICENSE.md)、[品牌资产许可](https://github.com/HD838A/remote-mic-app/blob/fe09cb090b7aa3e9ddbfcc58a93955cc907f71a8/LOGO-LICENSE.md)。
- [v1.9.21](https://github.com/HD838A/remote-mic-app/releases/tag/v1.9.21)、[API](https://api.github.com/repos/HD838A/remote-mic-app)、[官网](https://sayall.app/)。
