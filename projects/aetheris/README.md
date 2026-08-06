<!-- markdownlint-disable MD013 -->

# Aetheris（灵思 Agent）

- 仓库：[shiqiaoshangxue/aetheris](https://github.com/shiqiaoshangxue/aetheris)
- 快照：2026-08-07 抓取；GitHub API 显示其创建于 2026-08-06，约 32 stars、0 forks，MIT。数字会随时间变化。
- 分类：办公、商业与行业应用

## 定位

面向学术研究流程的 Web/桌面 Agent：作者宣称将选题、文献检索、讨论、写作、数据分析、作图、引用和审稿回复组织为九类工作流，并提供多模型路由、多个子 agent 与科学数据库接口。

## 用法

README 要求 Node.js 18+。克隆后进入其 `source/` 目录，运行 `npm install` 与 `npm run dev`，在本机 Web 面板选择工作流；未配置 provider 时为 mock 演示模式。若要使用真实模型，需在设置中填写 OpenAI、Claude 或 DeepSeek 等 provider 的 API key。项目也给出了 Electron 打包与 `npm test` 入口。

## 原理

系统把“商讨方案”和“执行方案”分开：前者以检索和澄清为主，后者由 planner、research、code、debug、analyze、write 等子 agent 分工，再由技能加载器和工作流约束串联。它将外部科学数据库检索结果、模型生成和本地产物放进同一控制面，但公开 README 中的“101 skills / 60 databases / 发表级”等覆盖范围主要是作者声明。

## 价值

对希望将研究任务拆成可见阶段、复用检索/写作模板并集中管理产物的个人研究者或小团队，它提供了较完整的工作台式原型。讨论与执行分离也有助于在高成本或高风险操作前保留人工判断点。

## 风险边界

模型生成的综述、引用、实验脚本和论文段落不构成可发表结论；文献完整性、引文准确性、统计方法、署名和版权仍必须由研究者核验。外部数据库、消息渠道与模型 provider 还会扩大网络、密钥和研究数据暴露面。仓库 README 的克隆示例指向不同的组织路径，安装前应先核对来源与发布完整性。

## 补充建议

先以无敏感的公开主题和 mock/provider 隔离环境试跑，记录每条引用的原始 DOI/URL 与检索时间；对文献综述做抽样逐条核对，对代码与分析用独立环境和基准数据复现。不要把“发表级”营销表述用于替代导师、同行评议、伦理审批或数据治理。

## 参考资料

- [项目 README](https://github.com/shiqiaoshangxue/aetheris)
- [仓库测试入口](https://github.com/shiqiaoshangxue/aetheris/tree/main/source/test)
- [GitHub API 元数据快照](https://api.github.com/repos/shiqiaoshangxue/aetheris)
