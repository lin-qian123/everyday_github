# everyday_github 应用摘要

## 这是什么
`everyday_github` 是一个按日期整理的 AI 热点内容仓库，核心产物是每日热点报告与单项目解读文档。仓库当前以 Markdown 文档为主，未发现可执行应用代码。

## 面向谁
主要面向需要快速跟踪 AI 工具与社区趋势的内容研究者、技术分析者与开发者。

## 能做什么
- 按天产出 AI 热点日报（`daily/YYYY-MM-DD/ai-hotspots.md`）。
- 汇总多平台信号：GitHub、X、YouTube、Instagram（见日报结构）。
- 为单个热门项目提供中文速览卡片（如 `qwen-code/README.md`）。
- 提供“是什么/能做什么/原理/上手”的统一解读模板（多个项目目录同构）。
- 记录来源链接，方便回溯与二次验证（各 README 与日报末尾“来源/参考链接”）。
- 保留连续日期历史，支持纵向比较热点变化（`daily/` 下多日期目录）。

## 如何工作（仅基于仓库证据）
- 组件 1：项目解读层。每个项目目录（如 `99/`、`openai-skills/`）以 `README.md` 存放结构化解读。
- 组件 2：日报聚合层。`daily/<日期>/ai-hotspots.md` 聚合多平台热点与当日结论。
- 组件 3：版本管理层。`.git/` 提供历史追踪与增量更新。
- 数据流：外部平台热点信息 -> 人工或流程整理为 Markdown -> 按“项目解读/日报”落盘到仓库。
- 自动抓取脚本/调度服务/API 服务：Not found in repo。

## 如何运行（最小上手）
1. 克隆仓库并进入目录：`git clone <repo-url> && cd everyday_github`。
2. 读取当日日报：打开 `daily/<日期>/ai-hotspots.md`。
3. 深入单项目：打开对应目录下 `README.md`（如 `qwen-code/README.md`）。
4. 一键生成命令或本地运行入口：Not found in repo。
