<!-- markdownlint-disable MD013 -->

# Huashu Design：以真实参照、多方向初稿和 HTML 管线组织设计

- 主上游：[alchaincyf/huashu-design](https://github.com/alchaincyf/huashu-design)；repository ID `1215145625`。
- 采样日期：2026-10-27（Asia/Shanghai）；分类：前端、UI 与 Agent 交互层。
- API 累计快照：26,707 stars / 2,960 forks / 6 open issues（含 PR 口径），与榜单日增分开。
- 默认分支 `master`；本页主线静态依据固定在 `4fc7bfdbd5ec3fa2d43ce7a6433de60976a5e4b1`。发行 API 首项 [v3.0.0](https://github.com/alchaincyf/huashu-design/releases/tag/v3.0.0)，UTC 2026-10-17T11:40:41Z，正式发行标记。
- 核验层级：读取一手文档、许可、元数据与所列部分实现；未安装运行上游、调用模型或复现实验。

## 定位

Huashu Design 是跨 Agent 的设计技能包，围绕网页、交互原型、演示稿、信息图和动画输出组织工作。核心是参考资料、素材、脚本与设计流程，而不是另一个图像生成模型。主线 3.0 文档强调六个候选挑三个方向、84 种风格样张、外观账本和用户偏好。

## 用法

上游提供安装入口，本轮未执行：

```bash
npx skills add alchaincyf/huashu-design
```

安装后检查 SKILL.md 以及 references、assets、scripts、demos 是否齐全，不能只同步一个说明文件。随后在支持技能的宿主中提出具体交付要求，例如“做三页研究介绍，先给三种视觉方向，文字可编辑并标明来源”。模型、浏览器、渲染器、字体和媒体工具依任务另行准备。

导出已有 HTML 为 PPTX 的一条主线入口如下，需要 Playwright / Chromium、python-pptx 与 Pillow；本轮未执行：

```bash
python scripts/pptx_from_rendered.py deck.html -o deck.pptx --selector '.slide'
```

客户要求原有模板时，再依文档传入 `--template`、版式和公共 logo 排除参数，并检查母版继承。

## 原理

技能先读取能力、偏好和近期外观记录，再按交付媒介路由到模块；设计师思路、现实参照和风格抽样各给候选，缩略图筛选后展示真实初稿。Gate 文件记录事实、品牌和方向选择，lint 报告可测量问题，账本帮助下一次避免机械复用外观。

PPTX 有两条不同管线：新写且满足约束的 HTML 由 html2pptx.js / PptxGenJS 翻译为文本框和形状；已有视觉稿则可用浏览器渲染坐标和 python-pptx 重建，并继承客户模板。两条路径不能直接混用坐标约定。

## 价值

适合需要保留代码、真实素材和可编辑输出的快速设计迭代；把“先看方向、再精修”变成明确交付点。版式规则和事实清单也便于复核，但 README 的耗时与品质描述属于作者展示，不能当成跨任务的性能或审美保证。

## 风险边界

- **可编辑不只看扩展名**：文字、图表、图片和母版要逐类检查；复杂 SVG / CSS 可能转成图像或产生布局偏差。文字核对通过不能替代目标 PowerPoint / Keynote 渲染检查。
- README 同时保留旧版 demo 与 3.0 案例；旧视频不证明 3.0 的所有能力。脚本说明中的历史通过率也不是本轮复现结果。
- 设计体检量化的是若干结构特征，不提供事实正确、审美或功能完整的证明。品牌素材、照片、字体和音频的许可独立于代码 MIT。
- 技能会调用宿主工具、抓取素材、写交付文件；偏好与外观记录默认落在本机 `~/.huashu-design/`，仍要审查所用模型和外部素材服务的数据出口。
- 三方向、Gate 文件和用户原话是工作流约定，其约束力依宿主执行，不能当作 OS 权限机制。

## 补充建议

先做两页代表页，确定视觉和编辑方式，再扩展全稿。保留文本和数据的独立来源，分别检查 HTML 交互、导出丢字、模板母版和目标应用视觉结果；不用“导出成功”替代可编辑性与科学内容验收。

## 参考资料

- [README.md](https://github.com/alchaincyf/huashu-design/blob/4fc7bfdbd5ec3fa2d43ce7a6433de60976a5e4b1/README.md)。
- [SKILL.md](https://github.com/alchaincyf/huashu-design/blob/4fc7bfdbd5ec3fa2d43ce7a6433de60976a5e4b1/SKILL.md)。
- [references/editable-pptx.md](https://github.com/alchaincyf/huashu-design/blob/4fc7bfdbd5ec3fa2d43ce7a6433de60976a5e4b1/references/editable-pptx.md)。
- [references/pptx-from-rendered-html.md](https://github.com/alchaincyf/huashu-design/blob/4fc7bfdbd5ec3fa2d43ce7a6433de60976a5e4b1/references/pptx-from-rendered-html.md)。
- [LICENSE](https://github.com/alchaincyf/huashu-design/blob/4fc7bfdbd5ec3fa2d43ce7a6433de60976a5e4b1/LICENSE)。
- [仓库 API](https://api.github.com/repos/alchaincyf/huashu-design)、[发行 API](https://api.github.com/repos/alchaincyf/huashu-design/releases?per_page=1)；动态元数据仅代表本轮采样。
- 事实依据为以上一手材料；价值、风险判断与建议为本库工程分析，未写作实测结论。
