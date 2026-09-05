<!-- markdownlint-disable MD013 -->

# dive-into-llms（Lordog/dive-into-llms）

> 记录日期：2026-09-06（Asia/Shanghai）。本页依据上游 README、章节目录、release 与 GitHub REST API 做静态整理；本轮未运行 notebook、未检查所有外部课程依赖，也未复现任何模型训练或安全实验。

## 定位

`dive-into-llms` 是由上海交通大学相关课程讲义扩展而来的中文大模型编程实践教程，面向课程设计和科研入门。内容以课件、章节说明和 Jupyter Notebook 组织，覆盖微调部署、prompt/CoT、知识编辑、数学推理、水印、越狱、隐写、多模态、GUI agent、agent safety 与 RLHF 安全对齐。

2026-09-06 的 GitHub 官方 Jupyter Notebook Trending 抓取显示约 `+186 stars today`；REST API 快照为 `52,004 stars / 6,216 forks / 15 open issues`，最新 release 为 `v1`。仓库根目录没有 LICENSE，GitHub API 也未识别许可证，因此“公益、免费”不能解释为允许任意复制、修改或再分发。

## 用法

该项目不是单一可安装包，适合按章节阅读 README、课件并在隔离环境运行 notebook。例如先从 `documents/chapter1` 的微调/部署或 `chapter2` 的提示学习开始，再进入安全和 agent 章节。

建议将每章 notebook 复制到独立环境，逐项检查模型、数据、API key、硬件和版本；不要直接在含个人凭据的主环境运行旧依赖或攻击演示。

## 原理

- **章节化实践**：每个主题组合课件、文字教程与 notebook/script，便于从概念进入代码。
- **任务递进**：从基础微调和 prompting 延伸到知识编辑、数学推理、多模态与 GUI agent。
- **安全专题**：水印、越狱、隐写、agent risk awareness 与 RLHF 对齐将攻击/防御问题放入可操作练习。
- **国产软硬件路线**：README 另列与昇腾社区合作的“大模型开发全流程”课程，覆盖初中高级材料、实验手册和视频。
- **教学来源**：项目说明由上海交通大学课程讲义拓展，并列出多所机构贡献者。

## 价值

- 中文课件、说明和代码降低 LLM/agent 实践的入门门槛。
- 同时覆盖建模、部署、安全和多模态，适合形成课程阅读地图或实验选题池。
- 安全章节让学生看到模型能力之外的越狱、隐写、水印和 agent 风险问题。
- Notebook 形式便于逐单元重跑、改参数和记录观察，但结果仍依赖环境与外部资产。

## 风险边界

- 仓库最新 push 为 2025-10-10；2026-09-06 的 Trending 是关注度信号，不代表依赖、API、模型或最佳实践仍是最新状态。
- 根目录无 LICENSE；免费阅读不等于具备复制、改编、商用或分发授权，课件、图片、数据和外部视频还可能有各自权利。
- 上游免责声明也明确内容来自个人经验与公开材料且不保证完全正确；教程不能作为论文结论或生产设计的唯一依据。
- 越狱、隐写和 GUI agent 实验可能涉及攻击内容、真实账号或外部动作，只能在授权、隔离、低权限环境运行。
- Notebook “运行成功”只说明特定环境完成，不证明模型质量、公平性、安全性、数据许可或现实效果。
- 外部 API、模型和昇腾课程页面可能发生版本漂移，复现时必须记录日期、revision 和依赖锁定。

## 补充建议

- 先建立每章环境清单，固定 Python、CUDA/昇腾工具链、模型 revision、数据集版本和随机种子。
- 为每个实验增加预期输出、失败模式、费用/显存上限与清理说明，结果保存为可复核 notebook 或日志。
- 安全章节使用合成账号、本地靶场与书面授权，不让 GUI agent 连接个人购物、消息或支付账户。
- 在复用课件、图片、代码或数据前逐项确认许可证，并推动上游补充清晰的根许可证说明。
- 将教程中较旧的 API/模型声明与 2026 年官方文档交叉核验，明确“原教程”“更新后实现”和“本地实测”三层。

## 参考资料

- [GitHub 仓库](https://github.com/Lordog/dive-into-llms)
- [GitHub REST API](https://api.github.com/repos/Lordog/dive-into-llms)
- [v1 Release](https://github.com/Lordog/dive-into-llms/releases/tag/v1)
- [课程章节目录](https://github.com/Lordog/dive-into-llms/tree/main/documents)
- [README](https://github.com/Lordog/dive-into-llms/blob/main/README.md)
- [昇腾大模型开发学习专区](https://www.hiascend.com/edu/growth/lm-development#classification-floor-1)
