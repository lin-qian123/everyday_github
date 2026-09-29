<!-- markdownlint-disable MD013 -->

# cs249r_book（harvard-edge/cs249r_book）

> 上游仓库：<https://github.com/harvard-edge/cs249r_book> · 归类：AI 学习与教育资源 · 本页基于 2026-09-30 的 GitHub API、README、课程网站、各卷状态、Release 与 LICENSE 静态整理，未逐章审校教材、运行实验或验证教学效果。

- 抓取快照：28,718 stars、3,625 forks、6 open issues。
- 热度信号：GitHub Python Trending 抓取时约 +62 当日 stars。
- 版本与许可：GitHub API 为 `NOASSERTION`；根 `LICENSE.md` 是 CC BY-NC-SA 4.0。latest Release 为 Vol I `vol1-v0.7.2`，API 首个 tag 为 `vol2-v0.2.1`，各卷独立演进。

## 定位

这是 Harvard CS249r “Machine Learning Systems” 的开放课程与教材仓库，目标从单模型训练扩展到端到端 AI engineering。仓库同时承载四卷书、交互实验、TinyTorch、硬件 kits、MLSys·im 模拟器、StaffML 面试练习、教师 syllabus / rubric 和幻灯片，不是单一 notebook 教程。

## 用法

自学者可先读已发布的 Vol I，再按需进入 Vol II preview、交互 labs、TinyTorch 或硬件实验；教师可使用 Instructor Hub、课程地图、评分 rubric 与 Beamer slides。Vol III Agentic Systems 与 Vol IV Physical AI 仍在开发，上游明确提示不要据当前内容正式引用或授课。仓库的不同组件各有独立入口和依赖，应从对应 README 启动，而不是把整仓库当作一个 Python 包安装。

## 原理

课程按 Model → Fleet → Trajectory → Physical Plant 扩大系统边界：从单机训练 / 推理、分布式集群与可靠性，延伸到 Agent 记忆 / 工具 / 编排 / 安全，再到感知、控制和物理约束。学习循环强调 Read → Explore → Build → Model → Deploy → Practice → Teach，用模拟器和构建练习把吞吐、内存、网络、功耗与失效模式连接起来。

## 价值

它把常被拆散讲授的模型、硬件、系统、Agent 和部署放进同一工程框架，适合补齐“会训练模型但不会解释 serving / 集群 / 安全边界”的知识缺口。公开课程资产也方便教师复用结构、实验和评分思路，并能从书稿直接追到相应 lab、模拟和实现。

## 风险边界

- Vol II 仍是 preview，Vol III / IV 明确处于快速开发期；目录完整不等于内容稳定、已同行评审或可作为正式引用版本。
- MLSys·im 和交互 lab 是教学模型，不替代真实硬件、驱动、网络拓扑、成本和故障注入实验。
- StaffML、Socratiq 与 MLPerf EDU 等组件成熟度不同；面试分数、AI 导读或教学 benchmark 不能直接解释为工程能力。
- 仓库根许可是 CC BY-NC-SA 4.0，带非商业和相同方式共享要求；不能按常见宽松软件许可证处理教材、幻灯片和派生课程。
- 书稿、图片、论文链接、硬件资料和第三方依赖可能有各自权利边界；根许可不能自动重许可外部材料。

## 补充建议

学习时固定卷、tag / commit 和章节日期，区分 released、preview 与 in-development。实验报告同时记录模型假设与真实测量，模拟结果至少用一个可获得硬件样例校准。教师采用前先逐章复核链接、依赖和版权，并把 CC BY-NC-SA 的署名、非商业和 ShareAlike 要求写进课程分发流程。

## 参考资料

- [GitHub 仓库](https://github.com/harvard-edge/cs249r_book)
- [GitHub REST API](https://api.github.com/repos/harvard-edge/cs249r_book)
- [课程网站](https://mlsysbook.ai/)
- [Vol I v0.7.2 Release](https://github.com/harvard-edge/cs249r_book/releases/tag/vol1-v0.7.2)
- [Labs](https://github.com/harvard-edge/cs249r_book/tree/dev/labs)
- [TinyTorch](https://github.com/harvard-edge/cs249r_book/tree/dev/tinytorch)
- [Instructor Hub](https://mlsysbook.ai/instructors/)
- [LICENSE](https://github.com/harvard-edge/cs249r_book/blob/dev/LICENSE.md)
