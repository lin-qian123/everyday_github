# dashiAI-ppt-skill

<!-- markdownlint-disable MD013 -->

## 定位

`dashiAI-ppt-skill` 是一个面向 AI agent 的中文 PPT / 网页演示文稿 skill。它强调“生成之后还能编辑”：先生成可横向翻页的 HTML deck，每页自带编辑控制台，再导出可编辑 PPTX。

截至 2026-07-12，GitHub API 显示该仓库约 2439 stars、244 forks，创建于 2026-06-10，许可证为 AGPL-3.0。README 显示其覆盖 12 套视觉主题、1000+ 版式页面和大量可调控件。

## 用法

仓库 README 主要面向 agent skill 使用：把材料交给 Claude Code、Codex、豆包、Marvis、Workbuddy、Dumate、Qclaw 等宿主，让 agent 按 skill 流程生成 HTML PPT，再在浏览器中编辑并导出 PPTX。

典型工作流：

1. 输入文档、主题、受众和汇报目标。
2. 选择视觉主题和页面结构。
3. 浏览器中修改文字、布局、图表、配色和图片。
4. 导出 HTML、PDF 或 PPTX。

## 原理

它把 PPT 生成拆成三个层次：agent 理解材料并选择结构，HTML deck 负责可视化和交互编辑，导出工具再生成可继续办公协作的 PPTX。相比纯图片 PPT，它更强调页面控件和后编辑能力。

## 价值

- 代表中文办公场景中“agent skill + 可编辑交付物”的强需求。
- 对比 `ppt-master`、`presenton`：该项目更突出浏览器内编辑控制台和多主题版式库。
- 对企业汇报、咨询风格材料、产品方案和数据图表类内容有直接应用价值。
- 星数增长说明 PPT skill 仍是 agent 生态中最容易被普通用户理解的入口之一。

## 风险边界

- AGPL-3.0 对商业集成有明确开源义务，企业采用前必须评估许可证。
- 视觉模板多不等于事实准确，内容、数据和引用仍需人工复核。
- 复杂 PPTX 导出可能受浏览器、字体、图表和 Office 兼容性影响。
- 对涉密汇报材料，应先确认本地运行、模型调用和中间文件保存边界。

## 补充建议

- 与 `guizang-ppt-skill`、`ppt-master`、`presenton` 一起观察中文 PPT skill 是否会形成稳定套件。
- 在真实办公流程中评估“修改成本”，而不是只看首屏生成效果。
- 若用于公司内部，建议补充品牌字体、模板合规、数据来源脚注和导出 QA 清单。

## 参考资料

- GitHub 仓库：<https://github.com/chuspeeism/dashiAI-ppt-skill>
- English README：<https://github.com/chuspeeism/dashiAI-ppt-skill/blob/main/README.en.md>
- AGPL-3.0：<https://www.gnu.org/licenses/agpl-3.0.en.html>
