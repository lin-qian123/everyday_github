# hermex

- GitHub：<https://github.com/uzairansaruzi/hermex>
- 官网：<https://hermexapp.com/>
- 抓取时间：2026-07-05（Asia/Shanghai）
- 今日信号：GitHub API 显示该仓库创建于 2026-07-02，抓取时约
  `539 stars / 56 forks`，README 定位为 self-hosted Hermes agent 的原生 iPhone 控制端。

## 定位

`hermex` 是一个 SwiftUI iPhone 应用，用手机控制自托管的 Hermes /
hermes-webui agent。它强调手机是控制面，真正的 agent、工具和数据仍在用户自己的服务器上运行。

这代表了 agent 产品形态的一条新分支：不是把 agent 全部塞进移动端，
而是让移动端成为会话、任务、skills、文件和用量的远程 cockpit。

## 用法

项目 README 给出的使用方式包括：

- 从 App Store 安装 iOS 18+ 应用。
- 准备一个自托管 Hermes / hermes-webui 服务。
- 在手机端连接自己的服务器。
- 从手机上发起/停止会话、切换模型、浏览 sessions、查看 tasks、
  搜索 skills、查看 workspace、memory 和 insights。

项目明确强调没有订阅、没有内购、没有第三方 relay，应用只与用户配置的服务器通信。

## 原理

`hermex` 本身不承担推理计算。它的核心职责是：

1. 用原生 iOS UI 管理 agent 会话与项目。
2. 将聊天、文件、模型选择、reasoning effort、profile 等控制参数发送到自托管服务。
3. 流式展示回复、thinking 信息和 tool call 细节。
4. 离线缓存 sessions，提供只读 memory / insights 面板。

这种架构把移动端体验和服务端 agent 能力分离，适合自托管用户在离开桌面时继续监督任务。

## 价值

- 对 self-hosted agent 用户：提供比浏览器网页更自然的移动端操作入口。
- 对 agent 产品设计：展示“服务器执行、手机监督”的控制面模式。
- 对隐私敏感用户：相比托管 SaaS，数据路径更可控，但前提是用户真的能维护自己的服务器。

## 风险边界

- 它依赖 Hermes / hermes-webui 服务端能力，不能单独完成 agent 任务。
- 移动端远程控制文件系统、任务和 skills 时，权限边界必须谨慎配置。
- “无第三方 relay”降低了中间人风险，但用户仍需处理服务器暴露、TLS、认证和备份。
- App Store 版本、服务端 API 兼容性和项目维护节奏可能变化，需要持续验证。

## 补充建议

- 与 `hermes-studio`、`cherry-studio`、`open-webui` 横向比较：它更偏移动端控制面，
  不是通用桌面聊天壳。
- 如果团队使用，应先明确哪些任务允许从手机触发，哪些必须留在桌面或 CI 环境。
- 后续关注它是否支持更多 agent backend，而不是只围绕 Hermes 生态。

## 参考资料

- GitHub 仓库：<https://github.com/uzairansaruzi/hermex>
- 项目官网：<https://hermexapp.com/>
- App Store：<https://apps.apple.com/app/hermex/id6767006319>
- Hermes WebUI：<https://github.com/nesquena/hermes-webui>
