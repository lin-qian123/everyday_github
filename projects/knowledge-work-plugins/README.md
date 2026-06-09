# knowledge-work-plugins

## 项目定位
knowledge-work-plugins 是一个面向知识工作场景的插件集合仓库，核心方向是把检索、总结、写作、流程编排等能力插件化，便于在 Agent/IDE/自动化系统中复用。

- GitHub: https://github.com/skyworkai/knowledge-work-plugins
- Trending 参考: https://github.com/trending

## 用法
1. 克隆仓库并阅读插件清单与接入文档。
2. 按场景选择插件（检索、资料整理、写作辅助、任务编排）。
3. 在你的 Agent 或工作流平台中按官方方式注册插件。
4. 用真实任务小批量试跑，记录成功率、延迟与人工修订率。

## 原理
- 插件化抽象：把复杂知识工作拆成稳定可调用的能力单元。
- 上下文路由：根据任务类型选择合适插件，减少单模型硬扛全流程。
- 人机协同闭环：插件给出草案，人类做决策与最终发布。

## 价值
- 显著降低重复性知识劳动成本。
- 适合团队沉淀“可复用工作方法”而不是只沉淀文档。

## 风险边界
- 插件链路变长后，错误传播更隐蔽。
- 外部数据源质量会直接影响输出可信度。
- 涉及隐私/合规内容时必须有权限和审计约束。

## 补充建议
- 建立插件级别的验收指标（准确率、时延、可追溯性）。
- 对关键结论保留“来源证据 + 生成路径”。
- 先在低风险内容上规模化，再扩展到高风险业务。

## 参考资料
- 仓库主页：https://github.com/skyworkai/knowledge-work-plugins
- GitHub Trending：https://github.com/trending
