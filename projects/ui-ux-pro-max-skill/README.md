<!-- markdownlint-disable MD013 -->

# ui-ux-pro-max-skill

## 定位

`ui-ux-pro-max-skill` 是一个面向 AI coding agents 的 UI/UX 设计 skill，试图把设计系统生成、行业风格匹配、色彩、排版、动效、可访问性和交付检查封装成可安装的 agent 能力。

它属于“前端设计约束进入 agent skills”路线，和 `design-md`、`openpencil`、`stitch-mcp` 一样，核心问题是让 coding agent 不只会写组件，还能遵守可复用的设计判断。

## 用法

项目提供 npm CLI 与 skill 包。典型用法是把它安装到 Claude Code、Codex、Cursor、Antigravity、Kiro、Trae、Qoder 等宿主工具可读取的技能目录，然后在生成落地页、移动端界面、dashboard 或品牌页面时让 agent 调用其规则库。

README 展示的 v2.0 重点是 Design System Generator：根据产品类型、行业、目标用户和页面目标，检索并组合 UI 分类、风格、色板、落地页 pattern、字体组合和反模式清单。

## 原理

项目把设计经验拆成结构化规则与检索数据：

- 161 类产品 / 行业 UI 规则。
- 67 种 UI 风格。
- 161 套色彩方案。
- 24 种 landing page pattern。
- 57 组字体搭配。
- 可访问性、响应式、hover、focus、动画和交付前检查项。

agent 不是凭空“审美”，而是在用户需求和规则库之间做匹配，输出更具体的设计系统建议与实现约束。

## 价值

- **降低 AI 前端同质化**：把行业、品牌、页面目的和反模式显式写入生成过程。
- **提升交付检查**：强调对比度、响应式断点、focus state、hover state 和 reduced motion。
- **适合团队固化规范**：可以把主观设计偏好变成 agent 可复用的技能包。
- **连接设计与代码**：让设计 token、字体、布局 pattern 和实现检查进入同一个 coding agent 工作流。

## 风险边界

- 规则库不能替代真实用户研究、品牌系统和设计评审。
- 生成的色彩、字体和布局仍需人工检查版权、可访问性、性能和业务语境。
- 若把 skill 当成万能审美判断器，仍可能产出模板化界面。
- 对复杂产品工具和高密度后台系统，应避免过度营销页化和装饰化。

## 补充建议

- 更适合用作“设计检查清单 + 设计系统初稿”，而不是最终视觉决策者。
- 与 `design-md` 结合时，可以把项目级设计契约写入仓库，再让该 skill 做场景化生成和验收。
- 对企业项目建议沉淀自己的品牌 token、组件禁用项和行业示例，减少通用规则误配。

## 参考资料

- GitHub 仓库：<https://github.com/nextlevelbuilder/ui-ux-pro-max-skill>
- 项目网站：<https://uupm.cc>
- npm 包：<https://www.npmjs.com/package/ui-ux-pro-max-cli>
