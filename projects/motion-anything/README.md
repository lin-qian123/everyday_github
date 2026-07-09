# motion-anything

<!-- markdownlint-disable MD013 MD012 -->

## 定位

`motion-anything` 是 nexu.io / Open Design 家族中的 agentic motion layer，把“用一句话描述动效”连接到本地动画生成、组件级 motion 编辑、launch video 生成与多格式导出。它面向前端、设计工程和内容团队，强调本地优先、chat-native、零 npm 依赖和多 coding-agent 引擎接入。

截至 2026-07-10 抓取时，GitHub 仓库约 `342` stars、`31` forks，主语言为 JavaScript，许可证为 Apache-2.0。

## 用法

- 从仓库运行本地应用后，用户可以选择 design system 和 motion profile，用自然语言生成 animated page 或 launch video。
- 运行中的页面可点击组件并逐个配置 trigger、preset、keyframe、spring easing、motion path 和 restraint budget。
- 支持导出 JSON、CSS、React、Lottie、MP4、GIF 和 portable skills。
- README 标注可接入 Claude Code、Codex、Cursor、OpenCode、Grok Build、Hermes、Gemini、Open Design Cloud 等引擎或 BYOK API。

## 原理

项目内置大量 motion recipes、design packs、video templates、HTML prototype templates 和 icon 资源。agent 根据用户意图选择 recipe、约束动效强度并写回运行页面。编辑器侧提供 keyframe inspector、timeline、video compositor 和导出流程；偏好减少动效时遵守 `prefers-reduced-motion`，并尽量使用 GPU-safe properties。

## 价值

- 把前端动效从“重新生成整页”变成“在运行页面上逐组件调 motion”。
- 对 landing page、产品 demo、社媒短视频和 design-system proof-of-concept 有直接生产力价值。
- 通过 recipe、avoid_when 和 restraint budget，把“动效品味”显式写成 agent 可执行约束。
- 与 `design-md`、`open-design`、`hyperframes` 形成 AI 设计到动画/视频的连续工作流。

## 风险边界

- README 中的资源数量和引擎数量需要随版本核验，不能直接等同于成熟生产生态。
- 动效生成容易过度设计；真正上线仍需可访问性、性能和品牌审核。
- 导出到 React/Lottie/MP4/GIF 的一致性需在目标浏览器和设备上实测。
- 设计素材、第三方 recipe 和字体资产需要关注许可证和归属说明。

## 补充建议

- 将其归入“语音、视频与多模态”，同时跟踪其与前端设计工具链的交叉。
- 与 `FableCut`、`hyperframes` 比较：前者偏时间线视频剪辑，后两者偏 HTML/CSS/动画生成与渲染。
- 用真实品牌 design token 和 reduced-motion 测试做首轮验证，而不是只看 demo。

## 参考资料

- GitHub 仓库：<https://github.com/nexu-io/motion-anything>
- Open Design：<https://github.com/nexu-io/open-design>
- X 官方账号：<https://x.com/OpenDesignHQ>
