# aidlc-workflows（awslabs/aidlc-workflows）

- GitHub: <https://github.com/awslabs/aidlc-workflows>
- 核心定位：把 AI 编程助手纳入可治理的软件开发生命周期（AI-DLC），通过规则文件与阶段流程降低“直接生成代码”带来的不确定性。

## 1. 它解决什么问题

团队在引入 AI 编码时常见痛点：
- 需求、设计、实现、验证缺乏统一节奏；
- 不同 agent 产出风格不一致，复现困难；
- 人在回路控制不足，导致质量和合规风险上升。

`aidlc-workflows` 提供的方法是“先流程后生成”：让 agent 在结构化阶段中工作。

## 2. 快速使用（实践向）

```bash
# 1) 从 release 下载 ai-dlc-rules 压缩包并解压
# 2) 将 core-workflow.md 复制为项目根 AGENTS.md
# 3) 将 rule-details 复制到 .aidlc-rule-details/
# 4) 在会话里以“Using AI-DLC, ...”触发流程
```

落地建议：
- 先在一个中等复杂度项目试点，验证流程开销与收益；
- 把安全/测试扩展规则先落地，再扩展到更多规范；
- 将关键产物（计划、风险、测试策略）纳入代码评审。

## 3. 原理拆解（简化）

- 三阶段自适应：Inception（定义问题）→ Construction（实现与验证）→ Operations（运维方向）；
- 风险驱动：复杂变更走更完整流程，简单改动保持轻量；
- 人在回路：关键阶段需人工确认，避免全自动失控。

## 4. 为什么值得关注

- 适合希望“规模化使用 AI 编码”而不是“偶尔试验”的团队；
- 强调可复现与治理，利于合规场景（金融、企业内平台）；
- 对多 agent 协作项目尤其有价值。

## 5. 风险与边界

- 流程成本：短平快任务可能感到“文档负担”；
- 执行质量依赖：规则写得好坏会直接影响 agent 表现；
- 并非银弹：仍需要测试、评审与工程判断。

## 6. 我的补充建议

- 先定义“何时可以跳过阶段”的团队规则，避免流程过重；
- 为不同任务类型建立模板（缺陷修复、重构、新功能）；
- 定期复盘 aidlc-docs 与真实缺陷，反向优化规则集。

## 7. 参考资料

- 官方仓库：<https://github.com/awslabs/aidlc-workflows>
- AWS Labs 发布信息（仓库 README 内链接）
- GitHub Trending：<https://github.com/trending>
