# easy-vibe（datawhalechina/easy-vibe）

- GitHub: <https://github.com/datawhalechina/easy-vibe>
- 核心定位：面向零基础和产品导向人群的 AI 编程课程，用“会说需求就能做应用”的方式教学。

## 1. 它解决什么问题

传统编程学习常见痛点：
- 前置知识门槛高，初学者容易在环境搭建阶段流失；
- 学习内容和“做出可演示成果”之间距离太长；
- 很多人能看懂教程，但不会把想法快速变成原型。

`easy-vibe` 通过分阶段学习路径，把“需求描述 -> AI 协作开发 -> 可运行应用”打通。

## 2. 快速使用（实践向）

```bash
git clone https://github.com/datawhalechina/easy-vibe.git
cd easy-vibe
npm install
npm run dev
# 浏览器打开 http://localhost:3000
```

落地建议：
- 先走“快速首胜”路线，尽快完成一个端到端小项目；
- 每次让 AI 生成代码时，附上明确约束（技术栈、接口、验收标准）；
- 用 issue 记录“提示词 -> 产出质量 -> 修正策略”，形成个人迭代手册。

## 3. 原理拆解（简化）

- Prompt 驱动开发：把自然语言需求转成结构化任务；
- 可视化学习路径：通过地图化章节降低学习跳跃成本；
- 交互式实践：在真实项目迭代中学习前端、后端、部署与 AI 集成。

## 4. 为什么值得关注

- 对非科班/跨界人群友好，进入门槛低；
- 内容覆盖从原型到工程交付，适合训练“产品化思维”；
- 与当下 AI IDE/Agent 工作流高度贴合。

## 5. 风险与边界

- “会说就会做”并不等于“可维护、可扩展、可上线”；
- 依赖 AI 生成代码时，容易忽略安全、性能和测试；
- 快速迭代模式下，技术债会在中后期集中暴露。

## 6. 我的补充建议

- 在课程实践中强制加入最小测试（单测/集成测试）与代码审查；
- 引入发布前检查：鉴权、日志、错误追踪、成本预算；
- 为每个项目补“手工兜底流程”，避免 AI 失效时完全停摆。

## 7. 参考资料

- 官方仓库：<https://github.com/datawhalechina/easy-vibe>
- GitHub Trending：<https://github.com/trending>
- Trendshift：<https://trendshift.io/>
