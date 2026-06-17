# ppt-master（hugohe3/ppt-master）

- GitHub: https://github.com/hugohe3/ppt-master
- 官网: https://hugohe3.github.io/ppt-master/
- 记录日期: 2026-06-17 (Asia/Shanghai)

## 定位

`ppt-master` 是一个把文档、资料和提示词转成“原生可编辑 PPTX”的开源工作流。它的重点不是生成一组演示稿截图，而是生成可以继续在 Microsoft PowerPoint 中逐页编辑、带动画、带讲稿、可跟随模板的真实文件。

## 热度信号

1. GitHub API 在 2026-06-17 抓取时显示约 `28.3k stars`、`2.5k forks`。
2. GitHub API 显示仓库在 `2026-06-16` 仍有推送更新，项目活跃。
3. 项目主页和 README 反复强调“native editable PPTX”而非图片式导出，这个定位和大量 AI deck 工具形成了明显区分。

## 用法

### 1) 安装依赖

```bash
pip install -r requirements.txt
```

官方说明中，最基础的依赖是 Python 3.10+。

### 2) 获取项目

```bash
git clone https://github.com/hugohe3/ppt-master.git
cd ppt-master
pip install -r requirements.txt
```

### 3) 通过 agent 触发工作流

它不是一个独立聊天产品，而是一个可被 Claude Code、Codex、Cursor、Copilot、Aider 等 agent 工具调用的 workflow。典型输入方式是把 PDF、文稿或提纲交给 agent，然后让它按项目提供的流程产出 `.pptx`。

## 原理

1. 项目把“资料解析、结构组织、版式生成、素材组合、导出 PPTX”做成一套 workflow / skill。
2. 输出不是 HTML 幻灯片或整页图片，而是 PowerPoint 可直接编辑的 DrawingML 元素、文本框、图表和动画。
3. 模型负责内容理解和版式决策上限，workflow 负责把这些决策稳定落地成真实文件。
4. 项目同时支持模板跟随、讲稿旁白等增强能力，使产出更接近业务可交付物。

## 价值

- 对咨询、投研、教育、产品汇报和内容团队都很实用，因为最终交付物仍是熟悉的 `.pptx`。
- 它比“一键生成静态 deck 页面”更贴近真实办公流程，因为人类还能继续改稿、换图、调动画。
- 也适合作为 agent + 办公软件协作的代表案例，说明 AI 工具真正有价值的地方是帮人省掉繁琐加工环节。

## 风险边界

- 项目作者明确提醒：这不是许愿池，最终质量依赖模型能力、输入材料和使用者本身。
- 若使用低成本模型，结构与审美质量会明显下降，后续人工修稿量可能仍然较大。
- 如果资料涉密，还要单独评估模型 API 调用、素材生成和本地缓存的合规边界。

## 补充建议

1. 把它视为“高质量初稿生成器”，而不是终稿自动机。
2. 在正式业务场景中，先固定模板、品牌色和目录结构，再让 agent 生成内容，效果会稳定得多。
3. 若团队经常做相似类型的 deck，可以基于该项目沉淀自己的模板、审校清单和素材规范。

## 参考资料

- https://github.com/hugohe3/ppt-master
- https://hugohe3.github.io/ppt-master/
- https://github.com/hugohe3/ppt-master/blob/main/docs/getting-started.md
- https://ossinsight.io/trending
