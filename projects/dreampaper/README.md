# dreampaper

## 定位

`dreampaper`（DreamPaper）是本地运行的科研配图与学术幻灯片生成应用。它为科研图选取参考模板，为幻灯片读取用户母版，再分别调用可配置的 Design、Implement 和 Search 模型生成内容，前端采用 React/Vite，后端采用 FastAPI。

截至 2026-07-30，GitHub API 显示仓库创建于 2026-07-29，约 8 stars、1 fork，未声明 SPDX 许可证；这是早期开发者信号。未明确许可时，不应把代码、示例或生成工作流默认用于商业分发。

## 用法

科研绘图模式需要用户自行下载 PaperBananaBench 参考库；幻灯片模式需要上传有权使用的母版。建立虚拟环境、安装 Python/Node 依赖后，分别启动后端和前端，服务默认监听本机地址。

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
npm install
uvicorn backend.app.main:app --reload --host 127.0.0.1 --port 8000
```

## 原理

项目把设计拆成“先抽取结构/母版、再填入内容”的两阶段：参考图或母版提供版式与视觉约束，模型配置决定具体生成；资料中的产品/仪器还可触发检索，以减少用文字框替代真实对象的情况。配置、上传资产和任务记录存于 `~/.dreampaper/`。

## 价值

- 试图把科研图和学术 slides 从一次性提示词变成可复用模板驱动流程。
- 本地保存配置与产物，便于把模型供应商选择和素材管理留在用户控制范围内。

## 风险边界

- 图像模型可能生成错误结构、失真数据、不可读文本或不可靠的仪器/产品细节；科研图必须回到原始数据、方法和人工审稿。
- 模板、母版、PaperBananaBench 与检索图片分别有版权和许可边界，用户须确认有权上传、再利用与发布。
- 本地文件夹仍可能含 API key、未发表数据与上传材料；多用户机器需限制权限与备份范围。

## 补充建议

只将其用于草图和可编辑初稿。最终交付前重绘数据图、检查比例尺/单位/统计口径，逐页核验引用、图源和可访问性；并先向作者确认仓库整体许可证。

## 参考资料

- GitHub：<https://github.com/dream-rec/dreampaper>
- GitHub API 快照：<https://api.github.com/repos/dream-rec/dreampaper>
- PaperBananaBench：<https://huggingface.co/datasets/dwzhu/PaperBananaBench>
