# open-kimi-ppt-skill

- 仓库：[Binaryify/open-kimi-ppt-skill](https://github.com/Binaryify/open-kimi-ppt-skill)
- 快照：2026-08-06 抓取；GitHub API 显示其创建于 2026-08-05，约 550 stars、155 forks，MIT。数字会随时间变化。
- 分类：办公、商业与行业应用

## 定位

非官方的 Kimi Slides 兼容演示文稿 Skill，面向兼容 `SKILL.md` 的 coding agent 生成、读取、编辑和导出 PPTD/PPTX，并附带本地浏览器编辑器。

## 用法

需 Node.js 18+。按仓库说明执行 `npx open-kimi-ppt-skills install`，或让支持 skills 的 Agent 安装该仓库；可用自然语言指定主题、页数、风格和参考模板。用 `npx open-kimi-ppt-skills serve` 启动本地编辑器，在授权目录中复查 PPTD 后再导出 PPTX。

## 原理

项目以逐页 PPTD 中间表示承载内容、版式与媒体，再生成真实可编辑 PPTX；README 声称导出前可用多模态模型检查图片总览中的遮挡、越界和文字溢出。该路线试图避开“整页图片幻灯片”难以二次编辑的问题。

## 价值

同时保留结构化源文件和可交付 PPTX，适合需要人工续改、模板复用及版本管理的办公场景。浏览器编辑器让非开发者可在 agent 初稿之后直接查看与调整。

## 风险边界

该项目明确为非官方逆向实现，Kimi/Moonshot 的网页资源、协议或格式变化可使兼容性失效；生成内容、素材授权、字体嵌入和 PPTX 跨版本渲染均须人工验收。安装会写入用户级 skills 目录，先在隔离账户检查包内容。

## 补充建议

将源材料、许可证明和视觉验收清单纳入交付；以 PowerPoint、WPS 和目标投放环境分别打开关键样稿。不要把视觉质检声明当作无障碍、品牌合规或事实准确性的保证。

## 参考资料

- [项目 README](https://github.com/Binaryify/open-kimi-ppt-skill)
- [npm 包入口](https://www.npmjs.com/package/open-kimi-ppt-skills)
- [GitHub API 元数据快照](https://api.github.com/repos/Binaryify/open-kimi-ppt-skill)
