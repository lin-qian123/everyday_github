<!-- markdownlint-disable MD013 -->

# personal-model

## 定位

`Intuition-Lab/personal-model` 是一个本地优先的 Personal Model / `HUMAN.md` 项目，项目名 Persome。它从用户授权的 macOS 活动中提取证据化上下文，并通过 MCP 给 Codex、Claude Code 和其他可信客户端提供“这个用户如何工作、如何决策、当前关注什么”的个人模型。

## 用法

README 提供 synthetic demo、真实数据安装和 MCP client 连接路径。项目要求用户授予 macOS 权限，随后在本机生成可检查、可修正、可导出、可删除的个人模型。

## 原理

Persome 把活动证据组织成多层结构：Point 是单个来源观察，Line 是关系或变化，Face 是由证据支持的模式，Volume 是跨项目/生活领域的高阶结构，Root 是当前整合模型。重要推断保留 receipts，后续证据可以强化、修正或推翻旧推断。

## 价值

- 把 agent memory 从“项目事实”推进到“用户偏好、工作方式和长期注意力”。
- MCP 接口让个人模型可被多种 AI 客户端复用。
- 本地优先、可导出和可删除是个人数据场景的基本要求。
- 对个人 AI 助理、长期研究、写作和项目管理都有潜在价值。

## 风险边界

- 个人模型会处理高度敏感活动数据，权限、存储位置、导出和删除必须严格审查。
- 模型对用户的推断可能错误或过度概括，需要可纠错机制。
- 把个人偏好注入 agent 可能提升体验，也可能放大既有盲点。
- macOS 活动捕获和 MCP 暴露都应采用最小权限。

## 补充建议

- 先用 synthetic demo 验证数据结构，再决定是否接入真实活动数据。
- 建立周期性 review：哪些推断仍然正确，哪些需要删除或降权。
- 不要把 Personal Model 与企业合规、医疗、金融建议混用，除非有明确审计和授权边界。

## 参考资料

- GitHub: <https://github.com/Intuition-Lab/personal-model>
- Website: <https://intuition-lab.github.io/personal-model/>
