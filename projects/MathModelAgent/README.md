<!-- markdownlint-disable MD013 -->

# MathModelAgent（jihe520/MathModelAgent）

> 记录日期：2026-09-05（Asia/Shanghai）。本页依据上游 README、仓库结构、release 与 GitHub API 做静态整理；未运行建模任务，也未验证生成论文、引用、代码或竞赛成绩。

## 定位

`MathModelAgent` 面向数学建模竞赛和研究写作，把问题分析、模型选择、代码、绘图、论文撰写、Typst 排版与检查组织为桌面应用和一组可安装 skills。上游还保留早期 Web / backend / frontend 路径，但 README 表示后续重点转向 harness + skills。

2026-09-05 的 GitHub 官方 Python Trending 快照显示约 `+47 stars today`；REST API 快照为 `4,161 stars / 360 forks / 31 open issues`，最新 release 为 `v0.0.15`（2026-09-02）。GitHub API 未识别 SPDX 许可证，仓库根目录也没有独立 `LICENSE`；README 的版权段落写明“个人免费使用，请勿商业用途”，因此不能按常见开源许可证推定商业复用权。

## 用法

上游提供三条入口：

1. 从 Releases 下载桌面版；macOS 分 Apple 芯片和 Intel 构建，Windows 包上游明确标为当前未签名。
2. 通过 Skills CLI 安装全部建模 skills：

```bash
npx skills add jihe520/MathModelAgent --all
```

1. 用 Docker Compose 或本地 Python / Node 环境运行旧的 Web / backend / frontend 路径。

上游示例中包含 `--dangerously-skip-permissions` 和 `--yolo`。真实竞赛资料、个人文件或联网搜索场景不应照抄这些全权限参数；应在副本目录、最小网络权限和人工审批下运行。

## 原理

- **阶段化 skills**：将分析、建模、编码、绘图、写作、Typst 和验收拆成可串联或单独调用的步骤。
- **模板与知识库**：上游列出 17 套 Typst 模板、模型选择决策树和常见错误规则。
- **代码解释器**：旧路径可用本地 Jupyter 或 E2B / Daytona 等云端执行环境。
- **多角色 / 多模型**：README 描述建模、代码、论文等角色可使用不同模型。
- **验收意图**：上游描述文本泄漏、数值一致性、Typst 编译和 PDF 可视化等检查，但这些检查的覆盖率仍需逐项审计。
- **外部搜索与检索**：README 功能表提到 Tavily、ChromaDB 和 rerank；同一 README 的后期计划又标注部分功能未实现或只存在配置，因此必须以具体 commit 和实际测试为准。

## 价值

- 把数学建模论文生产链拆成可审阅步骤，比单次提示直接生成整篇论文更容易定位错误。
- Typst 模板和阶段性产物有利于统一竞赛格式，并保留进一步人工修改入口。
- skills 化后可在不同 harness 中复用部分流程，也便于只调用分析、绘图或排版环节。
- 对教学和流程研究有参考价值，可观察 agent 如何在模型、代码、证据和写作之间交接。

## 风险边界

- “1 小时完成获奖级论文”“可直接提交”等是上游愿景或宣传，不是本页验证结论。
- README 的功能特性、配置表和 TODO 对 HIL、Web Search、RAG、fallback、evaluator 的完成状态存在不一致；应按固定 release 做功能级验收。
- 自动生成模型、数据、代码、图、数值和引用都可能错误，编译通过不能证明科学正确。
- 竞赛可能限制 AI、外部资源、协作和引用方式；使用前必须阅读当届规则并如实披露。
- 桌面版、云端 interpreter、Web Search 和多模型 API 会接触题目、数据与密钥；需审计外发和日志保留。
- Windows 未签名包与全权限启动参数扩大供应链和本机执行风险。
- 许可证边界不是 OSI 常见开源许可；商业、再分发和衍生使用应先取得作者许可。

## 补充建议

- 以公开历年题建立 golden set，分别验证问题理解、公式、单位、数据来源、代码、图表、引用和结论。
- 强制保留来源 URL、抓取时间、原始数据 hash、脚本和随机种子；禁止只交最终 PDF。
- 对每个数值结论做独立重算，对每条引用回到原文核对，对关键图表回读数据范围。
- 默认关闭全权限模式，在副本仓库运行，并为联网、执行代码、覆盖文件和最终导出设置人工闸门。
- 把“功能在 README 中出现”“配置项存在”“代码路径存在”“实测可用”分成四种状态记录。

## 参考资料

- [GitHub 仓库](https://github.com/jihe520/MathModelAgent)
- [GitHub REST API](https://api.github.com/repos/jihe520/MathModelAgent)
- [v0.0.15 Release](https://github.com/jihe520/MathModelAgent/releases/tag/v0.0.15)
- [上游版权说明](https://github.com/jihe520/MathModelAgent/blob/main/docs/md/License.md)
- [在线入口](https://mathmodel.top/home)
