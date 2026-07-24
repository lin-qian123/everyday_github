# scientific-illustrator

## 定位

`scientific-illustrator` 是 Codex 插件，面向 Microsoft PowerPoint 与 draw.io Desktop 将科研插图复刻或设计为尽可能可编辑的原生对象，并用 Designer → Drawer → Reviewer → Corrector 质量闭环持续检查。截至 2026-07-25，仓库创建于 2026-07-24，约 8 stars、1 fork，采用 MIT 许可证。

## 用法

先审阅安装脚本；可克隆仓库后执行 `codex plugin marketplace add "$(pwd)"` 与 `codex plugin add scientific-illustrator@scientific-illustrator-tools`，重启 Codex 并开启新任务。选择 PowerPoint 或 draw.io，并说明是参考图复刻、无参考图设计、审查还是修正；PowerPoint 实时控制需要 Windows 桌面版 Office，draw.io 可走桌面端。

## 原理

插件先检测后端能力，再逐面板优先生成原生文本、形状、连接线、表格与图表，仅把不能可靠表达的最小区域保留为原子图片。每个局部都经历结构检查与真实渲染检查；PowerPoint 通过本机 COM 控制，draw.io 通过绑定 `127.0.0.1` 的调试通道操作 graph API。

## 价值

- 关注“可编辑交付物”而非把参考图压平成一张图片，适合科研示意图和可维护演示材料。
- 将视觉一致性、对象结构和深层可编辑性作为独立质量门，减少 agent 一次调用即宣称完成。
- 双后端共享一套语义验收约束，便于比较不同办公绘图工具的产物。

## 风险边界

- 连续纹理、显微图、热图等无法无损转成原生矢量对象，像素级一致性不应被承诺。
- PowerPoint 仅支持 Windows 桌面版；draw.io 的 macOS/Linux 行为是尽力支持，受 Electron 打包影响。
- 科研参考图和未发表数据可能被送入模型上下文；安装远程脚本、开放本地调试接口前均需审查。

## 补充建议

先在非保密示例图上检查结构审计与导出，再处理真实论文图。把可编辑性验收、引用/版权核查和科学内容核验分开；插件通过渲染检查不代表结论或数据正确。

## 参考资料

- GitHub：<https://github.com/icebird1998/scientific-illustrator>
- draw.io Desktop：<https://www.drawio.com/>
