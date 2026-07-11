# pixel2motion

<!-- markdownlint-disable MD013 -->

## 定位

`pixel2motion` 是面向 Codex / Claude 的 logo 动效生成 skill。它把 PNG、JPG、WebP 或截图中的 raster logo 转成 motion-ready SVG，再生成 SVG logo animation、HTML 动效 demo、GIF / video 预览和 motion QA 证据。

截至 2026-07-12，GitHub API 显示该仓库约 1619 stars、153 forks，创建于 2026-06-12，许可证为 MIT。项目主页展示了从像素 logo 到 SVG 动效的交互演示。

## 用法

仓库提供 `SKILL.md`，可作为 Codex / Claude skill 使用。典型流程：

1. 提供 logo 图片或截图。
2. skill 将像素轮廓拟合为简洁 SVG。
3. 生成 motion 方案和可交互 HTML demo。
4. 导出 GIF、视频预览或透明视频，并保留拟合与动效 QA 证据。

## 原理

项目把品牌动效拆成“矢量重建 -> SVG 结构 -> 动效时间线 -> 预览和 QA”。这种拆法对 agent 友好：每一步都有中间产物，可被人审查，也便于根据反馈调整节奏、路径、透明度和导出格式。

## 价值

- 说明 agent skill 正从文本 / 代码扩展到设计生产中的可审查交付物。
- 对品牌 logo reveal、网站 loading、产品发布页和社媒短视频素材有直接用途。
- MIT 许可证降低试用门槛。
- 与 `motion-anything`、`FableCut`、`hyperframes` 共同体现“agent-native motion workflow”趋势。

## 风险边界

- raster-to-SVG 拟合对复杂 logo、渐变、细节纹理和商标准确性有限。
- 生成动效不能替代品牌规范审查，尤其是大型企业的 logo 使用规则。
- 视频 / GIF 导出质量依赖本地浏览器、渲染器和字体环境。
- 如果输入 logo 涉及第三方版权或商标，生成结果仍需授权确认。

## 补充建议

- 适合先在内部 demo、开源项目 logo、个人品牌素材中试用。
- 与 `pixel2svg-html` 配套观察：一个偏矢量重建，一个偏 motion。
- 对商业设计交付，应把原图、SVG、HTML、导出视频和 QA 截图一起归档。

## 参考资料

- GitHub 仓库：<https://github.com/nolangz/pixel2motion>
- 在线演示：<https://nolangz.github.io/pixel2motion/>
- Skill instructions：<https://github.com/nolangz/pixel2motion/blob/main/SKILL.md>
