<!-- markdownlint-disable MD013 MD034 -->

# thinking-orbs：为 Agent 状态设计的轻量 Canvas 动效组件

> 上游仓库：https://github.com/Jakubantalik/thinking-orbs · 归类：前端、UI 与 Agent 交互层 · 本页基于 2026-09-22 的 README、package、许可证与 REST API 静态整理；未安装 npm 包、跑视觉回归或测量端侧性能。

## 定位

`thinking-orbs` 是一个 React / TypeScript 组件库，用 2D Canvas 把 `working`、`searching`、`solving`、`listening`、`connecting` 等九种 Agent 状态画成点阵球形动效。它解决的是界面反馈与状态辨识，不负责推理、任务调度或真实进度计算。

2026-09-22 的 GitHub 官方 TypeScript Trending 抓取显示约 `+203 stars today`；REST API 快照为 `3,107 stars / 249 forks / 20 open issues`，MIT，无 GitHub Release，默认分支最后 push 为 2026-08-16。

## 用法

```sh
npm install thinking-orbs
```

```tsx
import { ThinkingOrb } from "thinking-orbs";

export function AgentState() {
  return <ThinkingOrb state="searching" size={64} aria-label="正在检索资料" />;
}
```

组件提供 `20` 与 `64` 两套单独调参的尺寸，以及 `auto` / `dark` / `light` 主题、速度和暂停选项。上线前应把枚举状态与应用自己的有限状态机显式映射。

## 原理

- 每个状态使用独立点阵、轨迹和节奏，而不是给同一 spinner 换文字。
- 只用 Canvas 2D arc，不依赖 WebGL、滤镜或 SVG filter；device pixel ratio 被限制到 2。
- `auto` 主题依次观察祖先 `data-theme` / class、系统 `prefers-color-scheme`，并在客户端绘制以避免 SSR 直接访问 Canvas。
- 实例共享一个 animation clock；离开 viewport 或页面隐藏时通过 observer 暂停。
- `prefers-reduced-motion` 下输出静态代表帧，并以 `role="img"` 与每状态默认 `aria-label` 暴露语义。

## 价值

- 将“正在做什么”从单一 loading spinner 拆成可区分的语义状态，有助于长任务界面建立预期。
- 20 px 与 64 px 分别针对行内和头像尺度设计，比运行时任意缩放更可控。
- 自动主题、reduced motion 和不可见暂停覆盖了常见产品化细节。
- API 很小，适合聊天、Agent dashboard、Copilot panel 或 workflow 节点直接嵌入。

## 风险边界

- 动效只反映应用传入的字符串；它不能证明 Agent 真在检索、求解或连接，也不能表达百分比进度。
- `role="img"` 的重复状态变化可能让屏幕阅读器产生噪声；关键进度仍应使用文本或合适的 live region。
- Canvas 输出需在 Safari、低端设备、缩放、高对比度和 reduced-motion 环境做视觉 / 可访问性回归。
- 仓库没有 GitHub Release；直接追随 npm `latest` 或默认分支会扩大供应链和不可重复构建风险。
- 本页未验证多实例 CPU / GPU 占用、内存回收或 SSR hydration 行为。

## 补充建议

1. 固定 package 版本与 lockfile，不从 GitHub 默认分支直接安装。
2. 用真实 Agent state machine 驱动，并为超时、失败、等待用户、取消增加文字状态，避免“永远在思考”。
3. 在 1x / 2x DPR、暗色 / 亮色、Safari / Chromium / Firefox 与 reduced motion 下做截图回归。
4. 对屏幕阅读器只播报有意义的状态转移，装饰性 orb 可按场景设置隐藏。

## 参考资料

- 上游 README：https://github.com/Jakubantalik/thinking-orbs
- 在线 Demo：https://orbs.jakubantalik.com
- npm：https://www.npmjs.com/package/thinking-orbs
- GitHub REST API：https://api.github.com/repos/Jakubantalik/thinking-orbs
- LICENSE：https://github.com/Jakubantalik/thinking-orbs/blob/main/LICENSE
